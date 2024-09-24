# Proof Journey in Fiamma

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Fig6. ZKIndexer on Bitcoin with Fiamma</p></figcaption></figure>

For the Happy Path, it includes 5 steps:
1. The customers of Fiamma send their zk proofs to the Fiamma chain;
2. The Block proposer in the Fiamma chain will verify these proofs first and package them into one block, then broadcast it;
3. The proof will achieve Soft finality when the consensus is finished;
4. The monitor user nodes start to read the proof and consensus result on the Fiamma chain. Then they will execute the verification process locally. If the result is the same, they will submit the confirmation result. Otherwise, they will kick off the unhappy path.
5. When the proof gets enough confirmation, the state transits to Hard finality

You can see that there is nothing relevant to the Bitcoin network. However, the Bitcoin network will be involved in the unhappy path. This is a core point in the Fraud proof module.

So for the unhappy path, there are 7 steps: 
1. The customers of Fiamma send their proofs to the Fiamma chain;
2. The Block proposer in the Fiamma chain will verify these proofs first and then pack them into one block, but please note that, the Block proposer plans to be malicious now, so he gives the wrong result.
3. The state of proof is soft finality now
4. The monitor user nodes start to read the proof and consensus result on the Fiamma chain. 
5. The user nodes can easily find that the result is incorrect, so one of them will kick off the challenge transaction as he or she will get rewards for it.
6. The Block proposer has to broadcast the Assert transaction because if he doesn't respond to it, she will be slashed directly
7. Anyone could kick off the Disputed transaction to slash the Block Proposer