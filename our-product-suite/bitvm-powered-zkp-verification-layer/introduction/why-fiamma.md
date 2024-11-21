# Challenges Tackled

**Centralization of Off-Chain State Verification**:

* Fiamma consists of both objective POS node module and intersubjective mobile node module.
* The discrepancy between the results of intersubjective and objective node modules would be settled by Bitcoin network via BitVM2.
* By this approach, Fiamma eliminates the reliance on a single sequencer, thus preventing a single point of failure and promoting a more democratic verification process.

**Latency in On-Chain State Verification**:

* Fiamma's design mitigates delays arising from proof aggregation and on-chain delay parameters. We will reduce the time required for each proof verification from hours to seconds.

**High Costs of On-Chain State Verification**:

* With high costs ranging significantly across different ZK proof algorithms (e.g., Groth at 250,000, Halo2-KZG at 400,000, and STARK-FRI at 1,500,000), Fiamma reduces these expenses by over 99%, making ZK proof verification more accessible.

**Limited Compatibility with ZK Verification Algorithms**:

* Fiamma is designed to be compatible with a variety of ZK proof algorithms, not just those that are Snark-friendly, thus accommodating a broader spectrum of blockchain applications.

**Non-Atomic Cross-Chain Operations**:

* Fiamma's infrastructure supports atomic transactions across different blockchains by receiving ZKPs from multiple chains. This ensures that operations are executed correctly and consistently on all involved chains, making Fiamma an excellent infrastructure for building cross-chain ZK bridges.

**High Threshold for Validator Nodes**:

* By lowering barriers to entry with intersubjective verifiers on mobile devices, Fiamma encourages more diverse and inclusive participation in the network's governance and operation.
