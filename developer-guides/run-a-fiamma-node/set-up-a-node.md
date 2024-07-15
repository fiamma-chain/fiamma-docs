---
description: In this tutorial you will learn how to set up a fiamma node
---

# Set up a Node

{% hint style="info" %}
NOTE

This guide requires having Fiamma installed on a Linux System. The instructions can be found on the Installation page The version to install is specified at the [fiamma-testnet-1 ](https://github.com/fiamma-chain/networks/tree/main/fiamma-testnet-1)network info page.
{% endhint %}

## System Requirements

The following specifications have been found to work well:

* Quad Core or larger AMD or Intel (amd64) CPU
* 32GB RAM;
* 1TB NVMe SSD Storage (disk i/o is crucial);
* 100Mbps bi-directional Internet connection;

## Install Fiammad <a href="#id-1-initialize-the-node-directory" id="id-1-initialize-the-node-directory"></a>

You can refer to the [installation page](../../user-guides/installation.md) to install the fiammad binary

## Initialize the Node Directory <a href="#id-1-initialize-the-node-directory" id="id-1-initialize-the-node-directory"></a>

First, initialize a node configuration directory under `~/.fiamma`. The `$NODENAME` variable specifies the name you aim to give your node.

```shell
fiammad init $NODENAME --chain-id fiamma-testnet-1
```

Then, retrieve the genesis file and place it in the node directory:

```bash
wget https://raw.githubusercontent.com/fiamma-chain/networks/main/fiamma-testnet-1/genesis.json -O ~/.fiamma/config/genesis.json
```

## Add Peers and Modify Configuration <a href="#id-2-add-peers-and-modify-configuration" id="id-2-add-peers-and-modify-configuration"></a>

Edit the configuration file at `~/.fiamma/config/config.toml` and modify the `seeds` and `persistent_peers` attributes to contain appropriate seeds and peers of your choice. The full list of Fiamma approved seeds and peers can be found under the [fiamma-testnet-1 ](https://github.com/fiamma-chain/networks/tree/main/fiamma-testnet-1)network info page.

```toml

# Comma separated list of seed nodes to connect to
seeds = "5d6828849a45cf027e035593d8790bc62aca9cef@18.182.20.173:26656,526d13f3ce3e0b56fa3ac26a48f231e559d4d60c@35.73.202.182:26656"

# Comma separated list of nodes to keep persistent connections to
persistent_peers = "5d6828849a45cf027e035593d8790bc62aca9cef@18.182.20.173:26656,526d13f3ce3e0b56fa3ac26a48f231e559d4d60c@35.73.202.182:26656"
```

Edit the configuration file at `~/.babylond/config/app.toml` and modify the `minimum-gas-prices` attribute and set it to a value of your choosing. For example

```toml
minimum-gas-prices = "0.00001ufia"
```

## Setup Cosmovisor <a href="#id-3-setup-cosmovisor" id="id-3-setup-cosmovisor"></a>

Cosmovisor is a tool for automating the management of Cosmos SDK application binary files. It simplifies the process of upgrading and rolling back chains.

To install the latest version of Cosmovisor

```bash
go install cosmossdk.io/tools/cosmovisor/cmd/cosmovisor@latest
```

Create the necessary directories

<pre class="language-bash"><code class="lang-bash"><strong>mkdir -p ~/.fiamma/cosmovisor
</strong>mkdir -p ~/.fiamma/cosmovisor/genesis/bin
mkdir -p ~/.fiamma/cosmovisor/upgrades
</code></pre>

Copy the `fiamma` binary into the `cosmovisor/genesis` folder

```bash
cp $GOPATH/bin/fiammad ~/.fiamma/cosmovisor/genesis/bin/fiammad
```

Setup a cosmovisor service:

```bash
sudo tee /etc/systemd/system/fiamma.service > /dev/null <<EOF
[Unit]
Description=Fiamma daemon
After=network-online.target

[Service]
User=$USER
ExecStart=$(which cosmovisor) run start --x-crisis-skip-assert-invariants
Restart=always
RestartSec=3
LimitNOFILE=infinity

Environment="DAEMON_NAME=fiammad"
Environment="DAEMON_HOME=${HOME}/.fiamma"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"

[Install]
WantedBy=multi-user.target
EOF
```

## Start the Node <a href="#id-4-start-the-node" id="id-4-start-the-node"></a>

```bash
sudo -S systemctl daemon-reload
sudo -S systemctl enable fiamma
sudo -S systemctl start fiamma
```

You can check the status of the node by running

```bash
systemctl status fiamma
```

You can also check the fiamma's log by running

```bash
journalctl -u fiamma -f
```
