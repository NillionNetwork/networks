# Keys

In order to validate on the nillion testnet you need to create keys.

## Create new key

To generate a new key run the following:

```bash
nilliond keys add <account_name>
```

## Recover key

If you already have a key then you can use the `--recover` flag.

```bash
nilliond keys add <account_name> --recover
```

This will prompt for the BIP39 mnemonic in order to recover the key.
