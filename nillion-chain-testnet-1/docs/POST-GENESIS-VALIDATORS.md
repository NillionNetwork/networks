# Post-Genesis Validators

First, [install](./INSTALL.md) and build the nilliond binary.

## **Create account and initialise**

An account is needed for pre-genesis. You will need to generate [keys](./KEYS.md) and then supply the following to Nillion:

You will also need to [initialise](./INITIALISE.md) the node.

### Download genesis file.

Download the genesis file from this repo:

```
wget https://raw.githubusercontent.com/NillionNetwork/networks/main/nillion-chain-testnet-1/genesis.json -O .nillionapp/config/genesis.json
```

### Add peers

Add the peers from the [peers.txt](../peers.txt) file in this repo into seeds field the `[p2p]` section in the `config.toml`.

### Start node

Start your node and let it catch up to the head of the chain.

```
nilliond status | jq .sync_info.catching_up
```
should return `false` when caught up.  

### **Submit validator message**

To allow your node to start validating you will need to submit a create validator message:

```bash
nilliond tx staking create-validator \
--amount=<amount> \
--pubkey=$(nilliond comet show-validator) \
--moniker="<moniker>" \
--chain-id="nillion-chain-testnet-1" \
--commission-rate="<commission>" \
--commission-max-rate="<max-commission>" \
--commission-max-change-rate="<max-commission-rate-change>" \
--min-self-delegation="<min-self-delegation>" \
--fees=<fees> \
--from=<key-name>
```

This will upgrade the node to validator status and it will be included in consensus.
