# ZKRollup on Bitcoin

  Fiamma enables real ZK-rollups secured by the Bitcoin network.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Fig6. ZKRollup on Bitcoin with Fiamma</p></figcaption></figure>

  ZK-Rollup without Fiamma: centralized verification, barely secured by Bitcoin network. 
  1. User submits transaction;
  2. The sequencer generates block and execution traces which can be used to generate zk proof;
  3. The prover generates zk proof and then sends it to the sequencer;
  4. The sequencer sends the proofs to the local ZKP verification group;
  5. The local ZKP verification network verifies it and signs the result;
  6. The Sequencer sends synchronization transactions to the Bitcoin network;
  7. This transaction checks the signatures and verification result == OP_TRUE, and stores the new root with OP_RETURN;
  The problem is that if the sequencer generates fake proof but the ZKP verification group gives a TRUE result, then it can be detected neither on-chain (Bitcoin) nor off-chain as no one except the centralized sequencer has the results. Even if the ZKP verification group publishes the result, there are still 3 problems:
  1. Users prefer reading results from a transparent and decentralized chain rather than those provided by a trusted party;
  2. If there is any dispute, it can't be resolved in a trustless manner (e.g., settled by the Bitcoin network)
  3. Because the dispute can't be solved on Bitcoin, it's not slashable;
  
  ZK-Rollup with Fiamma: decentralized verification, secured by Bitcoin network via BitVM2 and Babylon.
  1. User submits transaction;
  2. The sequencer generates block and execution traces which can be used to generate zk proof;
  3. The prover generates zk proof and then sends it to the sequencer;
  4. The sequencer sends the proof to the Fiamma chain;
  5. The Fiamma chain verifies proof and provides a signature for the verification result;
  6. The Sequencer sends synchronization transactions to the Bitcoin network;
  7. This transaction checks the signatures and verification result == OP_TRUE, and stores the new root with OP_RETURN;
  This could solve the problems we proposed before:
  1. Users can read the result Fiamma chain, it's transparent;
  2. If the dispute happens, it can be solved on the Bitcoin network directly;
  3. The assets staked could be slashed directly;