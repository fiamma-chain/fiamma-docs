# Architecture

The vision of **Fiamma Bridge** is to build the most secure bridge, enabling BTC users to thrive across every corner of the blockchain world. We aim to achieve this vision through a sufficiently decentralized design, as illustrated in the architecture diagram below.

<figure><img src="../../.gitbook/assets/whiteboard_exported_image (11).png" alt="" width="563"><figcaption><p>Bridge Architecture</p></figcaption></figure>

#### **Bitcoin Model**

1. **BTC Asset Management**
   * The user's BTC is transferred to a **multi-signature Taproot address**, where the signers are the user and the bridge committee.
2. **BitVM2 Transactions**
   * Pre-signed transactions that define how the user's BTC can be spent (e.g., for withdrawals or penalties).

#### **Destination chain Set (illustratory)**&#x20;

* **EVM-compatible chains**: Ethereum, BSC, Pharos, Base, Arbitrum, etc.
* **SVM (Solana Virtual Machine)**: Solana
* **Move VM chains**: Sui, Aptos, etc.
* **Wasm VM**: Babylon

#### **Challenger Group**

* A **permissionless** group responsible for detecting malicious operators.

#### **Committee Group**

* A **permissioned** group that secures the bridge during pre-signing phases. Its roles include:
  1. Participating in pre-signing BitVM2 transactions.
  2. Distributing rewards to challengers.

#### **Operator Group**

* Currently **permissioned**, but will transition to **permissionless** in the future.
* Facilitates user withdrawals from any sidechain.

#### **Fast Processor (FP) Group**

* Currently **permissioned**, but will become **permissionless** in the future.
* Handles withdrawal requests that cannot be processed directly by the Operator (e.g., partial withdrawals or complex cases).

#### **Front-end Model**

* **Website**: Users can access the Fiamma bridge via the web interface.
* **App**: Users can access the Fiamma bridge through the Fiamma mobile/desktop app.
