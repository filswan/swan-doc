# FilSwan Auction System

## Introduction to FilSwan Auction System

FilSwan is aiming at building an enterprise-level solution based on the Filecoin network. At this moment we have more than 3000+ nodes on the Filecoin network. However, there are lots of limitations to the full use of those nodes for storage and computing. Even though we have so many nodes , we do not know what spec they have. Are they hosted at home or an data center? What would be the expectation of storage clients? Do they really want the storage to fit the compliance like PCI-DSS? Or they just simply want to store some data on the network so that they can retrieve them as a backup in the future?

### Auction System

FilSwan provides an auction system to solve the issue. On FilSwan platform, users are allowed to enter their current hardware spec. For example, hosetd in a data center with 10 gigabyte network and is looking for a specific amount of price for storage. In order to meet all different requirements from users and match them with the storage providers, we developed a FilSwan auction system to meet the needs.

#### Manual bid vs Auto bid

**Manual Bid**

There are two types of bids in the FilSwan system. One is a manual bid; and the other is an auto bid. Manual bidding is a system designed for users who are actively involved in the bidding. The user needs to enter information about their storage provider manually, for example, the bandwidth, the pricing, the geo-location, and their capability of processing per day. When users are using the manual bidding system, they need to manually take the bid from the user interface or use API to win a bid.

The user cannot avoid other users’ interactions because they need to know who they expect to take the deal from. Afterwards the user can send the deal to them. It consists of two steps of dealing. The first step is to open the deal bid. The second step is assigning the bid. After the storage provider wins the bid. The storage provider can start sealing whenever the user wants. Since this step is open to the public, we call this kind of deal an “Open public deal”, which means that anybody in the system is competing for the bid.

As often happens, several times after the bid, the client might find that their storage provider is willing to work on a long-term basis. So, they may skip the bidding part and send deals directly to users in the future. We call this case as a “private deal”.

One advantage using manual bid system is you can send tips for each task, so it is more flexible in bidding.

**Autobid**&#x20;

![Autobid System](<../../.gitbook/assets/image (27).png>)

The auto bidding system is a reputation-based system. When a user signs up as a storage provider, the more they process, the higher score they will achieve as a storage provider. When they set the auto bid flag in your configuration on your storage provider, they will be able to join the auto bid pool. When a user sends out a deal to the auto bidding pool, the storage provider will be assigned deal based on their reputation score. The higher you are, the more chance they will win a bid. For example, if client want to send a deal size at 4Gb. If a storage provider is willing to accept deals bellow 4 Gb, they can win the bid. But if the storage provider receiving range is between 8 gigabytes to 16 gigabytes, he may lose the bid, because he is not in the range that they want.

The market matcher program distributes the order follow a lambda distributionm which means that even the storage provider score is low, he is still be able to get some deal, just a lower chance.

**Task **

In FilSwan system we have an important conception called tasks. A task consists of several deals. Currently, Filecoin only accepts specified size of deals. For example, maximum 32 gigabytes or 64 gigabytes depending on the storage provider you stored. If you want to store a data more than one terabyte or 10 terabytes, you need to manually split it to different deals, and then send them out. This could make the management of the deals difficult. In order to send more deals in a batch, we have created a conception called “tasks”. A task is a combination of deals, and you can give it a task name and label name. You can also define the curated dataset type for future usage.

**Swan Storage Provider**&#x20;

Swan storage provider is an agent running on the filecoin storage provider host. It is compatible with the latest version of Lotus provider. The uses the storage provider, manage your importing process, set up the heartbeat with swamp platform and bidding as with manual bidder or auto Bider.

Swan provider also keeps your status up to date. With the Swan platform, your client get your shared information about the file sealing life cycle.

We also provide the Restful API interface for developers to integrate swan provider to their own system.

Installation instructions for the Swan storage can be found here:

[https://github.com/filswan/go-swan-provider](https://github.com/filswan/go-swan-provider)
