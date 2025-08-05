# Permissionless Mint

Trustless Mint implies that users can obtain wrapped BTC (FiaBTC) without requiring trust in any intermediary. In our bridge design, we ensure that:

1. FiaBTC cannot be over-minted: fiaBTC can only be minted through a valid deposit transaction in the Fiamma Bridge, which requires:
   * Verification of the deposit transaction format
   * Validation of the deposit transaction by the Bitcoin light client (LC) on the destination chain
2. Users can obtain FiaBTC through two methods:
   * Via the official minter: The official minter can submit the mint request on behalf of users, with users covering the gas fees
   * Direct minting: If users don't trust the official minter or if the minter fails to process the request within a specified timeframe, users can call the mint function directly by providing valid transaction data

Approach 1 offers a better user experience (one-click minting) but requires the official minter to be operational (liveness assumption), while Approach 2 provides a trustless fallback option.

We will initially launch Approach 1 and implement Approach 2 in a subsequent upgrade.

