# fermi-1 (testnet)

## Meta

Chain-ID: `fermi-1`

Chain-Repo: [`github.com/NillionNetwork/nilchain`](http://github.com/NillionNetwork/nilchain)

Networks-Repo: [`github.com/NillionNetwork/networks`](https://github.com/NillionNetwork/networks)

Tag: `0.1.1`

Denom: `nil/unil`

Gentx Folder: `github.com/NillionNetwork/networks/fermi-1/gentx`

## **Prerequisites**

- Go 1.21+
- make and gcc

```bash
git clone git@github.com:NillionNetwork/nilchain.git
cd nilchain
# git checkout tags/0.1.1
make install
```

## **Create account**

Needed for pre-genesis

```go
nilchaind keys add <account_name>
```

> 💡 if you already have a key you would like to use, use the `—recover` flag to recover the key and get the `nilliond` `bech32` encoded version.

We need:

- `address`
- `pubkey`

_After you have provided an account address please wait for a pre-genesis link to conduct your gentxs._

## **Pre-genesis**

Download the pre-genesis file:

```bash
wget <url-to-pre-genesis.json> -O nilchaind/config/genesis.json
```

## **Submit gentx**

It is run on the computer that hosts the cold validator operator app key, using the keyring of your choice. Collect the consensus public key from CometBFT KMS.

```go
nilchaind genesis gentx <account_name> 1000000unil --chain-id=fermi-1 --moniker=<your moniker> --details=<your desc> --commission-rate=0.05 --commission-max-rate=0.2 --commission-max-change-rate=0.02 --pubkey=$(nilchaind tendermint show-validator) --identity=<your ident> --security-contact <your-email> --keyring-backend os
```

This creates a JSON file on the validator's computer, typically in `~/.nillionapp/config/gentx/`

Create a PR with your JSON to the [Nillion networks repo](https://github.com/NillionNetwork/networks) with your gentx in this folder `fermi-1/gentx`

## Testnet launch

### **Download final genesis**

```
wget <url-to-genesis.json> -O nilchaind/config/genesis.json
```

### **Submit node details**

```
nilchaind status
```

We need:

- **`id`**
- **`listen_addr`**

### Add peers

We’ll provide a list with all ID’s and IPs for you to configure your nodes with `--p2p.seeds`

### Genesis time

Have your nodes ready and live by Friday May17th 11am EST / 5pm CET
