# Fiamma Operator

This guide explains the setup, operating and maintenance of Fiamma Operator for Linux on mainnet.

### **System Requirements**

* Linux Distribution: Ubuntu 20.04 LTS or later (recommended), CentOS 8+
* Architecture: x86\_64 (AMD64)
* CPU: 4+ cores (8+ recommended for production)
* RAM: 96GB minimum (96GB+ recommended)
* Storage: 100GB SSD minimum (500GB+ recommended)
* Network: Stable internet connection with low latency

***

### **Funds Tiers**

* Fiamma Operator uses a 6-tier system determined by an operator's total deposited funds.
  * Higher tiers support larger transaction amount and earn higher rewards.

| Tier    | Total Funds                      | Supported Txn Range           | Pegin Funds                                  | Pegout Funds                               | Staked Funds                                    |
| ------- | -------------------------------- | ----------------------------- | -------------------------------------------- | ------------------------------------------ | ----------------------------------------------- |
| Purpose | Total BTC needed for an operator | User deposit & withdraw range | Funds used for pre-sign deposit transactions | Funds used to prepay withdraw transactions | Security deposit to precent malicious behaviors |
| L0      | 1.5 BTC                          | 0.001 BTC                     | 0.15 BTC                                     | 1.1 BTC                                    | 0.1 BTC                                         |
| L1      | 2.5 BTC                          | 0.001 BTC \~ 0.01 BTC         | 0.15 BTC                                     | 2.11 BTC                                   | 0.1 BTC                                         |
| L2      | 3.5 BTC                          | 0.001 BTC \~ 0.05 BTC         | 0.15 BTC                                     | 3.112 BTC                                  | 0.1 BTC                                         |
| L3      | 5.5 BTC                          | 0.001 BTC \~ 0.2 BTC          | 0.15 BTC                                     | 5.113 BTC                                  | 0.1 BTC                                         |
| L4      | 10.5 BTC                         | 0.001 BTC \~ 1 BTC            | 0.15 BTC                                     | 10.1135 BTC                                | 0.1 BTC                                         |
| L5      | 15.5 BTC                         | 0.001 BTC \~ 3 BTC            | 0.15 BTC                                     | 15.1136 BTC                                | 0.1 BTC                                         |

***

### Tutorials

**See the tutorials below on running Fiamma Operator:**

1. [Install Operator](1.-install-operator/)
2. [Run Operator](2.-start-operator/)
3. [Maintenance](3.-maintenance/)
