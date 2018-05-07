### 以太坊的分片技术
[官方资料](https://github.com/ethereum/wiki/wiki/Sharding-introduction-R&D-compendium)

##### 目标
1. Scaling: 可伸缩性，即性能能够达到VISA水平，千级TPS
2. 可用性：
   - 跨智能合约交易
   - 跨片交易
3. 紧耦合

##### Collation——校对数据结构
Collation Header
- shard_id: the Shard ID of shards, most like a network-id, from 0~N-1(N is shard number).
- parent_hash: the hash of parent collation.
- chunk_root: 类似于默克尔树root的一个字段，是对body里面的chunks的root.
- period（周期）: 进行校对的周期. (主链上五个区块算一个周期)
- proposer_bid: 该collation的提案人的地址.
- proposer_signature: 提案人的签名.

Collation Body
- chunks: list-chunks

#### 整体概览
两层和三个步骤：
- 第一层
  - 提案人(Proposer)收集交易放入到Collations中
  - 校对人(Collator校对
    - a: 链接Collations
    - b: 同意规范链
- 第二层
  - 执行人(Executor)
    - a: 处理交易
    - b: 执行智能合约
    - c: 计算状态

##### Proposer
1. 任何人都可以成为Proposer
2. 运行管理一个交易池
3. 收集所有的交易进行打包
4. 发送和接收Collation Body

##### Collator
1. 被伪随机抽样为来自所有碎片的整理池的“特定碎片和特定时期”的合格的整理者
2. 整理提案来构建排序规则

##### Executor
1. 执行状态转换功能
2. 提议者最好也应该是执行者，这样可以知道交易的消耗的gas，并选择费用高的交易

#### Sharding Manager Contract（SMC）
![SMC Architecture](../static/smc_architecture.png)


#### 执行流程
1. 验证者通过查看LOOKHEAD, 就是先前的区块链信息去判别接下来的验证者身份
2. 普通用户提交交易到proposer
3. proposer打包出collations并分一些gas去给验证者
4. 验证者传输接收潜在的collations
5. 验证验证直到一定的深度的片段
6. 验证者提交所验证的片段的深度给root chain
7. 恶意的验证者会提交一个非法的collation
8. 下一阶段的验证将在此分叉处处理这个非法的collation, 选取前一个合法的collation提交给root chain

#### 分片方案与现有架构的整合图
![Eth_Sharding Architecture](../static/eth_sharding_architecture.png)
