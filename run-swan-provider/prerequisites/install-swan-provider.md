# Install Swan Provider

#### Prerequisites

```
lotus-miner
go 1.16
sudo apt install aria2
```

{% hint style="danger" %}
Make sure you have lotus miner running with Swan Provider
{% endhint %}

## Install Swan Provider Binary

The Swan Provider is a binary that is created from the [Swan Provider](https://github.com/filswan/go-swan-provider) repository's `go/` path.

It contains both the logic for running an Swan Provider and also provides a CLI for handling registry, staking and other operations.

{% hint style="warning" %}
The Swan Provider is currently only supported on x86\_64 Linux systems.
{% endhint %}

## Downloading a Binary Release <a href="downloading-a-binary-release" id="downloading-a-binary-release"></a>

{% hint style="info" %}
We suggest that you build Swan Provider from source yourself for a production deployment of an Swan Provider.
{% endhint %}

For convenience, we provide binaries that have been built by the FilSwan Team. Links to the binaries are provided in the [release](https://github.com/filswan/go-swan-provider/releases) page.

## Building From Source <a href="building-from-source" id="building-from-source"></a>



Although highly suggested, building from source is currently beyond the scope of this documentation.

See [go-swan-provider](https://github.com/filswan/go-swan-provider) documentation for more details.

The code in the [`main` branch](https://github.com/filswan/go-swan-provider/tree/main) might be incompatible with the code used by other nodes in the production.

Make sure to use the version specified in the release.
