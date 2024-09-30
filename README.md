Swisstronik
---

# Swisstronik Installation Guide

This guide explains how to install `swisstronikd` from a `.deb` package. It is suitable for **Ubuntu 20.04** and newer versions. If you're using a different Linux distribution, please refer to the [Build from Sources](#) page.

## Prerequisites

Before installing and running `swisstronikd`, ensure you have the correct hardware and that **SGX** is properly configured. For more information, refer to the [Setup SGX](#) section.

## Install Go (v1.21.4+)

The following commands will install Go v1.21.4 and cleanly remove any previous Go installations:

```bash
sudo rm -rvf /usr/local/go/
wget https://go.dev/dl/go1.21.4.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.21.4.linux-amd64.tar.gz
rm go1.21.4.linux-amd64.tar.gz
```

### Configure Go

Add the following lines to your `~/.profile` file to configure Go:

```bash
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```

## Install Cosmovisor

Install Cosmovisor v1.0.0 by running the command below:

```bash
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

## Install Swisstronik Binary

To install the `swisstronikd` binary without building from sources, download and install the `.deb` package.

1. Download the `.deb` package from the [GitHub Releases](https://github.com/SigmaGmbH/swisstronik-chain/releases/tag/v1.0.1), or use the command:

    ```bash
    wget https://github.com/SigmaGmbH/swisstronik-chain/releases/download/testnet-v1.0.2/swisstronik_1.0.2_amd64.deb.zip
    ```

2. Extract the `.deb` package:

    ```bash
    unzip swisstronikd_v1.0.2.deb.zip
    ```

3. Install the `.deb` package using `dpkg`:

    ```bash
    sudo dpkg -i swisstronikd_v1.0.2.deb
    ```

4. Verify the installation:

    ```bash
    swisstronikd version
    ```

   The output should display the current version of the binary, for example, `v1.0.2`. If necessary, rename the binary:

   ```bash
   mv /usr/bin/swisstronikd_v1.0.2 /usr/bin/swisstronikd
   ```

## Troubleshooting

If you encounter the error `Enclave failure: SGX_ERROR_ENCLAVE_FILE_ACCESS`, ensure the `enclave.signed.so` file is in the correct location:

```bash
cp /usr/lib/enclave.signed.so /root/.swisstronik-enclave/enclave.signed.so
```

Alternatively, specify the `ENCLAVE_HOME` environment variable:

```bash
export ENCLAVE_HOME=/path/to/enclave
```
