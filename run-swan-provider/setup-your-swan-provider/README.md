# Setup Your Swan Provider

Setup Your Swan Provider Make sure you followed [prerequisites](../prerequisites/ "mention") before configuration

## Step 1: Obtain your API keys

Get your[ API Keys](../../getting-started/authentication/api-keys.md) so that Swan can authenticate your integration’s API requests.

### Step 2: Start Swan Provider

Make sure your [Lotus miner](https://docs.filecoin.io/mine/lotus/) is running one the same machine as the Swan provider will communicate with it and cannot work otherwise.

```
./swan-provider
```



The first time start swan provider will be interrupted due to incorrect configuration.

Launching `swan-provider` creates a default configuration. The config file locations are platform specific:

* Linux:` ~/.swan/provider/config.toml`

edit \~/.swan/provider/config.toml as follows

```
```



