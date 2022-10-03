# 3.向Filecoin 网络发送交易

#### 选项1️⃣ 手动竞标模式 <a href="#xuan-xiang-one-shou-dong-jing-biao-mo-shi" id="xuan-xiang-one-shou-dong-jing-biao-mo-shi"></a>

* **前提条件:** `[sender].bid_mode=0`, 参见 Configuration\


![](<../../.gitbook/assets/manual bid1.svg>)

* 任务和Car文件的状态只有`Created`。

#### 选项2️⃣ 自动竞标模式 <a href="#xuan-xiang-two-zi-dong-jing-biao-mo-shi" id="xuan-xiang-two-zi-dong-jing-biao-mo-shi"></a>

* **前提条件:** `[sender].bid_mode=1`, 参见 Configuration\


![](<../../.gitbook/assets/auto bid (1).svg>)

* 如果一个任务不符合自动竞价条件，它的状态将从`Created`更改为`ActionRequired`。
* 如果一个Car文件与自动竞价条件不匹配，它的状态将从`Created`更改为`ActionRequired`。
* 如果Car文件及其任务与自动竞价条件都匹配
  * Car文件将会被分配给任务和Car文件都匹配的矿工
  * 所分配的矿工的最大数量取决于`max_auto_bid_copy_number`, 参见 Configuration
  * 如果有矿工分配到一个Car文件，它的状态将被更改为`Assigned` 任务的状态仍然是 `Created`
  * 如果没有矿工满足Car文件及其任务的要求，则它们的状态保持为 `Created`

#### 选项3️⃣ 非竞价模式 <a href="#xuan-xiang-three-fei-jing-jia-mo-shi" id="xuan-xiang-three-fei-jing-jia-mo-shi"></a>

* **前提条件:** `[sender].bid_mode=2`, 参见 Configuration\


![](<../../.gitbook/assets/non bid.svg>)

* 在这个选项中，任务将在创建任务时发送。
* 任务和Car文件的状态只有`Created`。
