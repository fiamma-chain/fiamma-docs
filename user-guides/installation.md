---
description: >-
  In this tutorial, you will learn about the dependencies that need to be
  installed to run Fiamma.
---

# Installation

### Step 1: Install Golang <a href="#step-1-install-golang" id="step-1-install-golang"></a>

{% hint style="info" %}
Fiamma requires Golang [version 1.22.3](https://go.dev/doc/install) for Fiamma to be installed on your system. Install it using the instructions on the provided link.
{% endhint %}

```
$ go version
go version go1.22.3 linux/amd64
```

### Step 2: Build and Install Fiamma <a href="#step-1-install-golang" id="step-1-install-golang"></a>

You need to clone Fiamma’s GitHub repository to install the `fiammad` executable.

1. Install build requirements

```
sudo apt-get install -y make git bash gcc curl jq pkg-config openssl libssl-dev
```

2. Retrieve the Fiamma source code either through the [releases page](https://github.com/fiamma-chain/fiamma/releases) or by cloning the [source code](https://github.com/fiamma-chain/fiamma).
3. Navigate to the directory that contains the Fiamma source code. From there build and install the fiammad executable

```
git checkout <version_to_install>
make install
```

{% hint style="info" %}
Note! he last command first executes `git checkout` in the specific version that you want to install. Ensure that you install the same version of the Fiamma executable as the one that is running on the network you aim to join.
{% endhint %}
