---
description: GuideTutorial
---

# User Guide

### Requirements <a href="#requirements" id="requirements"></a>

Before you begin this guide, complete the following tasks to make sure you have all of the tools that you need:

* Complete the [Beginner Walkthrough](../getting-started/beginner-walkthrough/) to obtain Testnet USDC and set up MetaMask.
* You can obtain test _MATIC_ from several[ faucets.](../development-resource/swan-token-contracts.md)

MCP use both matic and usdc for uploading files to polygon network. We storongly suggest you testing with testnet first.

## **Instruction**

### **1. Login your account**

Sign up and login to [MCP website](https://calibration-mcp.filswan.com). (Swan registered users can directly use your **** Swan account without registering MCP account separately)

![](<../.gitbook/assets/image (30).png>)

### **2. Connect to your MetaMask wallet on Mumbai Testnet**

Connect your MetaMask wallet, and make sure to select the corresponding network on the MetaMask wallet. (Currently, we only support the Polygon Mumbai Testnet. In the future, it will be officially launched into the Polygon Mainnet. And we also planned to add other main networks such as Ethereum, BSC, Fantom, etc.)

![    ](<../.gitbook/assets/chrome-capture (3).gif>)

### 3. Upload file **to IPFS**

* Choose the file you would like to backup to Filecoin Network. The file name and file size will be displayed below upload button.
* Set a duration which refers to the terms in which you want the file to be stored on the Filecoin network. _The default value will be 365 days._&#x20;
* An estimated storage cost will be calculated according to the file size, the duration you set, and the average provider price.
* Based on the real-time DeFi exchange rate which got from Sushi Swap, three lock funds plans are provided to our users. The more funds are locked, the sooner your file will be stored on the Filecoin network. Any overpaid funds will be automatically refunded to users after the deal is on chain and contract collects enough DAO signatures.

![](<../.gitbook/assets/image (46).png>)

After Submitting your request, an uploading window will show up. Uploading time varies depends on the size of your file. Please keep the window open until uploading completes.

![](<../.gitbook/assets/chrome-capture (4).gif>)

### **4. Lock fund with MetaMask**

After the file has been successfully uploaded to IPFS, the next step is Lock funds to the smart contract, using the currency we support. For now, it is 'USDC' token.

Waiting time varies depends on the blockchain congestion.

![](<../.gitbook/assets/chrome-capture (5).gif>)

While the payment is completed, a pop-up window with the transaction link shows up. You can either click the link or check your MetaMask activity to see the transaction at the block explorer.

![](<../.gitbook/assets/image (45).png>)

{% hint style="info" %}
**TIPS:** If you changed your mind and wanted to select another plan?

No worries, as long as you didn't confirm your payment on MetaMask. Firstly, you need to reject the transaction on MetaMask. Then, go to the 'My Files' page, you will find a PAY button to the corresponding file. By clicking the PAY button, you can also complete your payment.
{% endhint %}

### **5. View your files.**

By clicking the 'Close' button, it will automatically turn to 'My Files' page.

In this page, you can find all the files you have uploaded. It provides you some frequently used informations, such as the file name, status, data cid, provider id, and payment button, etc.&#x20;

{% hint style="info" %}
**TIPS:** With the mouse is hovering over the provider id, it shows you the real-time deal status from blockchain.
{% endhint %}

{% hint style="success" %}
**GOOD TO KNOW:** In order to improve the efficiency, MCP system is using FilSwan's AutoBid function. A qualified and optimal provider will be automatically assigned to your deal. The storage provider will complete following backup procedure, and synchronize the 'Deal status' to our platform.
{% endhint %}

![](<../.gitbook/assets/image (34).png>)

To view more details, simply click on the **file name**. You can find all the related information on this page, including the IPFS download link, the retrieval from Filecoin Network command, and DAO signature information and status. You won't need to bother to check the deal with a blockchain explorer.:smile:

![](<../.gitbook/assets/chrome-capture (6).gif>)

#### DAO Signature Process:

* When the user's deal is successfully published on blockchain, the deal will be scanned by the DAO organization.&#x20;
* Then, DAO members will sign to agree to unlock the user's funds.&#x20;
* If a specified number of signatures from DAO are collected, the smart contract will unlock the funds.&#x20;
* Part of the locked funds will be used to pay the storage fee, and the remaining will be refunded to user's wallet.

{% hint style="info" %}
**NOTE:** An expire date is set while locking fund, the default is 6 days. If the storage task failed within 6 days, the locked funds in the smart contract will be directly refunded to users in full.
{% endhint %}

### 6. Billing History

Users can view the billing history of all deals in 'Billing history' page. It covers all the information about the order such as the transaction hash, amount, unlock amount, token, data CID, wallet address, etc.

![](<../.gitbook/assets/image (29) (1).png>)
