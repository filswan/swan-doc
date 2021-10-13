# Reputation System

## Methodology

#### Reputation Score = Time-based Reachability + Regional Weighted Adjusted Power + General Deals and Verified-Storage Provider Deals

### Reputation Score Formula:

The Filswan reputation system is providing an easy way of measuring the storage provider’s storage service quality based on their performance over time and geolocation diversity.

* The max score that the storage providers can have is 100 points.
* The score is based on 3 main sets of metrics, each set with a different weight in the total score:
  * Time-based Reachability - 30% weight
  * Regional Weighted Adjusted Power - 30% weight
  * General Deals and Verified-Storage Provider Deals - 40% weight

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

![](https://www.filswan.com/static/img/Methodology3.905c15e.png)

This max ranking method guarantees a base score for each storage provider and leverages more to the storage providers having larger number of verified-storage provider active deals. The verified-storage provider active rate rank is then normalized by the division of the number of storage providers.

The normalized verified-storage provider active rate rank is calculated with the following mathematical formula:

Normalized Verified-Storage Provider Active Deal Rate Rank = norm \[Rank_Max (Verified-Storage Provider Active Rate)]

The normalized verified-storage provider active rate is then weighted by another parameter, sector faculty rate. Deals fall into faults for some reason will lose weight and storage providers that have less faults are assigned more weight. In this scenario, sector faulty rate is calculated as the ratio of number of faults divided by the number of total live deals.

The sector faulty rate is calculated with the following mathematical formula:

Sector Faulty Rate = number of fault deals / number of live deals

Thus, the deals score is the weighted sum of verified-storage provider deals and external deals with faulty rate considered.

The General deals and verified-storage provider deals score is calculated with the following mathematical formula:

{% hint style="info" %}
General Deals and Verified-Storage Provider Deals Score = 40 \* \[0.3 \* 1 + 0.7 \* (1 - Sector Faulty Rate) \* (Normalized Verified-Storage Provider Active Rank)]
{% endhint %}
