---
description: Auto send auto-bid mode tasks with deals to auto-bid mode storage provider
---

# Set Auto-bid Mode

The autobid system between swan-client and swan-provider allows you to automatically send deals to a miner selected by Swan platform. All miners with auto-bid mode on have the chance to be selected but only one will be chosen based on Swan reputation system and Market Matcher. You can choose to start this service before or after creating tasks in Step 3. Noted here, only tasks with `bid_mode` set to `1` and `public_deal` set to `true` will be considered. A log file will be generated afterwards.

Start the autobid module before or after creating autobid mode tasks

```
python3 swan_cli_auto.py auto --out-dir [output_file_dir]
```

or (Recommanded)

```
nohup python3 swan_cli_auto.py auto --out-dir [output_file_dir] >> auto_deal.log &
```

**--out-dir (optional):** A deal info csv containing information of deals sent and a corresponding deal final CSV with deals details will be generated to the given directory. Default: `output_dir` specified in config.toml

The output will be like:

```
INFO:root:Getting My swan tasks info
INFO:root:Swan task count 203
INFO:root:Getting Swan task status, uuid: 9c330c9-ba7-4989-b0a-7b9f26602
INFO:root:Swan task status is: {"task_uuid": "9c330c9-ba7-4989-b0a-7b9f26602", "task_status": "Assigned", "deals": [{"contract_id": "0x5210ED929B5BEdBFFBA", "created_at": "1632762298", "deal_cid": null, "file_name": null, "file_path": null, "file_size": "103125", "file_source_url": "http://192.168.88.41:5050/ipfs/QmZAiNYWX8giAYnUrZXVowtBwVktKL8meBjf", "id": 6861, "md5_origin": "", "miner_id": null, "note": null, "payload_cid": "bafk2bzacebjglrfqg3eexbntnhke2zysfmdwkfnlankhq72fca3w2c", "piece_cid": "baga6ea4seaqa2nfklf5xgom5jelt75czi3i5ynhiwm2b5w3xfs", "start_epoch": 1160167, "status": "Created", "task_id": 1596, "updated_at": "1632762298", "user_id": 184}], "task": {"bid_mode": 1, "created_on": "1632762298", "curated_dataset": null, "description": null, "expire_days": 4, "fast_retrieval": 1, "is_public": 1, "max_price": "0.050000000000000000", "min_price": null, "miner_id": "t03354", "status": "Assigned", "tags": null, "task_file_name": "test.csv", "task_id": 1596, "task_name": "2021092702", "type": "regular", "updated_on": "\ufffd", "uuid": "9c3b30c9-ba17-4989-b03a-7b9f26602036"}}
INFO:root:['lotus', 'client', 'deal', '--from', 't3u7pumush376xbytsgs5wabkhtadjzfydxxda2vzyasg7cimkcphswrq66j4dubbhwpnojqd3jie6ermpwvvq', '--start-epoch', '320167', '--fast-retrieval=true', '--verified-deal=false', '--manual-piece-cid', 'baga6ea4seaqa2nfklf5xgom5jelt75czi3i5ynhiwm2b5w3xfsp7thnkfzgnmdq', '--manual-piece-size', '130048', 'bafk2bzacebjglrfqg3eexbntnhke2zysfmdwkfnlankhq72fca3w2c2dqq5j2', 't01101, '0.000000000000000000', '1051200']
INFO:root:wallet: umush376xbyabkhtadjzfydxxda2vzyasg7cimkcphswrq66j4dubbh
INFO:root:miner: t01101
INFO:root:price: 0
INFO:root:total cost: 0.000000000000000000
INFO:root:start epoch: 320167
INFO:root:fast-retrieval: true
INFO:root:verified-deal: false
INFO:root:Deal sent, deal cid: bafyrei2yuidanaxzsp3yvypxub5worfei5tojb55fd, start epoch: 320167
INFO:root:Swan deal info CSV Generated: /tmp/tasks/[output_files_dir]/task-uuid-info.csv
INFO:root:Swan deal final CSV /tmp/tasks/[output_files_dir]/task-uuid-deals.csv
INFO:root:Refreshing token
INFO:root:Updating Swan task.
INFO:root:Swan task updated.
```

{% hint style="info" %}
A successful autobid task will go through three major status - **`Created`,`Assigned`** and **`DealSent`**. The task status **`ActionRequired`** exists only when public task with autobid mode on failed in meeting the requirements of autobid. To avoid being set to **`ActionRequired`**, a task must be created or modified to have valid tasks and corresponding deals information as following.
{% endhint %}

*   **For task**:

    **task price:** Max price willing to pay per GiB/epoch for offline deal,which can be changed in `max_price` of `config.toml`

    **task fast retrieval:** \[true/false] Indicates that data should be available for fast retrieval,which can be changed in `fast_retreval` of `config.toml`

    **task type:** \[true/false] Whether deals in the tasks are public deals, which can be changed in `fast_retreval`of `config.toml`
*   **For deals**:

    **valid deals:** There must be at least one valid corresponding deal record. Check the \[task-name.csv] to make sure of it.

    **start epoch:** Start epoch for deals in hours from current time is also needed, which can be changed in `start_epoch_hours` of `config.toml`

    **car file urls:** The valid downloading url of car files must be filled in before creating Swan tasks. Check column `car_file_url` of car.csv before sending and modify it if needed.

    **car file size:** A correct car file size should be filled in \[car.csv] after car files generation

    **payload Cid:** Also known as data cid, which should be given in \[car.csv] after car files generation.

    **piece Cid:** Piece cid is required for offline deals,which should be given in \[car.csv] after car files generation as well.
