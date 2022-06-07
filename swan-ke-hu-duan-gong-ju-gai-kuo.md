---
description: Swan
---

# Swan客户端工具概括

## 如果您想使用Swan客户端工具发单

#### Swan客户端工具提供以下功能：

* 将源文件生成Car文件（可以使用Lotus、Graph-split 或者 IPFS）；
* 生成元数据，如 Car 文件的URI, 交易开始高度(start epoch)等. 并以JSON格式保存到元数据文件;
* 使用元数据JSON文件发起交易;
* 生成包含交易CID、存储提供者ID等数据的最终JSON文件，供存储提供者导入交易;
* 在filswan平台上创建任务和离线交易;
* 自动将交易发送给参与自动竞价的存储提供者;
