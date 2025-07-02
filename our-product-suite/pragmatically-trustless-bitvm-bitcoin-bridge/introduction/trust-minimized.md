# Trust-Minimized

The **Fiamma Bridge** is a revolutionary new solution for cross-chain BTC asset transfer. Unlike traditional multisig bridges, the BitVM2 Bridge achieves:

1. **BTC Safety**: Your BTC stays secure—no one can move it without your approval and signature.
2. **PEG-IN Safety**: Users can mint the exact amount of FiaBTC (tokenized BTC minted via Fiamma Bridge) on a specific destination chain.
3. **PEG-OUT Safety**: Users can withdraw safely from the destination chain at any time, converting FiaBTC into equivalent BTC.
4. **Exactly Pegged Value**: FiaBTC on the destination chain is always backed 1:1 by BTC on Bitcoin, ensuring that FiaBTC : BTC = 1:1.

The BitVM2 Bridge minimizes trust assumptions. When bridging BTC to another chain, users no longer have to worry about the security of their locked BTC. Similarly, withdrawing BTC from the other blockchain no longer depends on multisig holders' signatures.

### How Do We Secure Locked BTC?

Traditional solution: The **Multisig Committee** controls your BTC, so they **can** spend it without your signature.

Innovative solution: **The user and the** **Covenant Committee** control the user's BTC together. Therefore, the committee **can't** spend it without the user's signature.

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (9) (1).png" alt="" width="563"><figcaption></figcaption></figure>

But, when you want to take your BTC back, you need to trust the Committee as well. How do we solve this problem? **To emulate the OP\_CTV opcode, the user and the bridge committee will pre-sign a few transactions to specify how these BTC could be spent in the future. This feature is enabled by BITVM2.**

### High-Level Summary of PEG-IN (Deposit) and PEG-OUT (Withdrawal) Processes

#### **PEG-IN: Moving BTC to the destinatoin chain**

1. Users lock BTC in a multisig address shared with the Bridge Covenant Committee (BCC), ensuring both the users and committee control the BTC together.
2. Pre-signed rules dictate how locked BTC can be spent.
3. Relayer synchronizes Bitcoin block data to the destination chain.
4. Minter verifies the transaction and mints an equivalent amount of FiaBTC on the destination chain for the user.

**Key Security Point:** BTC stays in shared custody, and FiaBTC is only minted after a valid deposit is confirmed via Bitcoin consensus and light client verification.

#### **PEG-OUT: Moving FiaBTC Back to Bitcoin**

1. Users burn FiaBTC on the destination chain to initiate a withdrawal.
2. The operator validates the burn and pre-pays the equivalent BTC to the user.
3. A kick-off transaction allows the operator to reclaim the locked BTC after a challenge period.
4. Honest operators receive their BTC back; malicious operators are penalized, and challengers are rewarded.

**Key Security Point**: Bitcoin itself acts as the final validator, ensuring only valid withdrawals occur, with dispute resolution mechanisms protecting against malicious actions. We only require one honest challenger to initiate a challenge and anyone can become a challenger easily, making the trust assumptions nearly trustless. With significant rewards at stake and a straightforward, permissionless challenge process, rational actors are strongly incentivized to participate.

**Bitcoin's dispute resolution capabilities are fundamentally enabled by our implementation of** [**fragmented ZK verifier**](https://x.com/Fiamma_Chain/status/1830824142826086608) **in Bitcoin Script in July 2024, an indispensable and defining module of the BitVM bridge.**
