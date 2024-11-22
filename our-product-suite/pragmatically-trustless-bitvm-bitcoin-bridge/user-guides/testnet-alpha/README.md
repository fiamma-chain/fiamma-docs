# Testnet Alpha

## Function and Limitation

### Function

1. Support Ethereum Holesky Testnet
2. Support **ANY** `PEG-IN` amount.
3. Support Fungible `PEG-OUT`.
   1. User can transfer `mamaBTC`  to anyone.
   2. User can `PEG-OUT` varying amounts of `mamaBTC` to Bitcoin.

### Limitation

1.  Limited `PEG-OUT`amount: `0.00001sBTC to 0.0001sBTC`



    This limitation applies only to the Testnet, as the Operator must pre-fund users with her own`sBTC.`We can remove this restriction once we acquire more sBTC from liquidity providers or market makers.
2.  The `PEG-OUT` amount cannot be arbitrary.



    Currently, users can only `PEG-OUT` amounts that are included in the valid PEG-IN amount list.

## What's Next?

1. Users can `PEG-OUT` any `mamaBTC` amount in a specified range.
2. After integrating ZK light clients into the bridge, we can enable anyone to become an operator.
3. We aim to enable Bitcoin to bridge seamlessly to a wider range of blockchains.



