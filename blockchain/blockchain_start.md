### 区块链底层技术入门指北
区块链开发分为上层应用层开发和底层基础开发。

上层应用层开发主要集中在智能合约编写和RPC接口调用。
- 智能合约（DAPP）
  - 主要关于运用[Solidity Language](http://solidity.readthedocs.io/en/latest/index.html)的以太坊生态系统
  - 主要采取WASM的虚拟机生态系统，包括EOS等
- RPC接口调用 （钱包，区块浏览器）
  - 传统后端技能
  - 区块链节点部署能力
- FORK型区块链
  - 编程语言
  - 学会更改基本的创世区块或者辨识标识
  - 学会更改P2P系统的相关配置
- 区块链行业应用开发
  - 智能合约开发
  - 区块链框架的使用搭配和简单的配置

区块链底层基础开发主要分为四大模块：身份与验证模块（密码学相关），P2P网络和RPC网络交互模块，存储模块，共识模块。

#### 前期预备学习资料
##### 比特币系列
1. 白皮书: [原文](https://bitcoin.org/bitcoin.pdf), [中文](http://www.8btc.com/wiki/bitcoin-a-peer-to-peer-electronic-cash-system)
2. [源码地址](https://github.com/bitcoin/bitcoin)
3. Mastering Bitcoin书籍: [原文第二版-好](https://github.com/bitcoinbook/bitcoinbook), [中文](http://book.8btc.com/books/6/masterbitcoin2cn/_book/)
4. [社区](https://bitcointalk.org/)

##### 以太坊系列
1. [Ethereum Wiki (whitepaper, yellowpaper)](https://github.com/ethereum/wiki/wiki)
2. [Develop Framework](https://github.com/trufflesuite/truffle)
3. [Best Practices](https://consensys.github.io/smart-contract-best-practices/)
4. [中文](https://github.com/ConsenSys/smart-contract-best-practices/blob/master/README-zh.md)
5. [Resource Awesome](https://github.com/Scanate/EthList)

#### 后期强化底层知识
##### 共识算法系列
1. BFT
2. PoW
3. PoS(DPoS)
4. 密码学相关

##### P2P系列


##### 存储系列


##### 密码学系统


#### 真实项目源码参考


#### 标准代码组织结构
- src/main/{name} => 启动文件主目录
- consensus => 共识算法
- chain => 区块与交易结构
- verification => 验证机制
- witness/miner => 见证和打包机制
- network => 网络模块
- p2p => p2p网络以及穿透
- rpc => rpc接口
- sync => 同步模块
- db => 数据库交互
- storage => 存储机制
- account => 账户体系
- crypto  => 加密模块
- serialization => 序列化模块
- serialization_derive => 序列化派生
- logs => 日志
- tools => 工具
- primitives => 参数
- test-data => 测试数据
- bencher => 基准测试
- doc => 文档
