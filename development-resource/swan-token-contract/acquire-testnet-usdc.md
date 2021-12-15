---
description: This page will show you how to obtain and add testnet USDC to MetaMask.
---

# Acquire Testnet USDC

If you already have Testnet USDC, please skip to [MCP User Guide](../../multi-chain-payment/mcp-user-guide.md) start using our multi-chain payment service.

## Testnet Swan Faucet <a href="#testnet-link-faucet" id="testnet-link-faucet"></a>

By using the [Swan faucet](https://calibration-faucet.filswan.com), you can get Testnet USDC for your account on the Polygon Mumbai.&#x20;

![](<../../.gitbook/assets/image (38).png>)

### Get USDC token from Swan faucet

* Open up MetaMask, click the Wallet account name at the top to copy the address to your clipboard.
* Paste that address into the Swan Faucet `Testnet account address` input field, and click the `Request 100 USDC` button.
* You should see a modal show up with the text 'Transaction initiated'.
* Once the transaction is confirmed on-chain, the modal will show 'Request complete', along with the transaction hash of your request.

![](<../../.gitbook/assets/image (41).png>)

{% hint style="warning" %}
**Note:** You can only use this faucet for one wallet address once every 24 hours.
{% endhint %}

### Add USDC token in MetaMask wallet

* In order to see your USDC token balance in MetaMask, you will need to add the token.
* In MetaMask click on the `Import tokens` link under the 'Assets' tab. Copy the following address:

| Parameter              | Value                                      |
| ---------------------- | ------------------------------------------ |
| Token Contract Address | 0xe11a86849d99f524cac3e7a0ec1241828e332c62 |
| Token Symbol           | USDC                                       |
| Token Decimals         | 18                                         |

* Paste the token contract address into MetaMask in the `Token Contract Address` input. The token symbol and decimals of precision will auto-populate. Click on the `Add Custom Token` button.

&#x20;                                           ![](<../../.gitbook/assets/image (39).png>)

* A new window will appear, showing the USDC token details. Click on the `Import Tokens` button.

&#x20;                                           ![](<../../.gitbook/assets/image (28).png>)

* MetaMask should now display the new USDC balance.

&#x20;                                           ![](<../../.gitbook/assets/image (35).png>)
