### Algorand: 可扩展的拜占庭协议
##### 三种挑战
1. Sybil女巫攻击拜占庭协议
2. 适用百万级别用户
3. 弹性应对拒绝服务攻击和持续稳定服务

##### 应对方式
1. Weight users: 有效用户。（节点需要余额）
2. Consensus by committee: 共识委员会。（随机选举：影响因素：Weight），面临选举人被攻击的问题。
3. Cryptographic sortition: 密码学抽签。隐秘而且无交互的选举。用户自己在本地执行VRF算法，确认自己是否被选举上。通过自己的私钥和公共信息。如果被选举上，会生成一个简短的字符串来证明。当自己打包好信息之后，只要向别人广播的时候，带上这个字符串，别人就可以验证是否真的被选举上了。
4. Participant replacement: 参与者变更。不保留任何私人状态（不受任何私人信息控制），达到每次都会变更委员会成员。

#### 目标和假设
1. Safety goal. 安全目标。诚实会接受诚实的。Eclipse attack(日蚀攻击)。
2. Liveness goal. 活跃目标。
3. Assumptions. 一般常见的假设。

强同步与弱同步，强同步可以解决活跃的目标。弱同步结果安全目标。所有用户之间有弱同步的时钟，保证相差不大。

#### 总览和思路
区块组织形式与比特币类似，使用Gossip协议去传输交易。BA提供了两种共识: final共识与tentative共识。final共识意味着这个区块已经达成了最终的共识，被稳定确认了，后续区块可以接着此区块继续连接下去。tentative共识意味着这个区块，有人能够看到同轮的其他区块。这个区块上的所有交易都处于未确认的状态。Gossip协议来传输新产生的交易与区块。区块提案产生区块生成者们。BA协议确定最终的区块。

#### 密码学抽签 Cryptographic Sortition
VRF函数保证选举的本地执行和不用交互，参数包括（该轮的随机种子，自身的私钥，Weight信息）-> (hash, proof, J)证明信息。首先会确定角色：打包者和委员会成员。十分重要的一点就是需要有余额用于Weight证明。一个用户会被选举上超过一次，所以有了一个参数J，用于记录被选举的次数。也就是有了'sub-user'这个概念。验证的时候，带入公钥，hash等信息，就可以得到J，算出这个用户是否被选中。

其次是种子(seed)生成算法。r轮中的seed是在r-1轮基础上生成的。如果r-1轮没有生效seed, 则通过计算所有打包区块确认这轮的seed。seed为了防止被攻击者影响，会在R轮之后，重新刷新一次，执行一个mod算法。

如何在弱同步的网络中，防止用户执行empty block（上一块区块无效）算法。在计算r轮的时候，所有用户都会去计算r-1-(r mod R)的时间戳，通过对比上次区块的时间戳。

#### 区块提案 Block Proposal
sortition threshold 抽签阀值, 大于1，测算出来的是26最好。是否意味着每轮打包者的数量应该控制在26左右?
区块传输的最小化。根据候选区块的优先级传输。没轮的等待时间是一个固定的数。从收到上一轮的区块开始计算时间。

#### BA
两个实现阶段。一个是在两个候选区块中选择其中一个，另外一个是在有效无效区块中达成一致。这两个动作都是有交互的步骤的。第一阶段包括两个步骤，第二阶段如果最佳候选节点是诚实的，则需要两步，如果不是诚实的则需要11步。在每一步中，委员会成员都会进行投票。当投票结果超过某一个阀值之后，该结果就作为下一步的条件。

主要的步骤。就是确认这个区块是否是最终定型的区块，还是候选区块。为了高效，投票都是针对区块hash进行的，而不是区块内容。如果最终没有得到想要的结果BlockOfHash的结果，就需要与其他用户通信确认。算法形式：

```
procedure BA*(ctx, round, block): //ctx当前区块链的状态（包括seed, user weight, 最后的确认区块），round轮数，block是得分最高的候选区块
hblock <- Reduction(ctx, round, H(block))
hblock* <- BinaryBA*(ctx, round, hblock)
r <- CountVotes(ctx, round, FINAL, T_final, t_final, x_step)
if hblock* = r then
    return FINAL, BlockOfHash(hblock*)
else
    return TENTATIVE, BlockOfHash(hblock*)

```

投票机制。委员会成员执行。为了检验这个用户是否是委员会的一员。第一步是发送投票，就是说这个委员会成员被选中了，发送一个自己签名的信息，在信息里面包含一些区块信息，用以绑定内容， 包含自身状态下的最先前的一个区块。

```
procedire CommiteeVote(ctx, round, setp, t, value):
role <- ("committee", round, step)
sorthash, x, j <- Sortition(user.sk, ctx, seed, t, role, ctx.weight[user.pk], ctx.W)
if j > 0 then
    Gossip(user.pk, Signed(round, step, sorthash, x, H(ctx.last_block), value))

```

统计投票信息。分为统计投票和处理投票信息。

```
procedure CountVotes(ctx, round, step, T, t, x):
start <- Time()
counts <- {} //hash table, new keys mapped to 0
voters <- {}
msgs <- incomingMsgs[round, step].iterator()
while True do
    m <- msgs.next()
    if m = Null then
        if Time() > start + x then return TIMEOUT
    else
        votes, value, sorthash < PorcessMsg(ctx, t, m)
        if pk in votes or votes = 0 then continue
        voters += {pk}
        counts[value] += votes
        if counts[value] > T * t then
            return value

procedure ProcessMsg(ctx, t, m):
pk, signed_m <- m
if verifySignature(pk, signed_m) != OK then
    return 0, 0, Null
round, step, sorthash, x, hprev, value <- signed_m
if hprev != H(ctx.last_block) then return 0, Null, Null
votes <- VerifySort(pk, sorthash, x, ctx.seed, t, ("committee, round, step"), ctx.weight[pk], ctx.W)
return votes, value, sorthash

```

还原步骤。对于这是一个有效区块，还是一个无效（空）区块达成共识。对于区块链的活跃(liveness)是十分重要的部分。

#### Algorand 区块链



#### VRF应对双花攻击





### 密码抽签 cryptographic sortition
#### 选出验证者和领导者
假设在第r轮（可以理解为产生第r个区块的时间段）开始时，“种子”参数为Qr-1（表现为一个由0和1组成的长度为256的字符串），PKr-k是第r-k轮结束后系统中活跃的用户/公钥（活跃的标志是至少参与过一笔交易）的集合，其中k被称为回溯参数或安全参数。Qr-1和PKr-k属于公共知识（common knowledge）。

凭证的定义。对每一个PKr-k中的用户i，他使用自己的私钥对“种子”参数Qr-1进行电子签名后（用函数SIGi来表示）并输入哈希函数（用函数H来表示），得到自己的凭证H（SIGi(r,1,Qr-1))(函数SIGi有多个输入参数时，表示将这些参数简单串联后再进行电子签名，下同）。哈希函数的性质决定了：

1.凭证是一个近乎随机的、由0和1组成的长度为256的字符串，并且不同用户的凭证几乎不可能相同；

2.由凭证构建的2进制小数0.H(SIGi(r,1,Qr-1))（也就是将凭证字符串写到小数点后）在0和1之间均匀分布。

“潜在领导者”的选择。对0和1之间的一个数p，0.H(SIGi(r,1,Qr-1))≤p发生的概率为p，称所有满足此条件的用户为“潜在领导者”（也是这一步的“验证者”）。p使得以1-10-18的概率，在所有“潜在领导者”中，至少有一个是诚实的。

“领导者”的选择。在所有“潜在领导者”中，存在一个用户lr，其凭证按字典排序最小。也就是，对所有0.H(SIGi(r,1,Qr-1))≤p的用户i，均有H(SIGlr(r,1,Qr-1))≤H(SIGi(r,1,Qr-1))。用户lr就是第r轮的“领导者”。

“验证者”的选择。第r轮第s步（s>1）的“验证者”的产生程序与上文类似。在这一步中，每一个PKr-k中的用户i使用自己的私钥对“种子”参数Qr-1进行电子签名后并输入哈希函数，得到自己的凭证H(SIGi(r,1,Qr-1))。对0和1之间的一个数p，满足0.H(SIGi(r,1,Qr-1))≤p的用户就构成这一步的“验证者”。

#### 创建并不断完善种子参数
用Br表示第r轮结束后，拜占庭协议BA★输出的区块。如果Algorand在第r轮受到了“敌对者”攻击，Br可能是空的，也就是不含有任何真实交易记录（用符号来表示）。比如，“敌对者”可能腐化了这一轮的“领导者”，使其将两个不同的候选区块发给诚实的“验证者”。考虑到这个情况，“种子”参数的更新过程是：

Qr=H(SIGlr(Qr-1，r)),如果Br不是空区块

Qr=H（Qr-1，r）,如果Br是空区块

哈希函数的性质决定了，Qr和Qr-1之间的关系近乎随机的。回溯参数或安全参数k则保证了，“敌对者”在第r-k-1轮几乎不可能预测到Qr-1；否则，他将在第r-k轮引入恶意用户（也就是进入PKr-k），从而能影响第r轮“领导者”和“验证者”的选择。

