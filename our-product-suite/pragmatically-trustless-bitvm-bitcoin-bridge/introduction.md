# Introduction

## Let's Make BTC Greater Than Ever

### What is the Fiamma Bridge?

The **Fiamma Bridge** is a revolutionary new solution for cross-chain BTC asset transfer. Unlike traditional multisig bridges, the BitVM2 Bridge achieves:

1. **BTC Safety**: Your BTC remains secure—no one can transfer your locked BTC without your signature.
2. **PEG-IN Safety**: Users can mint the exact amount of mamaBTC (tokenized BTC minted via Fiamma Bridge) on the sidechain.
3. **PEG-OUT Safety**: Users can withdraw safely from the sidechain at any time, converting mamaBTC into equivalent BTC.
4. **Exactly Pegged Value**: mamaBTC on the sidechain is always backed 1:1 by BTC on Bitcoin, ensuring that mamaBTC : BTC = 1:1.

The BitVM2 Bridge minimizes trust assumptions. When bridging BTC to a sidechain, users no longer have to worry about the security of their locked BTC. Similarly, withdrawing BTC from the sidechain no longer depends on multisig holders' signatures.

### How Do We Secure Locked BTC?

Traditional solution: The Committee controls your BTC, so they **can** spend it without your signature.

Innovative solution: The user and the Committee control the user's BTC together. Therefore, they **can't** spend it without the user's signature.

<figure><img src="../../.gitbook/assets/whiteboard_exported_image (9) (1).png" alt=""><figcaption></figcaption></figure>

But, when you want to take your BTC back, you need to trust the Committee as well. How do we solve this problem? **To emulate the OP\_CTV opcode, the user and the bridge committee will pre-sign a few transactions to specify how these BTC could be spent in the future. This feature is enabled by BITVM2.**

### High-Level Summary of PEG-IN and PEG-OUT Processes

#### **PEG-IN: Moving BTC to the Sidechain**

1. Users lock BTC in a multisig address shared with the Bridge Covenant Committee (BCC), ensuring control.
2. Pre-signed rules dictate how locked BTC can be spent.
3. Relayer synchronizes Bitcoin block data to the sidechain.
4. Minter verifies the transaction and mints an equivalent amount of mamaBTC on the sidechain for the user.

**Key Security Point**: BTC remains under shared custody, and only valid transactions are minted, verified through Bitcoin's consensus and light client validation.

#### **PEG-OUT: Moving mamaBTC Back to Bitcoin**

1. Users burn mamaBTC on the sidechain to initiate a withdrawal.
2. The operator validates the burn and pre-pays the equivalent BTC to the user.
3. A kick-off transaction allows the operator to reclaim the locked BTC after a challenge period.
4. Honest operators receive their BTC back; malicious operators are penalized, and challengers are rewarded.

**Key Security Point**: Bitcoin itself acts as the final validator, ensuring only valid withdrawals occur, with dispute resolution mechanisms protecting against malicious actions. We only require one honest challenger to initiate a challenge, making the trust assumptions nearly trustless. With significant rewards at stake and a straightforward, permissionless challenge process, rational actors are strongly incentivized to participate.

**Bitcoin's dispute resolution capabilities are fundamentally enabled by our implementation of** [**fragmented ZK verifier**](https://x.com/Fiamma\_Chain/status/1830824142826086608) **in Bitcoin Script in July 2024, an indispensable and defining module of the BitVM bridge.**

In the next section, we will explain how to ensure the validity of the Bitcoin block containing the operator's peg-out transaction—an essential and complex task in building the first pragmatically trustless Bitcoin bridge.
