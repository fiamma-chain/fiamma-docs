---
description: >-
  Below is a high-level, preliminary design for the BitVM-based trustless
  Bitcoin bridge. We offer customizable implementations tailored to meet the
  unique needs of each partner.
---

# Introduction

### What Is a Trustless Bitcoin Bridge?&#x20;

Our trustless Bitcoin bridge provides secure, permissionless transfers of BTC between Bitcoin and sidechains. It ensures:

1. **Locked BTC Safety**: User's BTC remains secure, without unilateral control by any entity.&#x20;
2. **Trustless PEG-IN**: Bitcoin to sidechain transfers are fully permissionless.&#x20;
3. **Trustless PEG-OUT**: Sidechain to Bitcoin transfers maintain the same security and trustlessness.Comment.

### How Do We Secure Locked BTC? <a href="#how-do-we-secure-locked-btc" id="how-do-we-secure-locked-btc"></a>

* **Traditional Approach**: A committee controls your BTC, meaning they could spend it without your consent.
* **Our Solution**: BTC is co-controlled by the user and the committee, requiring both signatures, powered by pre-signed transactions with BitVM2 functionality. This setup prevents the committee from spending BTC without user authorization.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FNaWxhWAPbrPeq8rIwJHB%2Fuploads%2FmvPKn7Uxjy9UAC4GRHY8%2Fwhiteboard_exported_image%20(9).png?alt=media&#x26;token=ed87535f-4c3a-4fdd-98dd-3906537377d6" alt=""><figcaption></figcaption></figure>

### PEG-IN Process (Bitcoin to Sidechain) <a href="#peg-in-process-bitcoin-to-sidechain" id="peg-in-process-bitcoin-to-sidechain"></a>

To receive wrapped BTC on the sidechain, our system verifies transactions through a Bitcoin light client to ensure validity, preventing issues like:

1. **Incorrect Minting**: The Mint contract checks the validity of transactions on Bitcoin, ensuring that only authentic BTC transactions allow minting on the sidechain.
2. **Relayer Issues**: Users can directly submit valid data for minting if relayers are unavailable. Security is maintained by a slashing mechanism, with decentralized or permissionless relayers depending on the chain.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FNaWxhWAPbrPeq8rIwJHB%2Fuploads%2FhkKM2aBbjwlB1GgajUxn%2Fwhiteboard_exported_image%20(10).png?alt=media&#x26;token=1f6bd22c-8476-4967-a899-62f18a326582" alt=""><figcaption></figcaption></figure>

### PEG-OUT Process (Sidechain to Bitcoin) <a href="#peg-out-process-sidechain-to-bitcoin" id="peg-out-process-sidechain-to-bitcoin"></a>

1. **General Mode**: Users initiate BTC transfers back to Bitcoin. The system verifies transactions for legitimacy, preventing fraudulent claims by operators through challenge periods with zero-knowledge proof (ZKP) verifications.
2. **Forced Exit Mode**: If the bridge or operator is down, users can withdraw BTC directly, with protections in place to penalize invalid claims.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### **Key Features and Security Levels**

* **Locked BTC**: Secured with multisignature authorization.
* **PEG-IN**: Trust-minimized with light client verification, ensuring permissionless operations.
* **PEG-OUT**: Fully trustless and permissionless, with user-centric protections in place.

### **Efficiency and Future Enhancements**

To reduce transaction times, our ZKP verification layer ensures prompt and final verification, aiming to reduce the current 7-day challenge period to a few hours. We are also working to support variable BTC amounts with a new liquidity provider design to increase bridge flexibility.

