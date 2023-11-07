# Extend DataCap Terms Service

The Extend DataCap Terms Service is designed to support Storage Providers in extending the expiration of their sectors' terms to maintain the 10x QA(quality-adjusted) power.

### Requirements:

Before you get started with the [Extend Datacap Terms Service](https://datacap.swanchain.io/)., please ensure that you meet the following requirements:

1. The sectors must be active.
2. The deals must be received from the Swan platform.
3. The sector's proof time must be after V17 (2383680, 2022-11-30 140000 UTC).
4. Ensure that you have `lotus-miner` version 1.23.0 or higher installed.

### Extend Duration:

1. The sector expiration time can be extended by 180 days, 360 days, or 540 days.
2. The sector's maximum expiration time cannot exceed 540 days.

### How to Extend Datacap Sectors Expiration:&#x20;

According to [FIP0045](https://github.com/filecoin-project/FIPs/blob/master/FIPS/fip-0045.md), if you want to extend the DataCap sectors' expiration, you need to follow these two steps:

#### **Step One :**&#x20;

The **Client** needs to update the `TermMax` of the Claim for every deal in the sectors:

```
lotus send --from <deal_wallet> --method 11  --params-json '{"Terms":[{"Provider":1836766,"ClaimID":13847890,"TermMax":3680640}]}' f06 0
```

#### **Step Two :**&#x20;

The **Storage Provider** needs to extend the sector expiration:

```
lotus-miner sectors extend --extension=1555200  --really-do-it=true --drop-claims=true  --sector-file=[sector_file]
```

[Swan's Extend Datacap Terms Service](https://datacap.swanchain.io/) can help you with [**Step One**](extend-datacap-terms-service.md#step-one), and the provider needs to perform [**Step Two**](extend-datacap-terms-service.md#step-two).

### A Step-by-Step Guide

1. Head over to [Extend Datacap Terms Service.](https://datacap.swanchain.io/)
2. Fill in your **Storage Provider ID** and upload the list of your **Sector IDs** (follow the template file).
3. Select the **Extension** (extending time) and choose the claims you want to extend.
4. Provide your **Email** and **Transaction CID** to claim your request.
5. Click "**Claim**," and you will receive a confirmation email.
6. After confirming your payment, the FilSwan team will complete [**Step One**](extend-datacap-terms-service.md#step-one) and reply with the corresponding sector information via email.
7. Download the sectors file and run the command to complete [**Step Two**](extend-datacap-terms-service.md#step-two):

```
lotus-miner sectors extend --extension=518400 --really-do-it=true --drop-claims=true --sector-file=[sector_file]
```

**The extension days:**

| Days | Epoch   |
| ---- | ------- |
| 180  | 518400  |
| 360  | 1036800 |
| 540  | 1555200 |
