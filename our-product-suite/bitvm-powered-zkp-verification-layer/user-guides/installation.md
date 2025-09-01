---
description: >-
  In this tutorial, you will learn about the dependencies that need to be
  installed to run Fiamma.
---

# Installation

### Step 1: Install Golang <a href="#step-1-install-golang" id="step-1-install-golang"></a>

{% hint style="info" %}
Fiamma requires Golang [version 1.23.3](https://go.dev/doc/install) for Fiamma to be installed on your system. Install it using the instructions on the provided link.
{% endhint %}

For Linux server installation of Go language, you can refer to the commands below, and for installation tutorials of Go language on other operating systems, you can refer to the official[ Go language documentation.](https://go.dev/doc/install)

```
wget https://golang.org/dl/go1.23.3.linux-amd64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.23.3.linux-amd64.tar.gz
echo 'export GOROOT=/usr/local/go' >> ~/.profile
echo 'export GOPATH=$HOME/go' >> ~/.profile
echo 'export GOBIN=$HOME/go/bin' >> ~/.profile
echo 'export PATH=$PATH:$GOROOT/bin:$GOBIN' >> ~/.profile
source ~/.profile
```

After executing the above commands, you should check that the version of go is the same as the required version.

<pre class="language-bash"><code class="lang-bash"><strong>$ go version
</strong>go version go1.22.3 linux/amd64
</code></pre>

### Step 2: Build and Install Fiamma <a href="#step-1-install-golang" id="step-1-install-golang"></a>

You need to clone Fiamma’s GitHub repository to install the `fiammad` executable.

1. Install build requirements

```bash
sudo apt-get install -y make git bash gcc curl jq pkg-config openssl libssl-dev
```

2. Retrieve the Fiamma source code either through the [releases page](https://github.com/fiamma-chain/fiamma/releases) or by cloning the [source code](https://github.com/fiamma-chain/fiamma).
3. Navigate to the directory that contains the Fiamma source code. From there build and install the fiammad executable

```bash
git checkout <version_to_install>
make install
```

4. Check fiammad command

```bash
$ fiammad version
```

{% hint style="info" %}
Note! the last command first executes `git checkout` in the specific version that you want to install. Ensure that you install the same version of the Fiamma executable as the one that is running on the network you aim to join.
{% endhint %}
