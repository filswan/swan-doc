---
description: Full demo code to run python MCS SDK
---

# Full Demo Code

To use the full demo code, you will need to add your wallet info and add the `amount` and `file_path` in the following script.

```python
import os
from dotenv import load_dotenv
from mcs.upload.mcs_upload import MCSUpload

if __name__ == '__main__':
    
    # setup env and wallet
    load_dotenv(".env")

    # Load file path
    file_path = "./test.py"

    # Upload file
    upload_handle = MCSUpload("polygon.mainnet", os.getenv('wallet_address'), os.getenv('private_key'), os.getenv('rpc_endpoint'), file_path)
    file_data, need_pay = upload_handle.stream_upload()

    # Process payment
    if need_pay:
        upload_handle.approve_token(<amount>)
        upload_handle.pay()
    
    print('Upload successfully')
```
