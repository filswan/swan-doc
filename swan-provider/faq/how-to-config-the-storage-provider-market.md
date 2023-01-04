# How to config the Storage Provider Market?

Suppose the public IP address of `Lotus-miner` is `123.123.73.123`。

## 1. Enable the Market Subsystem

Change the following content in the `$LOTUS_MINER_PATH/config.toml`file:

```
[Subsystems]
 EnableMarkets = true
```

## 2. Lotus-miner IP Configuration

Change the following content in the `$LOTUS_MINER_PATH/config.toml`file:

Change the IP in `ListenAddresses` to `123.123.73.123` (the public IP address), specify a fixed port, for example: `1024`；

```toml
[Libp2p]
 ListenAddresses = ["/ip4/123.123.73.123/tcp/1024", "/ip6/::/tcp/0"]
```

After changing the configuration, you need to restart `Lotus-miner`.

## 3. Publish the Multiaddress

Publish your Multiaddress (the `ListenAddresses`, which you configured above) to the chain so that other nodes can talk to it directly and make deals:

```
lotus-miner actor set-addrs /ip4/123.123.73.123/tcp/1024
```

After the message is published and confirmed, you can check the result with the following command:

```
lotus state miner-info [f0xxxx]
```

## 4. Add balance to the Storage Market Actor

```
lotus wallet market add --from=<wallet_address> --address=<miner_ID>
```

## 5. Check the Lotus-miner connectivity

Visit:

```
https://console.filswan.com/#/tools/checkDataCap
```

Enter your storage provider ID to check its status.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

## 6. Config the Lotus-miner's ask

```
lotus-miner storage-deals set-ask --price 0 --verified-price 0 --min-piece-size 56KiB --max-piece-size 32GiB
```

## 7. Filter client (optional)

```
[Dealmaking]
 Filter = "jq -e '.Proposal.Client == \"f1nslxql4pck5pq7hddlzym3orxlx35wkepzjkm3i\" or .Proposal.Client == \"f1stghxhdp2w53dym2nz2jtbpk6ccd4l2lxgmezlq\" or .Proposal.Client == \"f1mcr5xkgv4jdl3rnz77outn6xbmygb55vdejgbfi\" or .Proposal.Client == \"f1qiqdbbmrdalbntnuapriirduvxu5ltsc5mhy7si\" '"
```

### &#x20;              _**Feel free to contact us on**_ [_**Discord**_](https://filswan.com/discord) _**if you have any questions.**_
