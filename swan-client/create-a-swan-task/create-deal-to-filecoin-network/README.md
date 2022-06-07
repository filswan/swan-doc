# Create Deal to Filecoin Network

### Flowchart

#### Option1️⃣ Manual-bid Mode

* **Conditions:** `[sender].bid_mode=0`, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

![](<../../../.gitbook/assets/manual bid1.svg>)

* Only `Created` status exists for both task and car file

#### Option2️⃣ Auto-bid Mode

* **Conditions:** `[sender].bid_mode=1`, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

![](<../../../.gitbook/assets/auto bid.svg>)

* If a task does not match auto-bid conditions, its status will be changed from `Created` to `Action Required`
* If a car file does not match auto-bid conditions, its status will be changed from `Created` to `Action Required`
* If both a car file and its task match auto-bid conditions
  * Miners that match the task and car file requirements will be assigned to car files
  * The max number of allocated miners depends on `max_auto_bid_copy_number`, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
  * If there are miners allocated to a car file, its status will be changed to `Assigned` and task's status remains at `Created`
  * If there is no miner meets the car file's and its task's requirements, then their status remain at `Created`

#### Option3️⃣ None-bid Mode

* **Conditions:** `[sender].bid_mode=2`, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

![](<../../../.gitbook/assets/non bid.svg>)

* In this option, deal(s) will be sent when creating a task.
* Only `Created` status exists for both task and car file
