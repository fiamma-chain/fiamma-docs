# Challengers

The **larger the challenger group**, the **more secure the bridge becomes**. The challenger role is **permissionless**—anyone can become a challenger by running the designated [challenger program.](../user-guides/testnet-beta/how-to-run-a-challenger.md)

Challengers interact with the bridge’s funds in two ways:

1. **Staking**
2. **Rewards**

**1. Staking (Self-Custodied & Time-Locked)**

* Challengers stake their own BTC in a **self-custodied** manner.
* The staked funds are locked in a **timelocked UTXO**, which can only be withdrawn **after the timelock expires** (typically **3–12 months**, matching the challenger’s tenure).
* Once the timelock ends, challengers can **permissionlessly reclaim their BTC** without relying on any third party.

**2. Rewards (Distributed by the Committee)**

* When a challenge succeeds:
  * The **operator’s slashed collateral** is transferred to a **committee-controlled address**.
  * The committee then **distributes rewards** to participating challengers based on their contribution.

