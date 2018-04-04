# consensus 共识机制

## POW   - bitcoin

## POS   - peercoin

## DPOS  - eos
https://steemit.com/dpos/@dantheman/dpos-consensus-algorithm-this-missing-white-paper

## POOL  - fabric/hyperledge 分布式一致性算法 Pasox Raft

## DBFT  - (DPOS一种) neo

## POI   - 重要性证明 nem

## POB: Proof of Burn - 燃烧证明

## PoC: Proof of Capacity - 容量证明

## Tendermint: https://github.com/tendermint/tendermint

## POA: Proof of Authority - 权威证明 https://poa.network/

## Hashgraph

## Proof of Activity (hybrid PoW + PoS) - DeCred governenance currency

## Proof of unique identity

## PoSt: Proof-of-Spacetime: 时空证明 fileCoin

## PoRep: Proof-of-Replication: 复制证明 fileCoin

## HoneyBadgerBFT: 一个网络环境无关的Byzantine容错的分布式共识协议, 完全异步的共识协议, 支持封闭网络, 主机数量固定
https://github.com/amiller/HoneyBadgerBFT

## Notary: 公证人?

## PBFT 联盟链共识

## SCF 联盟链共识

## Ouroboros Cardano的DPos共识算法
首先是一些术语及作用的解释：
  -. 在Cardano的运行中，时间被分为 slot
  -. 每个slot只能产生一个块，若这个块有问题，或者应该产出这个块的“矿工”(也就是stakeholder的候选人)不在线，或者产出的块没有广播给大多数人，那么这个slot是当作废弃的，也就是会跳过这个slot的块。
  -. 多个slot为一个 epoch，权益的计算是以每个epoch开始前的历史来计算，也就是说在这个epoch中所产生的权益变化不影响当前的这个epoch中的slot的出块者的选择和其他和历史相关的东西。当前epoch中所产生的这些历史只能在以后的epoch中生效。
  -. 每个epoch的开头有个 genesis block(注意是每一个epoch，不是整个链)，这个genesis block 不会上链(整个链初始的那个genesis会，当然这一点可以根据实现自己决定)，而是当前这个节点(矿工)自己在内存中生成，这个genesis block会记录好当前这个epoch中的可能参与出块的 stakeholder的候选人，及一个随机种子ρ。
  -. stakeholder是权益持有者，也就是潜在矿工，在Cardano的实现中权益stake并不是直接指代有多少Ada，而是和有多少Ada相关联(更详细的我不是很清楚)，同时要成为一个stakeholder需要有2%的Ada才行。当然论文中不关注这些，直接定义了stakeholder。而stakeholder并不一定要参与出块，只有记录在每个epoch的genesis block中的stakeholder才能参与当前epoch中slot的出块，所以记录在每个epoch中的genesis block中的stakeholder叫做 “stakeholder候选人”
  -. 由这些epoch衔接而成的链就是由Ouroboros共识产生的链，这个链的基本属性和Bitcoin相同(如每个块包含上一个块的hash等等)。
  -. Slot Leader Selection 是指根据权益占比选择按概率选择出当前slot的出块者。指代的是在当前的epoch中，按genesis block 中记录的stakeholder候选人的权益分别占用的比例为这个epoch中的每一个slot选择出块者的概率(注意这个概率是独立事件，也就是有可能在同一个epoch中重复选出相同的人)。在论文中用函数
     \mathbf{F}(\mathbb{S},ρ,sl_{j}) \; \; outputs \; \; U_{i}\in {U_{1},...,U_{n}}\\ 其中\mathbb{S}表示stakeholder候选人集合,ρ表示随机种子,sl_{j}表示第j个slot,U表示出块者(slotleader)
  -. 来表示按照权益占比为概率从stakeholder候选人选出该slot的出块者U。注意在论文中只是定义了这个函数具有这样的作用，在Cardano中使用了 “follow-the-satoshi(fts)” 算法(fts具有论文中定义的这个函数的性质)来选出这个slot leader也就是出块者。
  -. secure multiparty computation (MPC) MPC协议，参与者使用一种能达成MPC的密码学协议来参与生成下一轮epoch的随机种子ρ，这个MPC协议必须是保证guarantee output delivery(G.O.D，下文会解释)。这个随机种子ρ是用于Slot Leader Selection中的。
  -. 从链的真正创世块开始，硬编码进入了一些公钥和这些公钥vk对应的权益s及初始的种子ρ，之后，这个epoch会采用这些基础信息继续运行。
  -. 每个节点自己独立运行代码，根据当前epoch的种子ρ，执行F(比如 follow-the-satoshi)，把genesisblock中的权益，ρ和slot的index作为输入，根据概率获得当前这个slot应该由谁出块。
    -. 若发现是自己出块，则执行打包交易等等操作，和bitcoin没有太大区别，但是除了基础工作之外，还会生成一个随机数，但是这个随机数不放到链(块)中，而是放一个承诺(后文解释)。
    -. 若不是自己出块，则等待出块者出块并广播。收到这个块的时候就进行和bitcoin类似的检查，要是长时间未收到(超出这个slot的时间)则会认为这个slot的块废弃。
  -. 在当前epoch中不断重复2的流程直到这个epoch中的所有slot结束。
  -. 在整个epoch的过程中会产出一个在这个epoch参与出块者们(slot leaders)都共同认同的随机种子ρ。
  -. 在自己的内存里记录好这个ρ及下一个epoch参与的stakeholders，开启下一个epoch周期，进入2的流程。
以上就是 Ouroboros 大致执行的流程
关于随机p的真随机算法。

https://zhuanlan.zhihu.com/p/33824015

## SPECTRE DAG共识算法
https://docs.wixstatic.com/ugd/242600_bc8db338d74a4cdcbf90a81ab78a7711.pdf

## PHANTOM DAG共识算法
https://docs.wixstatic.com/ugd/242600_92372943016c47ecb2e94b2fc07876d6.pdf



# 参考资料

### Polkadot 波卡链: 解耦共识组件和状态转换组件 https://polkadot.network
Tangle是个关于共识系统的概念性尝试。不把交易排序再打包到区块中，而是通过串联的共识得出一个全局的一致性状态改变排序，它在很大程度上抛弃了高度结构化的排序想法，而是推出一个有向无环图，后续的有依赖的交易通过明确的指向，来帮助前面的交易达成一致。对于任意的状态改变，这个依赖图就会很快地变得无法处理，然而对于更简单的UTXO模型，立即就变得合理了。因为系统总是松散地连贯，而且交易通常是相互独立的，大规模的全局并发变得非常自然。使用UTXO模型确实可以让Tangle定位成价值转移的货币系统，而并没有其他的更多通用和可扩展的功能。因为没有了全局依赖性，而和其他系统的交互又需要确定性地知道其状态，这种方法就变得不切实际了。
公证通（Factom）演示了个没有有效性的一致性系统，能够高效地记载数据。由于没有全局状态和其带来扩展性问题，它可以被看做是一个可伸缩的方案。然而前面也提到了，严格上来说它只解决了很少的问题。

### Tendermint Cosmos
实用拜占庭，DPos

### Factom

### Casper

### Dfinity BLS签名算法 VRF可验证随机函数算法
https://zhuanlan.zhihu.com/p/28172716

### FLP定理  https://www.cnblogs.com/javaleon/p/3945864.html
### 分布式系统理论基础 - 一致性、2PC和3PC http://www.cnblogs.com/bangerlee/p/5268485.html
