# 12. How to set the "ask price"?

The minimum verified deal is 1MiB, therefore the following configuration is required:

```
lotus-miner storage-deals set-ask --price 0 --verified-price 0 --min-piece-size 1MiB --max-piece-size 32GiB
```
