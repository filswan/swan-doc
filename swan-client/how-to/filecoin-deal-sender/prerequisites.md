# Prerequisites

If you have set `market_version = "1.2"` in the `config.toml`, you must do the following steps:

* Import the client wallet private key to the swan repo(default: `~/.swan`):

```
./swan-client wallet import wallet.key
```

* Add funds to client wallet Market Actor in order to send deals:

```
lotus wallet market add --from <address> --address <market_address> <amount>
```

**Note：** If you are using `market_version = "1.2"`, please make sure the storage providers are using the `swan-provider` [v2.1.0-rc1](https://github.com/filswan/go-swan-provider/releases/tag/v2.1.0-rc1) at least.
