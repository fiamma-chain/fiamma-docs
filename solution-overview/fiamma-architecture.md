---
description: >-
  The following diagram illustrates the comprehensive workflow of the Fiamma
  chain, highlighting the processes involved in handling and verifying
  Zero-Knowledge Proofs (ZKP) and the interactions between
---

# Fiamma Architecture

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Fig3. The arvhitecture of Fiamma</p></figcaption></figure>

### Components Involved:

1. **Mobile Phone Nodes:** User-operated nodes that generate and submit proofs.
2. **Babylon AVS Nodes:** Nodes participating in the Babylon AVS (Actively Validated Services) consensus mechanism.
3. **Namespace:** Different namespaces represent various application-specific data streams.
4. **Front-End Service:** Receives proofs from different applications.
5. **Back-End Service:** Processes proofs and sends them to the Data Availability (DA) layer and various blockchains for verification.
6. **Internal and External Layers:** Layers of nodes handling different levels of processing and validation.
7. **Ethereum, Bitcoin, and Others:** Blockchains where data and signatures are verified.

### Steps:

#### Step 1: Proof Generation and Submission

* **Mobile Phone Nodes:**
  * Generate proofs and submit them to different namespaces within the front-end service.

#### Step 2: Receiving Proofs

* **Front-End Service:**
  * Receives proofs from various applications through different namespaces (Namespace-1, Namespace-2, etc.).
  * Forwards these proofs to the Babylon AVS nodes for validation.

#### Step 3: Validation by Babylon AVS Nodes

* **Babylon AVS Nodes:**
  * **Node\_0 (Initial Node):** Receives proofs and starts the validation process.
  * **Internal Layer :** A smaller, more centralized layer of nodes that further processes the proofs.
  * **External Layer :** A larger, more decentralized layer of nodes that performs additional validation, ensuring robustness and scalability.
  * Nodes in the internal and external layers validate proofs and generate signatures using BLS/Schnorr schemes.

#### Step 4: Back-End Service Processing

* **Back-End Service:**
  * Receives the validated signatures from the nodes.
  * Processes the proofs and prepares the data for sending to the DA layer and various blockchains.

#### Step 5: Sending Data and Signatures

* **Back-End Service:**
  * Sends the processed data to the Data Availability (DA) layer to ensure secure and transparent storage.
  * **Send Signatures:** Transmits the signatures to blockchains such as Ethereum, Bitcoin, and others for verification.
* **Data Availability (DA) Layer:**
  * Stores the processed data securely, ensuring its availability and integrity.
* **Ethereum, Bitcoin, and Other Blockchains:**
  * Perform final checks and verifications of the signatures and data, ensuring comprehensive validation across different networks.
