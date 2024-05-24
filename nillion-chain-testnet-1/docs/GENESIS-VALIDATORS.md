# Genesis Validators

First, [install](./INSTALL.md) and build the nilliond binary.

## **Create account and initialise**

An account is needed for pre-genesis. You will need to generate [keys](./KEYS.md) and then supply the following to Nillion:

- `address`
- `pubkey`

You will also need to [initialise](./INITIALISE.md) the node and add your genesis account:

```bash
nilliond genesis add-genesis-account <account_name> 1000000unil
```

## **Submit gentx**

It is run on the computer that hosts the cold validator operator app key, using the keyring of your choice. Collect the consensus public key from CometBFT KMS.

```bash
nilliond genesis gentx <account_name> 1000000unil --chain-id=nillion-chain-testnet-1 --moniker=<your moniker> --details=<your desc> --commission-rate=0.05 --commission-max-rate=0.2 --commission-max-change-rate=0.02 --pubkey=$(nilliond comet show-validator) --identity=<your ident> --security-contact <your-email> --keyring-backend os
```

This creates a JSON file on the validator's computer, typically in `~/.nillionapp/config/gentx/`

Create a PR with your JSON in this repo with your gentx in this folder [nillion-chain-testnet-1/gentx](../gentx)

## Testnet launch

### **Download final genesis**

Download the [genesis](../genesis.json) and add to the `.nillionapp/config` directory

### Set short commit timeout

Please set the `timeout_commit = "1s"` in `config.toml`

### **Submit node details**

Start your node and get its status via:

```
nilliond status
```

We need:

- **`id`**
- **`listen_addr`**

### Add peers

We’ll provide a list with all ID’s and IPs for you to configure your nodes with `--p2p.seeds`

### Genesis time

Have your nodes ready and live by Friday May17th 11am EST / 5pm CET
