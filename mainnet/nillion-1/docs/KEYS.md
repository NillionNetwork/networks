# Keys

In order to validate on the nillion mainnet you need to create keys.

> DO NOT recycle the mnemonic used for testnet if you are a testnet validator. Please use new keys.

## Create new key

To generate a new key run the following:

```bash
nilchaind keys add <account_name>
```

## Recover key

If you already have a key then you can use the `--recover` flag.

```bash
nilchaind keys add <account_name> --recover
```

This will prompt for the BIP39 mnemonic in order to recover the key.
