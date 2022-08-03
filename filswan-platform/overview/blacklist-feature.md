---
description: Miner blacklist feature
---

# Blacklist Feature

### Introduction

Miner will not only be evaluated on its reputation score, but also on its recent deal rejection history.  A miner rejecting a large number of deals over a long period of time will be put on the miner blacklist and unable to take more deals.

### Methodology

The miner's blacklist status is related to a blacklist score (as the **score** in the rest of the document). The score is will be deducted when miners reject deals without a satisfying reason.

Each newly registered miner will start with 100 scores. And will lose scores on certain rejections (With a threshold of 5 points per day). This makes sure that inactive miners will not receive deals, and reduce the probability of unsuccessful deals occurring.

There are the rejection responses lead to score deduction:

* Filswan being blacklisted: -1
* Unidentified rejection: -0.5
* Unqualified deal: -0.3
* Error message: -0.1
* Deal time out: -0.05

After a miner's score is below 30, the miner will be automatically put on the blacklist.

#### Score recovery

For miners on the blacklist, their score can be recovered by being active. For each day the miner's heartbeat status is **Online**, the miner will gain 1 score until the score reaches 30, and the miner will be removed from the blacklist.

#### Scanning

The miner's deal history will be automatic review each day. Offline deals that are rejected will be scanned for score deduction purposes. And the score will be updated afterwards.

#### Manual blacklist

Miners could also be manually blacklisted for different reasons, without having the score reduced below 30.
