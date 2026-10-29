---
type: entity
title: HyperLedger Fabric
created: 2026-09-30
updated: 2026-09-30
tags: [区块链, 技术框架, 许可链]
related: [sources/4-news--7-05-数字科技--4-2018--23-区块链技术在贸易融资中的应用及挑战贸易融资资讯--dcbhxl, 许可链供应链金融与核心企业主导不变论-2018口径, 区块链联盟格局2016-2017快照]
sources: ["news/05-数字科技/2018/区块链技术在贸易融资中的应用及挑战_贸易融资资讯.md"]
---

# HyperLedger Fabric

Linux 基金会主导的开源许可链（permissioned）技术框架，2016–2018 年为金融与供应链金融联盟链项目的主流选型之一（参见 [[区块链联盟格局2016-2017快照]]）。

## 核心组成（据 2018 文思海辉技术文章口径）

- **成员服务（Membership Service）**：依托 PKI 将 non-permissioned 网络转为 permissioned 网络，管理节点身份、隐私与可审计性
- **区块服务（Blockchain services）**：基于 HTTP/2 P2P 协议管理分布式账本，维护 world state 副本，共识协议可插拔（PBFT、Raft、PoW、PoS 等）
- **链码服务（Chaincode / 智能合约）**：安全轻量沙盒容器执行，base 镜像经签名验证，当时支持 Go 语言
- **事件服务**：VP 节点与链码发出 events 触发监听
- **API 与 CLI**：REST API 与命令行，用于注册、查询、发送交易与链码测试

## 在贸易融资中的应用

文思海辉 2018 年的区块链贸易融资产品以 Fabric 为基础平台，采用虚拟专有网 + 分级部署（骨干/大型/特殊成员）方案，详见来源页。
