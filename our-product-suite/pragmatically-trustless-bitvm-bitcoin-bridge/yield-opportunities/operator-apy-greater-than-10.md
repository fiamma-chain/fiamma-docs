# Operator (APY > 10%)

#### APR Formula

$$
APR = [\frac {(A + r*A * x)}{16} *\frac{365}{x+1}] * 100\%
$$

\
A: Represents the profit on the first day

r: The proportion of recyclable funds, with a value range of \[0,1]

x: Denotes number of days, with a range of \[1,364]

r\*A: represents the daily profit after the first day, assuming each subsequent day's earnings are r of the first day's

A + r\*A \* x: represents the total profit over x+1 days

\frac{365}{x+1}: represents the number of such profit cycles within 365 days&#x20;

16: denotes 16 sBTC in principal

#### How to calculate A

1. Revenue
   1. Deposit Revenue
      1. Fee rate> 8: 660 sats per Deposit transaction
      2. Fee rate < 8: 330 sats per Deposit transaction
   2. Withdrawal Revenue:
      1. 0.15% of advanced payment amount
      2. 1000 × Feerate: Real-time Bitcoin network fee rate
2. Expenditure
   1. Fund Recovery Cost
      1. Maximum Claim+Happy Take transaction size:
         1. 586 vbytes + 420 vbytes = 1006 × Feerate
      2. Minimum Claim+Happy Take transaction size:
         1. 300 vbytes + 420 vbytes = 720 × Feerate

\
Define:

a The number of deposit transactions

b The number of withdrawal transactions

v The volume of withdrawal requests

f\_p The average feerate of withdrawal requests

f\_{ch} The average fee cost of claim transaction and happy take transaction\
Then, we calculate&#x20;

$$
A = (660 * a + b * 1000 * f_p + v * 0.0015) - b*f_{ch}
$$

#### Why do yields (A) decrease in subsequent days?

On Day 1, the Operator's principal remains 100% available, resulting in the highest yield rate on this initial day. From Day 2 onward, only redeemed funds become recyclable for reuse. We assume an average daily capital recovery rate of 10%, which is then redeployed (note: compound interest effects are excluded from this calculation due to multiple yield-impacting factors, hence APY computation is not considered here).

<figure><img src="../../../.gitbook/assets/whiteboard_exported_image (31).png" alt="" width="563"><figcaption></figcaption></figure>

The 10% figure is a hypothetical value, with the actual ratio being influenced by multiple factors:

1. Bitcoin Network Congestion
   1. High congestion may reduce the Operator's capital recovery rate to near 0%
   2. Under low-congestion conditions, 100% recovery becomes achievable
2. Fee Rates of Claim & Happy Take Transactions
   1. If the Operator's preset fee rate (determined during the deposit phase and immutable) falls below current network rates:&#x20;
      1. &#x20;Recovery requires waiting until network fees drop to the preset level
3. User-Specified Fee Rates
   1. Operators typically select recovery fee rates ≤ users' specified rates to avoid losses
   2. When user-specified rates are significantly below current network fees:&#x20;
      1. Recovery timelines extend proportionally

#### APR Trend Chart

Since the Operator cannot initiate the next round of services only after 100% of the funds have been recovered, a dynamic fund recovery process is a more reasonable method for calculating the Operator's APR. We selected several different sets of values to demonstrate the changing trend of the Operator's APR.

**A = 0.2， r = 0.1 and r = 0.05**

The yellow line represents a daily recovery rate of r = 0.05, corresponding to an ultimate annualized yield of APR = 24%. The green line represents a daily recovery rate of r = 0.1, corresponding to an ultimate annualized yield of APR = 46.75%.

<figure><img src="https://rg8wvc8zvxs.sg.larksuite.com/space/api/box/stream/download/asynccode/?code=ZTdhMzI1NjUwZDA3YWRmMDUyNGI5YTcyYmFiZmE5N2JfM0s4SzlvUTdYcFN6TWZPNzl5WkJEZUVUdVIyWTBXQmZfVG9rZW46VGRVdmJoSDgxb1VvUmN4a0JIZmxRS0s4Z21jXzE3NTE4OTgyMTQ6MTc1MTkwMTgxNF9WNA" alt="" width="563"><figcaption></figcaption></figure>

**A = 0.2, r = 0 and r = 1**

We present the APR yields under two extreme scenarios, which determine the upper and lower bounds of the Operator's APR. The yellow line represents a daily recovery rate of r = 0, corresponding to an ultimate annualized yield of APR = 1.25%. The grey line represents a daily recovery rate of r = 1, corresponding to an ultimate annualized yield of APR = 456.25%.

<figure><img src="https://rg8wvc8zvxs.sg.larksuite.com/space/api/box/stream/download/asynccode/?code=YmY3YzEyYTVhY2E1NzA5MDczMmJkMzQ1ZGNmZWNlMDRfREszMDVSQVNwd0tYWm9Oc3JUd2dYbXFiMnBRNlY5U3BfVG9rZW46UzB3M2JTU0w0b3d4eXh4WmlEMGx3aTJ6Z3FmXzE3NTE4OTgyMTQ6MTc1MTkwMTgxNF9WNA" alt="" width="563"><figcaption></figcaption></figure>

**APR > 5%, r = ？**

Considering that most real-world BTC annual yields are below 5%, we calculate the required recovery rate r for which APR > 5%.

<figure><img src="https://rg8wvc8zvxs.sg.larksuite.com/space/api/box/stream/download/asynccode/?code=YTA1MTRjZjM3NDE4NjNjY2M4MjY5YjJlMGIzZTM2NWNfYkFkZ09XaDY0QlVVYmtZbHlRbWxOOUR4MGZEZG1PUTdfVG9rZW46S3I4NmI1NTU1b1RKSjR4dU9ac2xtMEs1Z3B6XzE3NTE4OTgyMTQ6MTc1MTkwMTgxNF9WNA" alt=""><figcaption></figcaption></figure>

According to calculations, when A = 0.2 and r = 0.009, the Operator's APR = 5.345%. This requirement is highly achievable in practice. With an initial principal of 15 BTC, a daily refund of just 0.135 BTC (15×0.009) from Day 2 onward would suffice to maintain an APR above 5%.
