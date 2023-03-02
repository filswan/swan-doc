# Reputation System

## Concept

**Status**: Active/Inactive.if a  lotus SP is running and reachable, it should report it with:

```shell
$ lotus-miner net reachability
```

**Heartbeat**: If the Lotus SP running Swan Provider,the swan provider will send out heartbeat to swan Platform every 5 minutes. It connected to Swan platform, the value is **Online**, otherwise it will be **offline**

## Reputation Score

### Methodology

#### Reputation Score = Base Score+ Bidding Score

**Base Score** = Time-based Reachability + Regional Weighted Adjusted Power + Deals

**Bidding Score**



### Reputation Score Formula:

The reputation system can conduct a comprehensive evaluation of various parameters of the nodes. It integrates running time, geographical location, regional influence, quantity, packet loss rate, failure rate, and real-time transaction to perform mathematical weighting. Afterward, it will generate an overall ranking and a quantitative evaluation of storage provider nodes. Growing data storage tasks received by top providers can lead to a more stable running system. Meanwhile, the reputation system ensures a focus on node operation and maintenance, thereby promoting the security and stability of the Filecoin storage network. It keeps users away from the hassle of seeking service providers. &#x20;

* The max score that the storage providers can have is 100 points.
* The score is based on 3 main sets of metrics, each set with a different weight in the total score:
  * Time-based Reachability - 30% weight
  * Regional Weighted Adjusted Power - 10% weight
  * General Deals and Verified-Storage Provider Deals - 60% weight

### 1. Time-based Reachability:

Time-based reachability measures the times of successful and failed requests when storage providers are scanned. The ratio of successful request count to total request count (successful request plus failed request) is the key metric used here.

Request Successful (reachable) = 1

Request Failed (unreachable) = 0

Success Rate = reachable count/ total count

In addition to the overall request success ratio, the latest request performance of storage providers in the recent few scans will be considered. The reason is that the system rewards storage providers based on their recent performances. The ratio of successful request count and total request count during the last 10 scans is calculated to represent the recent behavior. The weight of online reachability of all time and online reachability in the latest scans are 0.7 and 0.3, respectively.

The Reachability score is calculated with the following mathematical formula:

{% hint style="info" %}
Time-based Reachability Score = 30 \* (0.7 \* Online Reachability Total Success Rate + 0.3 \* Online Reachability Top10 Success rate)
{% endhint %}

![](<../../.gitbook/assets/image (33).png>)

### **2. Regional Weighted Adjust Power:** <a href="#reputationsystemdesign-2.regionalweightedadjustpower" id="reputationsystemdesign-2.regionalweightedadjustpower"></a>

The regional committed sector proof score is designed to measure the total committed capacity of the miner. The bigger the miner is the more collateral is required, and the technical support effort also increased. The importance of a miner in the region is inversely proportional to the total number of miners in the region, e. g. a miner in a 1-miner region is 10x more important than a miner in a 10-miner region since it is the only service provider.

To emphasize the importance of the miner of the region, we use the regional weighted adjust power to show the weight of the miner in the region.

![](../../.gitbook/assets/1.png)

The weighted adjust power is calculated with the following mathematical formula:

&#x20;                                         _Location Weight = 0.5 + 0.5 \* exp( -1 \* number of miners in its continents)_

&#x20;                                         _Number Weight  = 0.5+ 0.5 \* exp( -1 \* total adjusted power in its continents / total adjusted power worldwide)_&#x20;

&#x20;                                         _Weighted adjust power = Location Weight \* Number Weight \* adjusted power_

After adjusting the power by the location, the weighted adjusted power is then transformed by a log transformation so that the distribution of log weighed adjusted power is closer to a normal distribution. Then the log weighted adjusted power is normalized using min-max normalization approach.

The normalized log weighted adjust power is calculated with the following mathematical formula:

&#x20;                                       _Normalized Log Weighted Adjusted Power = norm \[log (Weighed Adjusted Power)]_

The normalized result is a number in the interval \[0,1] where 1 is the maximum score. A miner that has a score of 1 is rewarded with 30 reputation points.

The Reachability score is calculated with the following mathematical formula:

{% hint style="info" %}
_Committed Sectors Proof Score = 10\* Normalized Log Weighted Adjusted Power_
{% endhint %}

### 3. General Deals and Verified-Storage Provider Deals:

The 3rd component of the score reflects the proportion in which the Web3 Storage Provider (W3SP) has successfully run the storage deals. Making storage deals is the core of a Web3 Storage Provider (W3SP) and thus this component has the biggest weight in the score. The deals considered here involve both internal deals (swan deals) and external deals (general deals). The Web3 Storage Provider (W3SP) active rate accounts for the key parameter, defined as the ratio of the number of active deals divided by the number of total deals. The active rate for external deals is set to 1 for now and will be updated later on.

A verified Web3 Storage Provider (W3SP) is a Web3 Storage Provider (W3SP) who signed with their Web3 Storage Provider (W3SP)’s signature and email address, they usually also update their contact information in Swan or other platforms.

The deals considered here involve both verified-Storage Provider deals and external deals (general deals). The Web3 Storage Provider (W3SP) active rate accounts for the key parameter, defined as the ratio of the number of active deals divided by the number of total deals. The active rate for external deals is set to 1 for now and will be updated later on.

The verified-Storage Provider active rate is calculated with the following mathematical formula:

Verified-Storage Provider Active Deal Rate = the number of active deals/numbers of total deals After Web3 Storage Providers (W3SP) are ranked by the calculated verified Web3 Storage Provider (W3SP) active rate in increasing order with the method set to "max". In other words, the records that have the same values are ranked using the highest rank (e.g.: If ‘Tom’ and ‘Jerry' are tied in the 2nd and 3rd position with the same value, rank 3 is assigned to them both).

![](https://console.filswan.com/static/img/Methodology3.905c15e.png)

This max ranking method guarantees a base score for each Web3 Storage Provider (W3SP) and leverages more to the Web3 Storage Providers (W3SP) having a larger number of verified-Storage Provider active deals. The verified-Storage Provider active rate rank is then normalized by the division of the number of Web3 Storage Providers (W3SP).

The normalized verified-Storage Provider active rate rank is calculated with the following mathematical formula:

Normalized verified-Storage Provider Active Deal Rate Rank = norm \[Rank\_Max (Verified-Storage Provider Active Rate)]

The normalized verified-Storage Provider active rate is then weighted by another parameter, the sector faculty rate. Deals that fall into faults for some reason will lose weight and Web3 Storage Providers (W3SP) that have fewer faults are assigned more weight. In this scenario, the sector faulty rate is calculated as the ratio of the number of faults divided by the number of total live deals.

The sector faulty rate is calculated with the following mathematical formula:

Sector Faulty Rate = number of fault deals/number of live deals

Thus, the deals score is the weighted sum of verified-Storage Provider deals and external deals with faulty rates considered.

The General deals and verified-Storage Provider deals score is calculated with the following mathematical formula:

General Deals and verified-Storage Provider Deals Score = 60 \* \[0.3 \* 1 + 0.7 \* (1 - Sector Faulty Rate) \* (Normalized verified-Storage Provider Active Rank)]

### Bidding Score

The bidding score will affect the probability of Swan provider receiving deals. Swan providers with higher bidding scores will receive more deals in the long term.

_Biding Score_ = _Heartbeat Score_ \* 60% + _Deal Score \* 40%_

#### Heartbeat Score

The heartbeat score algorithm considers a swan provider's recent (weekly & daily) heartbeat activity. The heartbeat score gradually increases as the heartbeat rate increases.

Heartbeat Score = Heartbeat Rate ^ e

<figure><img src="../../.gitbook/assets/Screenshot 2023-02-15 at 1.20.25 PM.png" alt=""><figcaption><p>Heartbeat Score to Hearbeat Rate</p></figcaption></figure>

#### Deal Score

The deal score evaluates a swan provider's recent (monthly & weekly) deal success rate.&#x20;

_Deal Score_ = -2 (_Deal Success Rate_ + 1)^-1 + 1

<figure><img src="../../.gitbook/assets/Screenshot 2023-02-15 at 1.35.08 PM.png" alt=""><figcaption><p>Deal Success Rate to Deal Score</p></figcaption></figure>

#### To Increase Bidding Score

The bidding score will be increased if Swan Provider can maintain a consistent heartbeat on a daily basis and secure higher weekly and monthly deal success rates.

## **Blacklist Rule**

### Introduction

Miners will be evaluated not only on their reputation score but also on their recent deal rejection history.  If a miner rejected a large number of deals over a long period of time, its score will be conducted deduction. The deduction is possible to put the miner on the blacklist and enable it to take more deals.&#x20;

### Methodology

The miner's blacklist status is related to a blacklist score (as the **score** in the rest of the document). The score will be deducted when miners reject deals without a satisfying reason.

Each newly registered miner will start with 100 scores. And miner will lose scores on certain rejections (With a threshold of 5 points per day). This makes sure that inactive miners will not receive deals, and reduce the probability of unsuccessful deals occurring.

There are the rejection responses lead to score deduction:

* Filswan being blacklisted: -1
* Unidentified rejection: -0.5
* Unqualified deal: -0.3
* Error message: -0.1
* Deal time out: -0.05

After a miner's score is below 30, the miner will be automatically put on the blacklist.

#### Removal from Blacklist

For miners on the blacklist, their score can be recovered by being active. For each day the miner's heartbeat status is **Online**, the miner will gain 1 score until the score reaches 30, and the miner will be removed from the blacklist.

* Online per day: +1

#### Scanning

The miner's deal history will be automatic review each day. Offline deals that are rejected will be scanned for score deduction purposes. And the score will be updated afterwards.



