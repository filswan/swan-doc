# Basic Concept

### Task

In swan project, a task can contain multiple offline deals. There are two basic type of tasks: public task and private task.

Users can also set auto-bid mode to automatically send and receive deals.&#x20;

#### **Task type:**

* Public Task:
  * A public task is a deal set for open bid. If the bid mode is set to manuall,after bidder win the bid, the task holder needs to propose the task to the winner. If the bid mode is set to auto-bid, the task will be automatically assigned to a selected storage provider based on reputation system and Market Matcher.
* Private Task:
  * A private task is used to propose deals to a specified storage provider
* Auto-bid Mode:
  * The autobid system between swan-client and swan-provider allows you to automatically send deals to a miner selected by Swan platform. All miners with auto-bid mode on have the chance to be selected but only one will be chosen based on Swan reputation system and Market Matcher. The auto bidding system is a[ reputation-based system](../filswan-platform/overview/reputation-system.md). When a user signs up as a storage provider, the more they process, the higher score they will achieve as a storage provider.

#### **Task status:**

* <mark style="color:blue;">**Created**</mark>: Tasks are created successfully first time on Swan platform or tasks with `ActionRequired`status have been modified to fullfill the autobid qualification.
* <mark style="color:blue;">**Assigned**</mark>: Tasks have been assigned to storage providers manually by users or automatically by autobid module.
* <mark style="color:blue;">**ActionRequired**</mark>: Task with <mark style="background-color:orange;">autobid mode</mark> on, in other words,<mark style="color:yellow;">**`bid_mode`**</mark> set to <mark style="color:yellow;">**`1`**</mark> and <mark style="color:orange;">**`public_deal`**</mark> set to <mark style="color:orange;">**`true`**</mark>, have some information missing or invalid in the \[task-name.csv] can cause the failure of automatically assigning storage providers. Action are required to fill in or modify the file and then update the task information on Swan platform with the new csv file.
* <mark style="color:blue;">**DealSent**</mark>: Tasks have been sent to storage providers after tasks being assigned.

### Offline Deal

The size of an offline deal can be up to **64 GB**. It is suggested to create a CSV file contains the following information:

| uuid                                 | miner\_id | deal\_cid | payload\_cid                                                |
| ------------------------------------ | --------- | --------- | ----------------------------------------------------------- |
| 0b89e0cf-f3ec-41a3-8f1e-52b098f0c503 | f047419   | ---       | bafyreid7tw7mcwlj465dqudwanml3mueyzizezct6cm5a7g2djfxjfgxwm |

This CSV file is helpful to enhance the data consistency and rebuild the graph in the future. uuid is generated for future index purpose.
