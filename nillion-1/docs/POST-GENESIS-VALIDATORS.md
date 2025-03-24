# Post-Genesis Validators

First, [install](./INSTALL.md) and build the nilchaind binary.

## **Create account and initialise**

An account is needed for pre-genesis. You will need to generate [keys](./KEYS.md) and then supply the following to Nillion:

You will also need to [initialise](./INITIALISE.md) the node.

### Download genesis file.

Download the [genesis](../genesis.json.xz). Unpack the xz file and confirm the file sha256 matches that of [genesis.sha256](../genesis.json.sha256) and add to the `.nillionapp/config` directory

### Add seeds

Add the seeds from the [seeds.json](../seeds.json) file in this repo into seeds field the `[p2p]` section in the `config.toml`.

### Add peers

Add the peers from the [peers.json](../peers.json) file in this repo into persistent peers field the `[p2p]` section in the `config.toml`.

### Start node

Start your node and let it catch up to the head of the chain.

```
nilchaind status | jq .sync_info.catching_up
```

should return `false` when caught up.

### **Submit validator message**

To allow your node to start validating you will need to submit a create validator message:

```bash
cat <<EOF > validator.json
{
	"pubkey": $(nilchaind comet show-validator),
	"amount": <amount>,
	"moniker": "<moniker>",
	"identity": "<keybase>",
	"website": "<url>",
	"security": "<email>",
	"details": "<details>",
	"commission-rate": "<commission>",
	"commission-max-rate": "<max-commission>",
	"commission-max-change-rate": "<max-commission-rate-change>",
	"min-self-delegation": "<min-self-delegation>"
}
EOF

nilchaind tx staking create-validator validator.json \
--chain-id="nillion-1" \
--fees=<fees> \
--from=<key-name>
```

This will upgrade the node to validator status and it will be included in consensus.
