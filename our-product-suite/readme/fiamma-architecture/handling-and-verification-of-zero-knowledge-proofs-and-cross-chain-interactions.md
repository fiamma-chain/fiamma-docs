---
description: >-
  The following diagram illustrates the comprehensive workflow of the Fiamma
  verification layer.
---

# ZKP Verification Process



<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Fig4. Sequence diagram for the Fiamma network</p></figcaption></figure>

## Components

* **Public Chains:** These are the major blockchain networks like Bitcoin and Ethereum, where final transactions and state updates are recorded.
* **ZK Apps:** Applications that generate and aggregate Zero-Knowledge Proofs, ensuring privacy and integrity of transactions.
* **Objective Nodes:** Nodes participating in the Proof-of-Stake consensus mechanism to validate proofs.
* **Intersubjective Nodes :** User-operated nodes run on mobile devices involved in fetching,  verifying, and submitting proofs.
* **Fiamma Chain:** The core network handling the verification of Zero-Knowledge Proofs built with Cosmos SDK
* **DA :** Data Availability layer that stores proof-related data securely.
* **Staking:** Mechanism within the Fiamma ecosystem responsible for staking operations and state updates.
* **Finalize:** Finalization layer where transactions and state updates are recorded on the Bitcoin blockchain.

## Workflow Steps

**Step 1: Proof Submission and Aggregation**

* **ZK Apps:**
  * Submit individual proofs to the Fiamma network.
    * **Aggregate Proofs(Optional):** Aggregate proofs before submission to save costs. Note that this can increase the processing time from seconds to hours depending on the situation.

**Step 2:Objective Finality and Consensus**

* **Objective Nodes (PoS):**
  * **Begin Objective Finality:** The process to reach consensus on the submitted proofs begins.
  * **Consensus:** Nodes collaborate to validate the proof, ensuring its accuracy.
  * **Send Hash, Proof Results, and Multi-Signatures:** The validated proof, along with hash and signatures, is sent to the DA module.
* **Fiamma Chain:**
  * **Return Commitment:** The chain returns the commitment to the data.
  * **Pre-Sign Asset Transaction:** Prepares to sign the asset transaction for further processing.

**Step 3:Data Request and Proof Validation**

* **ZK Apps:**
  * **Request Merkle Proof:** Applications request the Merkle proof to construct transactions sent to the L1 chain.
  * **Access Proofs:** The requested proofs are accessed for validation.
* **Objective Nodes (PoS):**
  * **Provide Merkle Proof Request:** Nodes process the request for Merkle proofs.
  * **Access Proof Data:** Data required for proof validation is accessed and prepared.
* **Fiamma Chain:**
  * **Begin Intersubjective Finality:** The process for final validation involving intersubjective nodes **begins.**

**Step 4: Intersubjective verification and hard Finality**

* **Intersubjective Nodes (User):**
  * **Verify ZKP:** Nodes verify the Zero-Knowledge Proof.
  * **If Valid (Happy Path):** If the proof is valid, the result is marked as TRUE.
  * **Collect Intersubjective Results:** The results from various nodes are collected to confirm the proof’s validity. if the number exceeds the threshold, the proof state will be updated to hard finality.

**Step 5: Happy Path**

* **Intersubjective Nodes (User):**
  * **Send Results if TRUE:** If the proof is valid, the results are sent as TRUE.
  * **Achieve Objective and Intersubjective Finality:** Both objective and intersubjective finality are achieved, confirming the proof’s validity.
* **Public Chains:**
  * **Process Transactions (Soft Finality):** Transactions are processed if the network trusts the soft finality of the proof.
* **Fiamma Chain:**
  * **State Updates:** The chain updates its state, confirming the successful verification of proofs.

**Step 6: Unhappy Path (Orange)**

* **Intersubjective Nodes (User):**
  * **If Invalid (Unhappy Path):** If the proof is invalid, the unhappy path is triggered.
  * **Read Commitments:** Nodes read the commitments to identify discrepancies.
  * **Send Disputed Sub-Script:** A disputed sub-script is sent for further verification.
* **Fiamma Chain:**
  * **Handle Dispute:** The chain processes the dispute, verifying the invalid proof.
  * **Initiate Slashing:** Penalizes the involved parties for submitting invalid proofs.
* **Babylon Chain:**
  * **Manage Penalties and Slashing:** Manages the penalties and slashing operations for invalid proofs.
* **Bitcoin Chain:**
  * **Record Commitments and Checkpoints:** Records the necessary commitments and checkpoints for validation.
* **Public Chains:**
  * **Process Transactions (Hard Finality):** Transactions are processed if the network trusts the hard finality of the proof.

**Step 7: Finalization and Penalties**

* **Fiamma Chain:**
  * **Ensure Finalization:** Ensures that all processes are finalized, managing stakes and penalties appropriately.
* **Bitcoin Chain:**
  * **Record Timestamps and Checkpoints:** Records final timestamps and checkpoints to validate the process.

\***Additional Details:**

* <mark style="color:orange;">**Unhappy Path Handling**</mark>**:** When an invalid proof is detected (Proof\_0), it follows the "Unhappy Path," triggering the Slash mechanism and involving steps like reading commitments, issuing challenge transactions, and validating through consensus.
* <mark style="color:green;">**Happy Path Processing**</mark>**:** Valid proofs follow the "Happy Path," ensuring smooth and efficient processing without triggering penalties.

**Here's a table comparing the Happy Path and Unhappy Path in Fiamma's ZKP handling:**

| **Aspect**                   | <mark style="color:orange;">**Unhappy Path**</mark>         | <mark style="color:green;">**Happy Path**</mark>                     |
| ---------------------------- | ----------------------------------------------------------- | -------------------------------------------------------------------- |
| **Definition**               | Error-handling workflow triggered by invalid proofs         | Standard, error-free workflow with valid proofs                      |
| **Proof Submission**         | Users submit zero-knowledge proofs to the Fiamma chain      | Users submit zero-knowledge proofs to the Fiamma chain               |
| **Proof Reception**          | Proofs are received and processed                           | Proofs are received and processed                                    |
| **Objective Finality**       | Invalid proof triggers error handling                       | Consensus is reached, and proof results are sent to the Fiamma chain |
| **Proof Validation**         | Invalid proof detected, challenge process is initiated      | Proofs are validated, multi-signatures are generated                 |
| **Data Request**             | Commitments are read to identify discrepancies              | Merkle proof is requested and accessed                               |
| **Intersubjective Finality** | Disputed sub-script is sent for verification                | Users verify proofs and confirm validity (results marked TRUE)       |
| **Consensus Process**        | Nodes handle disputes and initiate slashing                 | Nodes achieve both objective and intersubjective finality            |
| **State Updates**            | State update is paused for further verification             | State is updated with validated proofs                               |
| **Commitments Handling**     | Invalid commitments handled through dispute resolution      | Valid commitments sent to Bitcoin chain                              |
| **Penalty Mechanism**        | Slashing mechanism is triggered for invalid proofs          | Not applicable                                                       |
| **Transaction Processing**   | Transactions processed if hard finality is trusted          | Transactions processed if soft finality is trusted                   |
| **User Notification**        | Users are informed of invalid proof and penalties           | Users are informed of successful validation                          |
| **Finalization**             | Ensures disputes are resolved, and penalties managed        | Ensures all processes are finalized and recorded                     |
| **Efficiency**               | More complex with additional steps for error handling       | Smooth, efficient, and straightforward                               |
| **Outcome**                  | Invalid proofs lead to penalties and potential delays       | Valid proofs lead to state updates and rewards                       |
| **User Experience**          | More complex due to error handling and validation processes | Positive, with timely processing                                     |
