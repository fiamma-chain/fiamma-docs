# Cross-chain Interoperability

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Fig6. Cross-chain Interoperability with Fiamma</p></figcaption></figure>

Note: Nexus and Fiamma chains integrate these chains concurrently.
1. Alice sends a request (intent) to the NEXUS entrypoint contract, records this message, and marks it as pending state;
2. The decentralized operators read the message and decide whether to accept this deal;
3. If the operator accepts this deal, the message will be marked as under progress, and generate a unique deal_id;
4. Then Alice transfers the assert to an address:
  1. For a programmable chain , it's a contract address;
  2. For a non-programmable chain, it's a taproot address and pre-sign a tx, the operator could spend this tx if he can provide a valid Fiamma signature otherwise Alice will take the asset back after a TIMELOCK;
5. Fiamma receives ZK proofs from these chains. If the chain is not the ZK chain, the Operator will generate the tx inclusion proof and then send it to Fiamma;
6. Fiamma finishes the verification function and sends data to Avail, including proof, input, and signature.
7. The operator requests the verification by using the deal_id;
8. Operator kick-off TAKE transaction to make money
  1. For a programmable chain, check the signature and execute the transfer function;
  2. For a non-programmable chain, spend taproot address

