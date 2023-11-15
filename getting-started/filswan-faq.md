# FAQ

## Who should use Swan?

Customers who want to store data files to Decentralized network. Filswan provides plenty of useful tools to help clients manage their data, encryption, trunk data to small data pieces, retrieval the dataset, fully backup data to filecoin network, find best service providers and simplify the transfer and storage process.

Storage providers on Filecoin network want a fully automatic solution for data lifecycle management, server resource management, reporting and billing.

## **How does** Swan **work?**&#x20;

Unlike traditional cloud providers, Swan does not operate any physical infrastructure. Instead, we maintain a cluster of application servers connected to various decentralized nodes. This results in a lower overhead and capital expense due to fewer servers.﻿

## Are there any fees or subscriptions to use Swan?

There is no sign-up fee nor any subscription fees. Swan provides a variety of free services and supports to early ecological enterprises. Swan operates using a pay-as-you-go model, meaning clients will only be paying for the storage space they are using.

## Does Swan have object size limits?

There is no limit to how much data a client can store through the Swan platform.

Objects stored on Filswan can range in size from a minimum of 0 bytes to a maximum of 300GB. The largest object that can be uploaded in a single HTTP PUT or POST is 5GB. If you want to upload an object larger than 5GB, you will need to initiate a multipart upload via our S3 API. However, Swan can accommodate clients who are looking to store data large datasets (TB and PB). Clients seek out and make data storage deals with storage providers who are willing to make offline deals.

## What type of file configuration do I need?

Files store on Filswan are configured into a meta-CSV file. A meta-CSV provides addition instructions to the storage provider to be able to store the data file properly.

To learn more about file configuration and how to generate a Car file please consult the following link for more information: [https://github.com/filswan/swan-client](https://github.com/filswan/swan-client)

## Do you have a customer referral program?

No, we do not, but feel free to invite friends to explore the platform using our telegram and Twitter accounts!

## What are the requirements that a storage provider needs to meet for autoBid?

There are several requirements need to be fulfilled for participating in autoBid. Firstly, your SP status should be '**Active**'; then, your SP should be registered as a Swan SP and select **accept offline deals** at registration; also, run our SP service and set '**bid\_mode**' to 1 and provide other values such as '**expected\_sealing\_tim**e' and '**start\_epoch**'.&#x20;

For more information about how to register storage provider, please consult \*\*\*\*(link).

#### To participate in the AutoBid mode.

1. Make sure your storage provider is **Active** and capable to be scanned on chain.
2.  Edit your storage provider's **price, verified-price, min-piece-size,** and **max-piece-size** as follow:&#x20;

    * ```
      lotus-miner storage-deals set-ask --price= --verified-price= --min-piece-size= --max-piece-size=
      ```

    _<mark style="color:blue;background-color:yellow;">Tips: set reasonable prices and a wide range of piece-size will help you get more deals.</mark>_
3. Register your storage provide as a Swan SP. The **accept offline deals** must to be **ON** at the time of registration.
4. Run Swan SP. Our heartbeat feature will regularly send signals to the server, to indicate whether your SP is **online**. Only online SP can get deals.
5.  Edit **bid\_mode**, **expected\_sealing\_time**, and **start\_epoch** in the config.toml file.

    edit `~/.swan/provider/config.toml` as follows:

    ```
    ...

    bid_mode: 1 
    expected_sealing_time: //1920 epoch or 16 hours.
    start_epoch: //2880 epoch or 24 hours.

    ...
    ```

You are now qualified to participate in AutoBid.
