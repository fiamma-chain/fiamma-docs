# Permissionless Slashable Protocol

**Permissionless slashing capability is the most critical feature of the BitVM2 bridge, effectively preventing operator maliciousness.**

In the BitVM2 protocol, we prioritize establishing a **permissionless slashing mechanism** for the operator:

* If the operator submits an **invalid claim**, slash them permissionlessly.
* If the operator **fails to respond to a challenge**, slash them permissionlessly.
* If the operator **does not post witness data on the destination chain**, slash them permissionlessly.
* If the operator **posts incorrect witness data on the destination chain**, slash them permissionlessly.\
  ...

We have built a **comprehensive mechanism** to detect and penalize operator misconduct. This design ensures:

> **"As long as there is one honest challenger, a malicious operator will be slashed—guaranteeing 100% bridge security."**

At the same time, we protect **honest operators**. If the operator acts honestly, they will always receive their BTC. To achieve this, we also implement a **permissionless slashing mechanism for challengers**:

* If a challenger **maliciously leaks the secret value `s_i`**, their collateral is slashed permissionlessly on the destination chain (typically in FIABTC).
* The bridge committee will then **transfer the BTC to the honest operator**.

This ensures that challengers gain **nothing** from:

* Submitting a fraudulent `disprove_2` transaction, or
* Maliciously leaking the secret value `s_i`.
