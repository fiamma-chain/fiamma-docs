# Operators

The Operator plays a crucial role in the BitVM2 Bridge. They advance BTC payments to users from their own funds, then reclaim equivalent BTC that was locked by other users after a fixed challenge period. Below, we explain this process in detail to demonstrate how Operators function within the bridge and clarify the underlying trust assumptions.

## Deposit Phase

The deposit process consists of two steps:

1. Transfer: The user initiates a deposit transaction, transferring BTC to a taproot address. This address is jointly controlled by both the user and the committee.
2. Pre-sign: The user, committee, and operator collaboratively pre-sign a set of transactions that define the spending rules for this address. These include:
   1. Claim transaction: The operator initiates this transaction to reclaim BTC after completing payment to the user.
   2. Challenge transaction: A challenger submits this transaction if they identify malicious activity by the operator.
   3. Assert transaction: The operator uses this transaction to respond to any challenges.
   4. Happy take transaction: When no challenges are raised, the operator submits this transaction to reclaim BTC while collecting the service fee.
   5. Unhappy take transaction: If a challenger acts maliciously, the operator submits this transaction to reclaim BTC while collecting both the service fee and challenge fee.
   6. Disprove transaction: If the operator is proven malicious, they fail to reclaim BTC and forfeit their staked amount.

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (13).png" alt="" width="375"><figcaption></figcaption></figure>

* How is the Operator's BTC utilized in the deposit phase?

The Operator uses their UTXOs to pre-sign the claim transaction. The primary purpose of these UTXOs is to cover at least the gas fees for either the happy path or unhappy path scenarios. This process is illustrated in the following diagram.

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (14).png" alt="" width="375"><figcaption></figcaption></figure>

The fixed setup amount is currently 10,000 sats, supporting a maximum feerate of 10 sats/vbyte. **These UTXOs remain entirely under the operator's control**. To enable parallel processing of multiple deposits, the operator must maintain a sufficient quantity of independent UTXOs at all times.

Maintaining an adequate number of UTXOs ensures operators can consistently deliver optimal user experiences. To facilitate this, we've implemented an automated solution that helps operators maintain the required UTXO balance

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (15).png" alt="" width="563"><figcaption></figcaption></figure>

The process follows a straightforward design. Each PegIn operation consumes one UTXO while generating either one or two new UTXOs for the PegIn address. These newly created UTXOs can then be directly utilized for subsequent PegOut operations. This mechanism has demonstrated reliable performance during our beta testnet phase.\


* How much does the operator need to prepare for the PegIn address?

Ideally, the more UTXOs, the better. This means that even if transaction numbers increase rapidly in a short time, there will be no negative impact on user experience. Our bridge can also function properly when operators don't maintain too many UTXOs (or too much BTC), as we have permissionless operators. Each subset of them can handle deposits separately.

Generally, we provide operators with several options, ranging from 2,000 UTXOs to 10,000 UTXOs. If an operator chooses to start with 2,000 UTXOs, they only need to prepare 0.2 BTC for the PegIn address. If an operator selects 10,000 UTXOs, they need to prepare 1 BTC.

Obviously, more UTXOs provide more yield opportunities. We won't cover this here; you can read about operator yield.In summary, for the deposit phase, the operator needs to:

1. Prepare between 0.2 to 1 BTC to support multiple PegIn processes simultaneously
2. Maintain full self-custody of these BTC

## Withdrawal Phase

The withdrawal process includes 2 steps:

**PegOut process**

In this step, the operator needs to maintain a PegOut address that is separate from the PegIn address for better UTXO management. Note that the operator retains full control of the PegOut address.

When a user submits a withdrawal request and Operator A accepts it, Operator A must:

* Pay the user in advance using their own BTC
* Verify the request's validity before processing the payment

The key validation checks include:

* Confirming the burn transaction's validity on the sidechain
* Determining whether another operator has already processed this request

The following diagram illustrates how we address these requirements.

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (16).png" alt="" width="563"><figcaption></figcaption></figure>

1. User burns FIABTC on Ethereum and specifies both the receiver address and the operator.
2. The bridge sends this request to the specified operator.
3. The operator program handles the checking process automatically. If there is an error, the program refuses to handle it.

* By adopting this approach, the operator doesn't need to trust anything but themselves.



**Claim process**

When the operator isn't concerned about the payment process, their next priority is how to reclaim BTC permissionlessly.&#x20;

Remember that during the deposit phase, the user, operator, and committee pre-signed transactions specifying how the operator can reclaim BTC. These transactions are utilized in this phase.&#x20;

Now, we can state that the sole requirement for reclaiming BTC is that an honest operator must provide valid proof for the PegOut transaction. We'll demonstrate how the operator can reclaim BTC in various scenarios.\


* Happy case: all challengers are honest

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (17).png" alt="" width="563"><figcaption></figcaption></figure>

1. After the operator successfully pays the user, the operator generates proof to confirm completion of the payment process.
2. The operator stores the proof in the claim transaction, initiating the challenge period. We set this challenge period to 6 block time because our design ensures sufficient active challengers (a significant improvement over traditional solutions).
3. Since the proof is completely valid, no challenger raises a challenge, allowing the operator to reclaim the BTC after the challenge period expires.\


* Unhappy case: One of the challengers is dishonest

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (18).png" alt="" width="563"><figcaption></figcaption></figure>

1. After the operator successfully pays the user, the operator generates proof showing completion of the payment process.
2. The operator stores the proof in the claim transaction, starting the challenge period. We set this period to  6 block time because our design ensures sufficient active challengers (a significant improvement over traditional solutions).
3. A **dishonest challenger** attempts to raise a challenge to block the operator from reclaiming BTC. However, since the operator is honest and the challenger cannot provide evidence of malicious activity, **the challenge fails**.
4. The operator submits the Assert transaction to respond to the challenge.
5. After a shorter challenge period, the operator submits the unhappy take transaction to reclaim BTC.



* Edge case: The operator can still get BTC

We would say that our solution is a 100% operator-friendly solution. The reason is that even if there is a potential bug in the challenger process, the operator could still get BTC back.

It benefits from our reward mechanism design. To let all challengers who raise challenges get rewards, we improved the reward mechanism in the original BitVM bridge design. In the original design, the challenger who sends the challenge tx won't get a reward, and only the one who sends the disprove tx can get a reward directly.

This design discourages challengers from raising challenges when the operator is malicious. So in our design, the reward will be transferred to the committee. The committee will deliver the reward to all challengers. We think it's better than the previous design because we can ensure all members who help slash malicious operators will get rewards, even if it means trusting the committee. For challengers, getting a reward with trust > getting no reward.

The reason why the operator could benefit from it is that when the operator is honest but a malicious challenger slashes the operator successfully, the operator could appeal to the committee, because BTC is transferred to the committee. Our committee members will be our important partners, such as our lead investors, ecosystem partners, etc. They would be willing to transfer BTC to the operator in order to maintain the bridge's operation.

\
In summary, during the withdrawal phase, the operator will:

1. Maintain full control of their BTC in the PegOut address
2. Reclaim BTC permissionlessly as long as they remain honest. They only need to trust the Bitcoin network.

## Setup Phase

In the setup phase, the operator only needs to stake 0.1 BTC as collateral in a taproot address. This taproot address has 2 spend paths:

1. operator\_pk + hash timelock: 100% controlled by the operator, but with a timelock, meaning that when the timelock expires, the operator can spend it permissionlessly
2. operator\_pk + committee: pre-signed with the disprove tx. This ensures that when the operator is malicious, the collateral will be slashed permissionlessly
