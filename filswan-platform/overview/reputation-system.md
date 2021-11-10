# Reputation System

## Methodology

#### Reputation Score = Time-based Reachability + Regional Weighted Adjusted Power + General Deals and Verified-Storage Provider Deals

### Reputation Score Formula:

The Filswan reputation system is providing an easy way of measuring the storage provider’s storage service quality based on their performance over time and geolocation diversity.

* The max score that the storage providers can have is 100 points.
* The score is based on 3 main sets of metrics, each set with a different weight in the total score:
  * Time-based Reachability - 30% weight
  * Regional Weighted Adjusted Power - 10% weight
  * General Deals and Verified-Storage Provider Deals - 60% weight

### 1.Time-based Reachability:

Time-based reachability is measuring the times of successful and failed requests when storage providers are scanned. The ratio of successful request count to total request count (successful request plus failed request) is the key metric used here.

Request Successful (reachable) = 1

Request Failed (unreachable) = 0

Success Rate = reachable count/ total count

In addition to the overall request success ratio, the latest request performance of storage providers in the recent few scans are considered into equation. The reason for adding recent behavior is that the system gives a higher reward to storage providers with recent good performances. The ratio of successful request count and total request count during the last 10 scans is calculated to represent the recent behavior. The weight of online reachability of all time and online reachability in the latest scans are 0.7 and 0.3, respectively.

The Reachability score is calculated with the following mathematical formula:

{% hint style="info" %}
Time-based Reachability Score = 30 \* (0.7 \* Online Reachability Total Success Rate + 0.3 \* Online Reachability Top10 Success rate)
{% endhint %}

![](https://www.filswan.com/static/img/Methodology.3b35506.png)

### **2. Regional Weighted Adjust Power:** <a href="reputationsystemdesign-2.regionalweightedadjustpower" id="reputationsystemdesign-2.regionalweightedadjustpower"></a>

The regional committed sector proof score is designed to measure the total committed capacity of the miner. The bigger the miner is the more collateral is required, and the technical support effort also increased. The importance of a miner in the region is inversely proportional to the total numbers of miners in the region, e. g. a miner in a 1-miner region is 10x more important than a miner in a 10-miner region since it is the only service provider.

In order to emphases the importance of the miner of the region, we use the regional weighted adjust power to show the weight of the miner in the region.

![](../../.gitbook/assets/1.png)

The weighted adjust power is calculated with the following mathematical formula:

_                                          Location Weight = 0.5 + 0.5 \* exp( -1 \* number of miners in its continents)_

_                                          Number Weight  = 0.5+ 0.5 \* exp( -1 \* total adjusted power in its continents / total adjusted power worldwide) _

_                                          Weighted adjust power = Location Weight \* Number Weight \* adjusted power_

After adjusting the power by the location, the weighted adjusted power is then transformed by a log transformation so that the distribution of log weighed adjusted power is closer to a normal distribution. Then the log weighted adjusted power is normalized using min-max normalization approach.

The normalized log weighted adjust power is calculated with the following mathematical formula:

&#x20;                                       _ Normalized Log Weighted Adjusted Power = norm \[log (Weighed Adjusted Power)]_

The normalized result is a number in the interval \[0,1] where 1 is the maximum score. A miner that has a score of 1 is rewarded with 30 reputation points.

The Reachability score is calculated with the following mathematical formula:

{% hint style="info" %}
_Committed Sectors Proof Score = 10\* Normalized Log Weighted Adjusted Power_
{% endhint %}

### **3. General Deals and Verified-Miner Deals:** <a href="reputationsystemdesign-3.generaldealsandverified-minerdeals" id="reputationsystemdesign-3.generaldealsandverified-minerdeals"></a>

The 3rd component of the score reflects the proportion in which the miner has successfully run the storage deals. Making storage deals is the core of a miner and thus this component has the biggest weight in the score.&#x20;

A verified miner is a miner who signed with their miner’s signature and email address, they usually also update their contact information in Swan or other platforms.

The deals considered here involve both verified-miner deals and external deals (general deals). The miner active rate accounts for the key parameter, defined as the ratio of number of active deals divided by the number of total deals. The active rate for external deals is set to 1 for now and will be updated later on.

The verified-miner active rate is calculated with the following mathematical formula:

&#x20;  _                                     Verified-miner Active Deal Rate = number of active deals / numbers of total deals_

After miners are ranked by the calculated verified miner active rate in increasing order with method set to "max". In other words, the records that have the same values are ranked using the highest rank (e.g.: If ‘Tom’ and ‘Jerry' are tied in the 2nd and 3rd position with the same value, rank 3 is assigned to them both).&#x20;

![](https://www.filswan.com/static/img/Methodology3.905c15e.png)

This max ranking method guarantees a base score for each storage provider and leverages more to the storage providers having larger number of verified-storage provider active deals. The verified-storage provider active rate rank is then normalized by the division of the number of storage providers.

The normalized verified-storage provider active rate rank is calculated with the following mathematical formula:

Normalized Verified-Storage Provider Active Deal Rate Rank = norm \[Rank\_Max (Verified-Storage Provider Active Rate)]

The balanced verified-storage provider active rate is then weighted by another parameter, sector faculty rate. Deals fall into faults for some reason will lose weight and storage providers that have less faults are assigned more weight. In this scenario, sector faulty rate is calculated as the ratio of number of faults divided by the number of total live deals.

The sector faulty rate is calculated with the following mathematical formula:

Sector Faulty Rate = number of fault deals / number of live deals

Thus, the deals score is the weighted sum of verified-storage provider deals and external deals with faulty rate considered.

The General deals and verified-storage provider deals score is calculated with the following mathematical formula:

{% hint style="info" %}
General Deals and Verified-Storage Provider Deals Score = 60 \* \[0.3 \* 1 + 0.7 \* (1 - Sector Faulty Rate) \* (Normalized Verified-Storage Provider Active Rank)]
{% endhint %}
