# Trustless Bridge

We want a bridge to be trustless and permissionless, ensuring the protocol's safety.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Fig6. Trustless Bridge on Bitcoin</p></figcaption></figure>

Transaction analysis
1. PEG-IN transaction: Alice PEG-IN 10 BTC on Bitcoin, the owner of output UTXO is Alice and The Committee;
2. PEG-OUT transaction: Alice PEG-OUT 10 BTC from the sidechain, it generates 2 connector outputs
3. Take-1 transaction: it's a happy path. Alice could take 10 BTC back if there was no one to issue the Challenge transaction in 7 days;
4. Take-2 transaction: Alice could take 10 BTC back if there was no one to issue the Dispute transaction in 1 day
5. Challenge transaction: Anyone could pay 1 BTC to issue this transaction, then the Take-1 transaction will not be spent as the input was spent by another transaction
6. Assert transaction: Alice broadcasts the Assert transaction, it generates 2 outputs
7. Dispute transaction: Anyone could issue this transaction to slash Alice . If Alice is malicious, then the Take-2 transaction will not be spent as the input was spent by another transaction
8. Timeout transaction: If Alice does not broadcast the Assert transaction in 3 days, he will be slashed
Overall flow
1. Alice PEG-IN 10 BTC by issuing the PEG-IN transaction;
2. Alice pre-signed 6 transactions with the Committee. These transactions decide the way that the output of PEG-IN could be spent. We could name it as the PEG-IN contract and the PEG-OUT contract
3. After a long time, Alice wants to PEG-OUT 10 BTC by issuing the PEG-OUT transaction. He must provide evidence that he burned 10 Wrapped-BTC on the sidechain.
4. There will be a 7-day challenge period for Alice to execute the Take-1 transaction. Anyone could issue the Challenge transaction to stop Alice from executing the Take-1 transaction
5. If the challenger issues the Challenge transaction by paying 1 BTC, then the challenge begins
6. Alice has to broadcast the Assert transaction in 3 days because he will be slashed by kicking off the Timeout transaction by the Committee if Alice doesn't respond to the challenge
7. Anyone could issue the Dispute transaction to slash Alice and get rewards if Alice really gives a wrong claim
8. If there is no one to issue the Dispute transaction in 1 day, Alice executes the Take-2 transaction to take 10 BTC back and the challenger loses his 1 BTC 
Key points clarification
1. Remove the 1st trust source: at least 1 Honest Committee member(mark 1)
The output UTXO is controlled by Alice and Committee, so Alice doesn't need to trust the Committee
2. Remove the 2nd trust source-2: at least 1 honest Operator(mark 2 & 3)
The output owner of the Take transaction is A directly instead of the Operator, so we don't need to introduce the Operator role in the new protocol
3. Keep the whole protocol fully slashable(marks 4 & 5 & √ & ×)
  1. As used in Babylon, we set the PEG-IN contract and PEG-OUT contract at the initial phase
  2. These transactions could ensure that:
    1. When Alice is honest, he can PEG-OUT successfully
    2. When Alice is dishonest, he must be slashed;
    3. When Challenge is dishonest, he must lose his challenge cost and Alice can PEG-OUT successfully