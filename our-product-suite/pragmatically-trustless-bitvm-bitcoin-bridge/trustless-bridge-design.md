---
description: >-
  Below is a high-level, preliminary design for Fiamma Bridge (the BitVM-based
  pragmatically trustless Bitcoin bridge). We offer customizable implementations
  for each partner.
hidden: true
---

# High-level Design of Fiamma Bridge

## What is a Trustless Bitcoin Bridge?

Our trustless Bitcoin bridge provides secure, permissionless transfers of BTC between Bitcoin and sidechains. It ensures:

1. **Locked BTC Safety**: User's BTC remains secure, without unilateral control by any entity.
2. **Trustless PEG-IN**: Bitcoin to sidechain transfers are fully permissionless.
3. **Trustless PEG-OUT**: Sidechain to Bitcoin transfers maintain the same security and trustlessness.

## How Do We Secure Locked BTC?

* **Traditional Approach**: A committee controls your BTC, meaning they could spend it without your consent.
* **Our Solution**: BTC is co-controlled by the user and the committee, requiring both signatures, powered by pre-signed transactions with BitVM2 functionality. This setup prevents the committee from spending BTC without user authorization.

<figure><img src="../../.gitbook/assets/whiteboard_exported_image (9).png" alt="" width="600"><figcaption></figcaption></figure>

## PEG-IN Process (Bitcoin to Sidechain)

To receive mamaBTC (tokenized BTC via Fiamma bridge)  on the sidechain, our system verifies transactions through a Bitcoin light client to ensure validity, preventing issues like:

1. **Incorrect Minting**: The Mint contract checks the validity of transactions on Bitcoin, ensuring that only authentic BTC transactions allow minting on the sidechain.
2. **Relayer Issues**: Users can directly submit valid data for minting if relayers are unavailable. Security is maintained by a slashing mechanism, with decentralized or permissionless relayers depending on the chain.



<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

## PEG-OUT Process (Sidechain to Bitcoin)

1. **General Mode**: Users initiate BTC transfers back to Bitcoin. The system verifies transactions for legitimacy, preventing fraudulent claims by operators through challenge periods with zero-knowledge proof (ZKP) verifications.
2. **Forced Exit Mode**: If the bridge or operator is down, users can withdraw BTC directly, with protections in place to penalize invalid claims.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Key Features and Security Levels

* **Locked BTC**: Secured with multisignature authorization.
* **PEG-IN**: Trust-minimized with light client verification, ensuring permissionless operations.
* **PEG-OUT**: Fully trustless and permissionless, with user-centric protections in place.

## Efficiency and Future Enhancements

* To reduce transaction times, our ZKP verification layer ensures prompt and final verification, aiming to reduce the current 7-day challenge period to a few hours.
* [We are also working to support variable BTC amounts with a new liquidity provider design to increase bridge flexibility.](#user-content-fn-1)[^1]
* ...

[^1]: revise later
