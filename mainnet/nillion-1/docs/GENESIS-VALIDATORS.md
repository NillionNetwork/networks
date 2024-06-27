# Genesis Validators

First, [install](./INSTALL.md) and build the nilchaind binary.

## **Create account and initialise**

An account is needed for genesis. You will need to generate [keys](./KEYS.md).

You will also need to [initialise](./INITIALISE.md) the node and add your genesis account:

```bash
nilchaind genesis add-genesis-account <account_name> 1000000unil
```

## **Submit gentx**


It is run on the computer that hosts the cold validator operator app key, using the keyring of your choice. Collect the consensus public key from CometBFT KMS.

```bash
nilchaind genesis gentx <account_name> 1000000unil --chain-id=nillion-1 --moniker=<your moniker> --details=<your desc> --commission-rate=0.05 --commission-max-rate=0.2 --commission-max-change-rate=0.02 --pubkey=$(nilchaind comet show-validator) --identity=<your ident> --security-contact <your-email> --keyring-backend os
```

This creates a JSON file on the validator's computer, typically in `~/.nillionapp/config/gentx/`

Create a PR with your JSON in this repo with your gentx in this folder [nillion-1/gentx](../gentx).  Please also include:

- `address`
- `pubkey`

in the PR description.


## Mainnet launch

### **Download final genesis**

Download the [genesis](../genesis.json) and add to the `.nillionapp/config` directory

### Set short commit timeout

Please set the `timeout_commit = "1s"` in `config.toml`

### **Submit node details**

Start your node and get its status via:

```
nilchaind status
```

We need:

- **`id`**
- **`listen_addr`**

### Submit Peer (Optional)

If you would like your node to be in the peers list, please submit a PR adding your id and listen address to [peers.txt](../peers.txt)

### Add seeds and peers

Once the peers and seeds have been populated, you can add them to your config prior to genesis.

### Genesis time

Have your nodes ready and live by TBD
