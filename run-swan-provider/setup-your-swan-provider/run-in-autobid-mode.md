---
description: An autobid market build by filswan
---

# Run in autobid mode

Autobid is a simplified process for swan provider who can fast join the auction process. By default, swan provider is running in autobid mode.

![Task Distribution to multiple Swan Provider](<../../.gitbook/assets/image (25).png>)

edit `~/.swan/provider/config.toml `as follows

```
...

bid_mode = 1 

...
```

### Restart the Swan Provider <a href="starting-the-miner" id="starting-the-miner"></a>

You are now ready to stop & restart your swan provider

```
./swan-provider
```

