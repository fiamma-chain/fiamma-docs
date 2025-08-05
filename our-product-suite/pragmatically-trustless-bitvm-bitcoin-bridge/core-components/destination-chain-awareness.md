# Destination Chain Awareness

**It is crucial for Bitcoin to be aware of the state of other chains (e.g., Ethereum). However, due to Bitcoin’s limited programmability, constructing a light client for other chains directly on Bitcoin is impossible.**

Fortunately, we’ve discovered that **even without Bitcoin’s native programmability, a secure cross-chain protocol can still be implemented between Bitcoin and other alt-chains**. The key insight is: **if Bitcoin can reliably verify the state of alt-chains, we can integrate this mechanism into our bridge protocol.**

#### Atomic Swap protocol

Atomic Swap is a **trustless, decentralized cross-chain trading protocol** that enables users to exchange cryptocurrencies across different blockchains **without intermediaries**. It relies on cryptographic primitives like **Hashed Timelock Contracts (HTLCs)** to ensure atomicity—either the entire swap succeeds or nothing happens.

**Atomic swaps are easy for users to learn about, as they are a mature protocol widely used in many scenarios,** such as the [Lightning network](https://github.com/lightning/bolts) and [Binance](https://docs.bnbchain.org/).

We focus only on the **key element we can reference: the hashlock** (the other component is the timelock, but we won’t explore it here).

#### Hasklock

A **Hashlock** is a cryptographic construct that restricts access to funds until a predefined condition is met:

* A **secret preimage** (`s`) is hashed to produce a **commitment hash** (`H = hash(s)`).
* Funds are locked in a script/contract that enforces:
  * **Unlock condition**: The correct `s` must be revealed to match `H`.

#### **How to Achieve Cross-Chain Awareness?**

Cross-chain awareness depends on the **leakage of secret `s`**. Bob can obtain secret `s` on Bitcoin only if Alice claims the asset on the destination chain by revealing `s`. Based on this logic, we design the following mechanism:

> **"If the operator is slashed on the destination chain, they can also be slashed on Bitcoin (because any challenger can spend the disprove transaction)."**

This means that **when the operator is slashed on the destination chain, secret `s` must have been leaked**, allowing any challenger to use `s` to slash the operator on Bitcoin.

***

#### **Hashlock-Based BitVM2 Bridge Protocol**

The hashlock-based solution enables challengers to easily detect malicious behavior—such as an **invalid Bitcoin block** submitted in a claim. The process consists of two main phases:

**1. Pre-Sign Phase**

* All challengers generate their own secret value `s_i`.
* All challengers submit `H(s_i)` (the hash of `s_i`) to the bridge service.
* The bridge service aggregates these hashes into a **Merkle root** and constructs a **Taproot address**, which will be used on both the destination chain and Bitcoin.
* The user, operator, and committee pre-sign necessary transactions.

> **Note:** Submitting `s_i` is **permissionless**—any challenger can participate.

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (29).png" alt="" width="375"><figcaption></figcaption></figure>

1.  **Challenger Phase**

    1. **Challenge Initiation**
       * Challenger A raises a challenge.
    2. **Operator Response**
       * The operator submits the assert transaction to respond to the challenge.
    3. **Slashing Execution**
       * Challenger B (who may be different from Challenger A) slashes the operator on the destination chain by revealing secret `s_i`.
    4. **Disprove Transaction**
       * Any challenger can then submit the `disprove_2` transaction using `s_i`.

    > **Note:** The `disprove_2` transaction prevents a malicious operator from withdrawing BTC from the bridge.

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (30).png" alt="" width="375"><figcaption></figcaption></figure>

**If you want to understand how we prevent challengers from maliciously slashing the operator, please see the section:** [Permissionless slashable protocol](https://app.gitbook.com/o/pCAnNlKAzOo8rYFBd4MY/s/NaWxhWAPbrPeq8rIwJHB/~/changes/76/our-product-suite/pragmatically-trustless-bitvm-bitcoin-bridge/core-components/permissionless-slashable-protocol)
