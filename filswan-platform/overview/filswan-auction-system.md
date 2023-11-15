# Swan Auction System

## Introduction to Swan Auction System

Filecoin users need to find suitable storage providers in the first instance. They need to actively seek providers, bargain offline, send data files, lock fees, and proceed with payment once file storage is completed as requested. &#x20;

**Over the course, there remain several key questions:**&#x20;

1\. Users can't fully understand the specific service quality of storage providers because of limited information available.&#x20;

2\. The lack of in-depth matching functionality, and diverse data storage needs are making the dealer market opaque.&#x20;

3\. There are not enough choices available for beginners. It is time-consuming as well as costly to find and compare storage providers that will work best for them.&#x20;

In this context, having an open and transparent matching system is necessary. Swan's auction system is optimal for simplifying data storage through matching providers and users in need automatically, thereby reducing the learning cost for users.&#x20;

#### Manual bid vs Auto-bid

**Manual Bid**

There are two types of bids in the Swan system. One is manual bid, and the other is auto-bid. Manual bidding is a system designed for users who are actively involved in the bidding. When bidding manually, users select providers in accordance with their bandwidth, storage capacity, geographic location, and daily processing ability. Similarly, users compare and filter attributes of assorted products on shopping platforms.

Users cannot avoid other users’ interactions because they need to know who they expect to take the deal. Afterward, users can send the deal. It consists of two steps: the first step is to open the deal bid, and the second step is to assign the bid. Users assign transactions to different storage providers to solicit public bids. Providers then store the data as requested after winning the bid. Since this step is open to the public, we call it an “open public deal”, which means that anybody in the system can compete for it.

After several satisfying bids, the user may be willing to build long-term private cooperation with the storage provider. So, they may skip the bidding process and send deals directly to each other in the future. We call this case a “private deal”.

One advantage of the manual bid system is that tipping the tasks makes it more flexible while bidding.

**Autobid**&#x20;

![Autobid System](<../../.gitbook/assets/image (27).png>)

The auto bidding system is a reputation-based system. When users sign up as a storage provider, they will be rated based on the data they processed. The more data they process, the higher score they will achieve.&#x20;

In the auto-bidding system, users are free from hassles like choosing storage providers. The system selects providers automatically while ensuring fairness. When a user sends out a deal to the auto bidding pool, the storage provider will be assigned the deal based on their reputation score. The higher score you have, the more likely they will win a bid.&#x20;

The FileSwan bidding system is a matching platform that enables convenient transactions between users and providers. In the era of decentralized storage, Swan ensures a quick pair of users and storage providers for the sake of time-efficient storage and backup services regardless of data scales.&#x20;

The Swan bidding system increases the earnings of real data storage. It additionally reduces the leverage difficulty to attract more novice users. &#x20;

The market matcher program distributes the order following a lambda distribution, which means that even if the storage provider scores low, he is still able to get some deals.

**Task**&#x20;

It is of great importance to conceptualize "task" in the Swan system. A task consists of several deals. Currently, Filecoin only accepts deals of specified sizes, eg., a maximum of 32 gigabytes or 64 gigabytes. If you want to store a data more than one terabyte or 10 terabytes, you need to split it to different deals manually to send them. This could make deal management daunting.&#x20;

In order to batch send deals, we have created a conception called “tasks”. A task is a combination of deals. Users can name it, label it, and define the curated dataset type for future usage.

**Swan Provider**&#x20;

The Swan Provider runs on the same node as the lotus miner nodes run, and assists lotus miners to process deals. In order to better share the information with the Flilswan client, [authentication](../../run-swan-provider/broken-reference/) from the Filswan platform is required.&#x20;

Swan provider also keeps your status up to date. With the Swan platform, your client can get your shared information about the file sealing life cycle.

We also provide the Restful API interface for developers to integrate the Swan Provider into their own system.

Read more: [https://github.com/filswan/go-swan-provider](https://github.com/filswan/go-swan-provider)
