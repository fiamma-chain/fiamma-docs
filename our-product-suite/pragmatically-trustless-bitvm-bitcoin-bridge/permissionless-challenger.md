# Permissionless Challenger

The Fiamma Bridge operates under a fundamental trust assumption: **at least 1 out of N challengers must be honest**. This means the larger the value of **N**, the more secure the bridge becomes.

Although the challenger role is permissionless, we strive to minimize barriers to entry to encourage broad participation. By ensuring a large and diverse pool of challengers (**N**), we enhance the bridge’s security, making Fiamma the safest Bitcoin bridge.

To achieve this, we’ve designed the permissionless challenger system with three key principles:

**1. Accessibility**

* **Easy to Run**: We provide a user-friendly challenger frontend for seamless operation. For details, refer to the [Challenger Guide](user-guides/testnet-beta/how-to-run-a-challenger.md).
* **Low Capital Requirements**:
  * **Collateral**: Only **0.0001 sBTC** (current testnet requirement).
  * **Challenge Cost**: At most **0.001 sBTC** per challenge.

**2. Incentives**

* **Regular Rewards**: Challengers earn rewards for verifying each proof submitted by operators.
* **High Stakes Rewards**: If a challenger successfully identifies and slashes a malicious operator, they can earn up to **1 sBTC**.

By combining low entry barriers with strong incentives, we foster a robust and decentralized challenger network, ensuring the highest level of security for users.

