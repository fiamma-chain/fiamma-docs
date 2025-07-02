# Users

**Security is the top concern for BTC bridge users, which is why we built Fiamma Bridge—a trust-minimized and hack-resistant BTC bridge designed to drastically reduce (or even eliminate) security risks for users.**

When using a bridge, users primarily care about three questions:

1. **Is the BTC held in a centralized manner?**
2. **Can I trustlessly bridge to another blockchain?**
3. **Can I trustlessly redeem my BTC?**

Below, we address each question in detail.

***

#### 1. Is the BTC held in a centralized manner?

**No.** Fiamma Bridge adopts an **ISA (Interactive Signature Aggregation) architecture.**

* User BTC is **not** controlled by a single address or a fixed multisig address, but by **dynamic multisig addresses**, significantly reducing hacking risks.
* In traditional single-sig or fixed multisig setups, if hackers (or malicious insiders) obtain enough private keys, **all bridge assets can be stolen.**
* With dynamic multisig, **such attacks are 100% prevented** because:
  * The **user themselves is one of the signers**, and the other signers (e.g., the Bridge Committee) are counter-parties.
  * For example:
    * User A’s BTC is co-controlled by User A + the Bridge Committee.
    * User B’s BTC is co-controlled by User B + the Bridge Committee.
    * **No overlap exists between users’ signing groups.**
  * Even if the Committee turns malicious, they **cannot steal User A’s BTC without User A’s signature**—a fundamental difference from traditional bridges.
* For technical details, see: Hack-Resistant Design.

***

#### 2. Can I trustlessly bridge to another blockchain?

**Yes.**\
Take bridging to Ethereum as an example:

* Fiamma’s bridge smart contract consists of two parts:
  1. **Bitcoin Light Client Contract** (verifies BTC transactions).
  2. **FiaBTC Contract** (mints 1:1 pegged wrapped BTC, i.e., FiaBTC).
* The `mint` function in FiaBTC is designed for permissionless execution—**anyone can mint FiaBTC by submitting valid proof** (e.g., a Merkle proof of their BTC deposit).

**Implementation Roadmap:**

* **Phase 1 (Initial):**
  * The `mint` function is guarded by an **Owner**, who must verify and submit a valid Bitcoin transaction to mint FiaBTC.
  * Users rely on the Owner’s **liveness** but are protected from arbitrary minting (the Owner cannot inflate FiaBTC supply).
* **Phase 2 (Permissionless):**
  * Users can **self-submit Bitcoin transaction proofs** to mint FiaBTC **without trusting any third party.**
  * This method is more secure but requires extra user effort (e.g., signing and submitting mint transactions).
* **Hybrid Approach:**
  * Fiamma will **combine both methods**: Users can either wait for the Owner or **trigger minting themselves if the Owner is unresponsive.**

***

#### 3. Can I trustlessly redeem BTC?

**Not yet, but minimal trust is required.**

* Users currently depend on the **liveness of the Operator Group** (at least one Operator must be online to process withdrawals).
* **Operators are permissionless and economically incentivized**:
  * Many Operators exist in the network, competing to serve users for rewards.
  * Users only need to trust that **one honest Operator is online during withdrawal.**
* **Future Work:**
  * Fiamma is researching ways to **eliminate Operator dependency entirely**, enabling fully trustless redemptions. Feasibility is under evaluation.
