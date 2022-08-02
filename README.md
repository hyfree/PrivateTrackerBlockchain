# PrivateTrackerBlockchain


## 是什么

首先，PrivateTrackerBlockchain（以下简称PTB）是一个简单的基于PBFT共识机制运行的区块链网络。它的主要目的用于展示区块链技术(研究和学习用途)，而非用于生产环境（商业用途）。

因此PTB总是假设自己运行在理想世界中，不存在现实世界中的诸多问题（网络延迟、网络波动、NAT问题、信任问题、节点频繁离线等）。

从理想世界的假设出发，我们降低了区块链网络和文件分享网络的设计复杂性，从而可以用一个比较简单的代码来实现我们预期的效果（演示效果）。

## 定义

PTB是一个去中心化的区块链账本驱动的BitTorrent 网络，使用区块链账本记录每个使用者对网络的贡献，从而推动文件分享网络的良性发展。


## 前提概要

### BitTorrent 

美国工程师 Bram Cohen 在 2001 年发布了 BitTorrent 协议，资源不再由一个人或一个中心服务器提供，而是所有人提供给所有人，下载的人越多，速度越快。这种模式也叫 peer-to-peer（用户群对用户群），也就是我们常说的 P2P 下载。

性质如下：

1.  它是*无中心服务器*的对等网络系统，而上文说的C/S模式是有中心服务器的中央网络系统
2.  对等网络的每个用户端既是一个节点，也有服务器的功能。所以*用户即可以下载文件也可以上传文件*给别人
3.  所以它叫用户群对用户群（peer-to-peer）模式。用户越多，*下载同一文件的人越多，下载该文件的速度就越快*

### BitTorrent 存在的问题

我们会构造一个P2P网络用于全速传输文件，但是遗憾的是由于BT 或者是 P2P 一切全靠自愿，这自然也少不了自私的人，也用可能是某些流氓吸血软件导致的或者是其他原因（就如我上面说的几点）。这网络上提供资源的人变少，索取的变多，导致整个网络变慢，偏离了人人为我，我为人人的精神。

## 我们的目标

### 概要

1.  我们将设计一个区块链网络来记录每个peer节点的共享，每个节点通过上传流量来获得积分，每上传1MB获得1个积分。同时，每个节点从网络下载1MB文件就会消耗1个积分。
2.  每隔一段时间，进行一次选举。通过选举选出在该时间范围获取积分最多并且符合条件的节点作为共识节点，共识节点的数量最多为32。这个数量与整个区块链中的节点的总共的数量有关。
3.  持有文件的peer节点称为提供者peer-A，下载文件的节点称为下载者peer-B。
4.  B从A下载1GB大小的文件，需要A和B都提供1GB的积分作为押金存到区块链网络
5.  下载完成后，A获得2GB积分。同时，抽取0.1%的作为手续费提供给共识节点。
6.  共识需要至少2/3的节点的认可。
7.  B在下载完成后，通过花费一定的手续费，可以通过注册功能将这个文件信息和自己的网络地址保存到区块链账本。
8.  任意peer节点通过花费一定份额的手续费，可以检举一份文件。共识成功后，文件的提供者将被处于高额罚金，如果罚金高于peer节点的余额，peer节点将被TK（踢出区块链网络），文件的检举者peer节点将会获得奖励，该文件的哈希将被登记到区块链账本的黑名单。
9.  任意节点可以通过区块链账本检索自己感兴趣的内容。
10.  任意节点可以通过支付费用从其他节点下载最新的账本文件。
11.  任意节点peer-everyone可以通过支付费用邀请区块链网络外的一个节点peer-guest节点加入区块链账本
12.  如果peer-guest在一定时间内被罚款或TK，邀请者peer-everyone将被处于被TK对象的1/2的罚款。如果被邀请者peer-everyone的余额不满足，peer-everyone将被TK。

### 特性

- [ ] 实现PBFT共识
- [ ] 实现POW共识，挑选超级节点
- [ ] 链式账本和分布式账本
- [ ] NAT穿越
- [ ] 使用区块链记录资源
- [ ] 使用共识算法均衡网络中的文件资源
- [ ] 卖家登记自己的资源
- [ ] 买家买入需要的资源
- [ ] 交易结算
- [ ] 通过共识机制邀请其他节点加入网络
- [ ] 通过共识机制剔除某个不合法的节点
- [ ] 通过共识机制排除网络上不合法的资源

