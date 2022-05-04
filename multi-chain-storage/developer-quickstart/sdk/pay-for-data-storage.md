# Pay for data storage

`makePayment(payloadCid, minAmount)`

After a file is uploaded, the file can be paid for by its payload cid. The method takes the payload cid as the first parameter and the minimum amount as the second.

```
const PAYLOAD_CID = ''
const MIN_AMOUNT = '1'
 
const tx = await client.makePayment(PAYLOAD_CID, MIN_AMOUNT)
console.log(tx.transactionHash)
```

### Parameters

* **payloadCid**: payload cid of the file
* **minAmount**: minimum amount to pay for the file. String value to avoid Big Number precision errors

### Return

Returns a web3.js receipt object. In the example above, only the transaction hash from this object is printed.
