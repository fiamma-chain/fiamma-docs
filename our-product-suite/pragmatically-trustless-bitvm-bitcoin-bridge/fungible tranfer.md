---
description: >-
  It's an important module in BitVM2-based trustless bridge design. In this section, we will describe how to support fungible tranfer.

  It should be noted that design still being optimized, so the content maybe change in the future.
---

# Overall flow

<figure><img src="../../.gitbook/assets/fungible_1.png" alt=""><figcaption></figcaption></figure>

There are 4 scenarios that we have to consider:
1. Normal case:  Mike could PEG-OUT successfully with 10 BTC
2. Abnormal case 1: The amount that Jane wants to PEG-OUT exceeds the maximum value (102 BTC > 100 BTC)
3. Abnormal case 2: The amount that Bob wants to PEG-OUT doesn't exist currently (0.5 BTC does not exist)
4. Abnormal case 3: Some wrapped BTC were transferred to the Burn address (0.5 BTC in the Burn address)

Then how can we solve these problems?

# Abnormal case 1

This case could be easily solved. We set up the maximum limitation for the PEG-IN process. But maybe one user on the sidechain might get more wrapped BTC and then plan to PEG-OUT.
So, for this case, the user has to PEG-OUT all the wrapped BTC with a few separate transactions.

<figure><img src="../../.gitbook/assets/fungible_2.png" alt=""><figcaption></figcaption></figure>

However, we will provide an additional approach (liquidity provider) to improve the user experience. 

<figure><img src="../../.gitbook/assets/fungible_3.png" alt=""><figcaption></figcaption></figure>
So, in this approach, the user could directly peg-out with the help of LP (liquidity provider). The LP should get more fees and the users should pay it.

# Abnormal case 2

Ideally, we hope that the amount distribution between bitcoin and sidechain should be like this:

<figure><img src="../../.gitbook/assets/fungible_4.png" alt=""><figcaption></figcaption></figure>

In this scenario, everyone could PEG-OUT smoothly. But in the real case, most of the amount is not the same

<figure><img src="../../.gitbook/assets/fungible_5.png" alt=""><figcaption></figcaption></figure>

To solve this problem, we use a few ways:
1. Support a wider range of amount types;
2. Introduce the roles of liquidity providers-- they could get some tokens and additional fees as rewards;

<figure><img src="../../.gitbook/assets/fungible_6.png" alt=""><figcaption></figcaption></figure>

There is a little difference between Abnormal Case 2 and Abnormal Case 1.
In Abnormal Case 2: the user does not need to pay additional fees for the LP
In Abnormal Case 1: the user does need to pay additional fees for the LP

Now, the overall flow should be like in the following picture:
<figure><img src="../../.gitbook/assets/fungible_7.png" alt=""><figcaption></figcaption></figure>

#  Abnormal case 3

If there is some wrapped BTC transferred to a burn (black hole) address by accident. This means that there will be some BTC locked in Bridge. 

The good thing is that the LPs can also help users take BTC back only if they can provide proof to prove that they really transferred some wrapped BTC to this address.

<figure><img src="../../.gitbook/assets/fungible_8.png" alt=""><figcaption></figcaption></figure>

In this case, we have to ensure the burn address is a black hole address, like the 0x00...000 address.

# Forced exit module with fungible case

In the normal case, the receiver (operator) is deterministic at the pre-signed phase and each operator will maintain a transaction list (all transactions that the receiver is himself) to know how much BTC he can take.

For example: 
Operator A could take 100 BTC
Operator B could take 50 BTC

It means there are 150 wrapped BTC in the sidechain total, but now operator A is offline.
So for operator B, it could only pay 50BTC. For other users, they can not PEG-OUT successfully unless Operator A is online again.

To solve this problem, we introduce the forced exit module for users. The general idea is the user will pre-sign a few additional transactions with the bridge committee but not specify the receiver (SIGHHASH_NONE). But the condition is, that the user has to provide a valid proof for the burn transaction, otherwise, he cannot take the BTC back

<figure><img src="../../.gitbook/assets/fungible_9.png" width = "400" div align=center/><figcaption></figcaption></figure>

A more radical approach:

In the normal case, the receiver (operator) is non-deterministic at the pre-signed phase and all operators share a common BTC pool they can take.

For example: 
Operator A could take 100 BTC
Operator B could take the same 100 BTC as well

So the advantage is that only one operator is honest. All users could peg out smoothly

But let's assume all operators are offline, we should support forced exit module as well.

<figure><img src="../../.gitbook/assets/fungible_10.png" alt=""><figcaption></figcaption></figure>