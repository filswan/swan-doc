---
description: GuideTutorial
---

# Tutorial

_This tutorial assumes you have already downloaded MetaMask, and that you have MATIC and USDC token in that wallet on the Mumbai Testnet. If you don’t have a wallet, visit our portal _[_here_](developer-quickstart/public-testnet/setup-metamask.md)_ to download one._

**Disclaimer: MATIC is the gas for MCP. You need MATIC to make transactions on Mumbai.**



## **Instruction**

### **1. Login your account**

![](<../.gitbook/assets/image (45).png>)

### **2. Connect to your MetaMask wallet on Mumbai Testnet**

![](<../.gitbook/assets/image (42).png>)

&#x20;            ![](<../.gitbook/assets/image (40).png>)    ![](<../.gitbook/assets/image (31).png>)

### 3. Upload file** to IPFS**

* Choose the file you would like to backup to Filecoin Network. The file name and file size will display under upload button.
* Set a duration which refers to the terms in which you want the file to be stored on the Filecoin network.
* An estimated storage cost will be calculated according to your file size, the duration you set, and the average provider price.
* Based on the real-time Defi exchange rate which got from SUSHI, three lock funds plans are provided for our users. The more funds locked, the sooner your file will be stored on the Filecoin network. Any overpaid funds will be returned automatically after the deal is on chain.

![](<../.gitbook/assets/image (43).png>)

After Submitting your request, an uploading notice window will show up. Uploading time varies depends on the file size. Please keep the window open until uploading completes.

![](<../.gitbook/assets/image (32).png>)

### **4. Lock fund with MetaMask**

After the file has been successfully uploaded to IPFS, the next step is Lock fund to the smart contract, using the currencies we support 'USDC'.&#x20;

Waiting time varies depends on the blockchain congestion.&#x20;

![](<../.gitbook/assets/image (33).png>)

![](<../.gitbook/assets/image (35).png>)

While the payment is completed, a pop-up window with the transaction link shows up. You can either click the clink or check your MetaMask activity to see the transaction at the block explorer.

![](<../.gitbook/assets/image (38).png>)

### **5. View your files.**

By clicking the 'Close' button, the page will go to the 'My Files' page.

In the back end, MCP scans the events of all the transactions. In order to improve the efficiency, MCP is using FilSwan's AutoBid function, a qualified and optimal provider will be automatically assigned to your file. The storage provider will complete the following backup procedure, and synchronize the 'Deal status' to our platform. Users can check the status of the order in real time and pay attention to its changes.

![](<../.gitbook/assets/image (28).png>)

When the user's storage deal is successfully completed, it will be scanned by the DAO organization, and then DAO signed to agree to unlock the user's payment. If a specified number of signatures from DAO are collected, MCP will unlock the fund from the smart contract. The locked amount will be used to pay the storage fee of the storage service provider, and refund the remaining locked virtual currency to your wallet.

Note: an expire date is set while locking fund, the default is 6 days. If the storage task fails within 6 days, the deposit in the smart contract will be directly refunded in full. The specific conditions and methods of return will be disclosed later.

### 6. Billing History

After the order is completed, the user can view the history of all orders in "Billing history", covering all the information about the order such as the currency, amount, final unlock amount, CID, wallet address and payment time of all previous orders.

![](<../.gitbook/assets/image (36).png>)
