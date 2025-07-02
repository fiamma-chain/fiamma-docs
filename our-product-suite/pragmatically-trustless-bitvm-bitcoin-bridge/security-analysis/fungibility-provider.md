# Fungibility Provider

**The primary role of FP (Fungibility Provider) is to facilitate BTC redemptions that cannot be directly handled by Operators.**

Here's why:

* Operators can only process withdrawals within specific amount ranges.
* When a user's redemption request falls outside these limits, **FPs advance the BTC payment to the user immediately**.
* Later, when FPs accumulate enough small withdrawals to form a processable batch, **they reclaim the BTC through Operators**.

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (19).png" alt="" width="563"><figcaption></figcaption></figure>

After FPs advance BTC to users, they must redeem the BTC themselves. In this scenario, **FPs assume the same role as bridge users**, following identical trust assumptions during redemption. (Refer to the [_User_](https://app.gitbook.com/o/pCAnNlKAzOo8rYFBd4MY/s/NaWxhWAPbrPeq8rIwJHB/~/changes/71/our-product-suite/pragmatically-trustless-bitvm-bitcoin-bridge/security-analysis/users) section for details.)

**Note:** Users are required to pay an additional service fee to FPs for this convenience.
