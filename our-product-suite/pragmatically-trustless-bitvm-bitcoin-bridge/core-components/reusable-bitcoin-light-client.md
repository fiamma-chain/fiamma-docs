# Reusable Bitcoin Light Client

Each mint request in the minting process must verify the validity of the deposit transaction by querying the Bitcoin Light Client (LC) on the destination chain. Similarly, the withdrawal process requires the Bitcoin LC to validate whether the PegOut transaction is confirmed on the Bitcoin blockchain.

Several other projects attempt to implement an off-chain (optimistic) Bitcoin LC, which operates locally with a permissioned challenger set (since constructing a native Bitcoin LC directly on Bitcoin is impossible). In contrast, our approach reuses the alt-chain Bitcoin LC deployed on the destination chain, which features a permissionless challenger set.

This means the minting and withdrawal processes share the same Bitcoin LC, hence we call it the **Reusable Bitcoin LC**.

The Reusable Bitcoin Light Client offers three key advantages:

1. It maintains the security of the bridge protocol without compromise.
2. The entire protocol remains permissionless, including operators and challengers.
3. It enables fast and low-cost validation of Bitcoin blocks (\~15 seconds on Ethereum at a cost of < 1 USD).

In comparison, optimistic Bitcoin LC solutions face impractical challenges—such as generating recursive ZK proofs for the entire Bitcoin chain, which would take weeks (even with ZK-STARKs) and exceed the typical two-week challenge window, making them unsuitable for production.

Regardless of the Bitcoin LC implementation, the ultimate goal is for Bitcoin itself to recognize the validity of its blocks. For further details, refer to the **"**[**Destination Chain Awareness**](https://app.gitbook.com/o/pCAnNlKAzOo8rYFBd4MY/s/NaWxhWAPbrPeq8rIwJHB/~/changes/76/our-product-suite/pragmatically-trustless-bitvm-bitcoin-bridge/core-components/destination-chain-awareness)**"** section.

