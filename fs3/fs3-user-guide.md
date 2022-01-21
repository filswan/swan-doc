---
description: >-
  Once everything is setup, FS3 browser is ready to use. Here is the tutorial
  how to use your FS3.
---

# FS3 User Guide

## Requirements

Before you begin this guide, complete the following tasks to make sure you have all of the tools that you need:

* Make sure you meet all the [prerequisites](https://app.gitbook.com/o/-Ma7\_tf6L8A170GHT9fr/s/-MauK7Ig3eWeXC35bZV7/c/9h2HfinXKBQdRYF7ovZb/fs3/setup-your-fs3/prerequisites) before installing
* Follow the install instructions [here](setup-your-fs3/install-fs3.md) to set up your database and install from sources using Terminal/Command.

## Instruction

### 1.  Creating a bucket

To get started, you can click the red button with a plus sign on the bottom right corner. It will pop up 2 yellow icons (upload files and create buckets) by clicking the red button. Files can not be uploaded without a bucket. The first thing is to choose the "<mark style="color:blue;">**Create buckets**</mark>" button in yellow, name it and press Enter/Return key to confirm.&#x20;

![](../.gitbook/assets/WechatIMG284.jpeg)

### 2. Loading files

Within a bucket, you can upload your files by choosing the "<mark style="color:blue;">**Upload files**</mark>" button in yellow which is right above the "create bucket" button. Same as before, to appear the "upload files" button, you need to click the red button with the plus sign on it.&#x20;

![](../.gitbook/assets/WeChat5cf513347fdac1e75f21ab1c684bb5e1.png)

### 3. Single file operations

Once your file is uploaded on FS3, you will see three dots on the right side of the file. The operations to the file including "<mark style="color:blue;">**Delete object**</mark>", "<mark style="color:blue;">**Share objec**</mark>t", "<mark style="color:blue;">**Backup to Filecoin**</mark>" and <mark style="color:blue;">**Download object**</mark>".&#x20;

![](<../.gitbook/assets/chrome-capture (1) (1) (1).gif>)

#### Backup to Filecoin (Online Deals)

There are 2 ways to choose your preferred storage provider.&#x20;

If you have a specific storage provider you want to work with, and you have the provider ID number, you can just simply fill it directly into the provider ID input field.&#x20;

If this is your first time to backup or you do not have anyone on your mind at the moment, you can choose your storage provider based on the list we provide for you.&#x20;

After choosing your provider, filling out offered price and setting up duration for the storage, you can click "<mark style="color:green;">**Send**</mark>" **** button" in green to send the request. You should get a list number of "<mark style="color:blue;">**Deal CID**</mark>" if your deal is sent successfully.&#x20;

### 4. Bucket operations

The bucket-level operations on FS3 including "<mark style="color:blue;">**Delete**</mark>" bucket, "<mark style="color:blue;">**Retrieval**</mark>" and "<mark style="color:blue;">**Backup to Filecoin**</mark>". By clicking the three dots in vertical next to the bucket, you should be able to see these options.

#### Backup to Filecoin(Online bucket-deals)

To backup a whole bucket to Filecoin, the proceure is same as single file backup. You can choose your storage provider either by filling a specific provider ID or selecting from our provided list. You also need to fill the price input field and the duration input field. After clicking the "<mark style="color:green;">**Send**</mark>" **** button" in green to send the request, you should get a list number of "<mark style="color:blue;">**Deal CID**</mark>" when your deal is sent successfully.&#x20;

![](<../.gitbook/assets/chrome-capture (2).gif>)

### 5. Backup plan

Users can backup the entire volume with customized schedulers (<mark style="color:blue;">**Backup Daily**</mark>/ <mark style="color:blue;">**Backup Weekly**</mark>) to Filecoin Network.&#x20;

* Create a backup plan by choosing "<mark style="color:blue;">**Backup Plans**</mark>" page.&#x20;

{% hint style="info" %}
**Price**: It is valued as GiB/epoch

**Duration**: Duration for keeping the backup needs to be in the range of 180 to 540.&#x20;
{% endhint %}

* You can view your created backup plans on "<mark style="color:blue;">**Backup Plans**</mark>" page.
* As soon as the creation is complete, FS3 is sending volume backup task to the assigned storage provider automatically using FilSwan [**Autobid**](https://docs.filswan.com/filswan-platform/overview/filswan-auction-system) **** module (click Autobid to know how it works).&#x20;
* If you choose to backup daily,  FS3 will compress the entire data volume into a car. file and upload it to the Filecoin Network every 24 hours. You can check all your backup jobs by choosing "<mark style="color:blue;">**Jobs**</mark>" page, and here shows you all the information about your jobs.
* Once the backup process has completed, the status under backup jobs on the "<mark style="color:blue;">**Jobs**</mark>" page will change from "<mark style="color:yellow;">**Running**</mark>" to "<mark style="color:green;">**Completed**</mark>".

### 6. Rebuild backup volume&#x20;

{% hint style="warning" %}
Rebuild image is accessible **only** when bakup job status is **completed**. Users can not rebuild image when backup process is still running.
{% endhint %}

To store your entire FS3 instance from one of your backups, you can use the FS3 "<mark style="color:blue;">**Rebuild Image**</mark>" service. FS3 will fetch a entire backup from Filecoin Network and overwrite your existing system.&#x20;

![](<../.gitbook/assets/2861639177168\_.pic copy.jpg>)

* &#x20;First, go to "<mark style="color:blue;">**Jobs**</mark>" page and all your backup jobs are listed here.
* &#x20;Second, make sure you are under "<mark style="color:blue;">**backup jobs**</mark>" for rebuilding an image (restore a backup). You can switch to rebuild jobs next to the backup jobs to view all your rebuild history.
* Third, on the very right side of each jobs, you should be able to click "<mark style="color:blue;">**Rebuild Image**</mark>" when the status is "<mark style="color:green;">**Completed**</mark>".
* Next, after clicking "<mark style="color:blue;">**Rebuild Image**</mark>", a pop up window will show as above. Please check your information and make sure you are rebuilding from the correct backup. Your backup name will show in bold font, as circled in blue.&#x20;
* Finally, choose "<mark style="color:green;">**OK**</mark>" to confirm your rebuild process and choose "**Cancel**" to quit from rebuilding backup.&#x20;
