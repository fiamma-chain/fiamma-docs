---
description: >-
  We are developing essential use cases built on our ZKP verification layer and
  leveraging BitVM2 to support and expand the growing Bitcoin ecosystem.
---

# Other Essential Protocols

These essential protocols include but not limited to ZK-indexers, liquidity cross-chain ZK bridge, bridgeless interoperability with Bitcoin L1, etc. \
\
Please see some high-level architecture of ZK-indexers and trust-minimized ZK bridge below.&#x20;

## **ZK-Indexer (BRC20)**

The [main problem](https://foresightnews.pro/article/detail/48043) with the BRC-20 Indexer is its centralized and isolated setup, requiring users to trust an off-chain indexer. Fiamma can enable a trustless, decentralized, and unified indexer, facilitating the growth of the BRC-20 market.

<figure><img src="../.gitbook/assets/whiteboard_exported_image (14) (1).png" alt=""><figcaption></figcaption></figure>

### &#x20;**Current solutions without Fiamma:**

1. Centralized indexer - the value of the BRC-20 token is secured by a centralized off-line indexer, subject to manipulation;
2. Separated ledger - different projects may operate different indexers, causing a wrong token value;

### **Solution-1 with Fiamma (ZKIndexer):**

1. Secured by Bitcoin - By integrating the Fiamma, the value of the BRC-20 token is secured by Bitcoin via Babylon and BitVM2;
2. Separated ledger - different projects may operate different indexers, causing token loss;
3. Unified ledger - the same ledger, the same value;

### **Solution-2 with Fiamma (ZKIndexer chain):**

1. Secured by Bitcoin - By integrating the Fiamma, the value of the BRC-20 token is secured by Bitcoin via Babylon and BitVM2;
2. Unified ledger - the same ledger, the same value;

## **Trust-minimized ZK-Bridge**

We want this ZK-Bridge to be trust-minimized, ensuring the protocol's safety as long as at least one committee member is honest.

<figure><img src="../.gitbook/assets/whiteboard_exported_image (16) (1).png" alt=""><figcaption></figcaption></figure>

The overall flow:

1. Alice peg-in 100BTC a few months ago and now she wants to peg-out to Bob;
2. The operator delegate pays 99 BTC (assuming charging transaction fee of 1 BTC) by kicking off the peg-out transaction;
3. When the peg-out transaction is finalized on Bitcoin, the operator generates proof for it;
4. The operator sends proof to Fiamma and then Fiamma returns the result;
5. The operator broadcasts the Fiamma ASSERT transaction and allocates 5 BTC as staking asset;
6. Anyone could spend the output of Fiamma ASSERT (5 BTC) if he or she could prove the operator is malicious;
7. After a fixed timelock, if the output isn't spent, the operator kicks off the TAKE transaction to get 105 BTC;

