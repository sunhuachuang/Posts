## 4. THE SPECTRE PROTOCOL
### A. The generation of the block DAG
As in Bitcoin, participating nodes (called miners) create blocks of transactions by solving PoW puzzles. A block specifies its direct predecessors by referencing their ID in its header (a block’s ID is obtained by applying a collision resistant hash to its header); we will describe in the next subsection how these predecessors are chosen. This results in a structure of a direct acyclic graph (DAG)  of  blocks  (as  blocks  can  only  reference  blocks  created  before  them),  denoted  typically G = (C,E). Here, C represents blocks and E represents the hash references. We will frequently write z ∈ G instead of z ∈ C.
和比特币一样，参与节点（称为矿工）通过解决PoW谜题来创建交易块。 一个块通过在其头中引用它们的ID来指定它的直接前辈（一个块的ID是通过对其头部应用抗冲突散列来获得的）; 我们将在下一小节描述如何选择这些前辈。 这导致块的直接无环图（DAG）的结构（因为块只能参考在它们之前创建的块），通常表示为G =（C，E）。 这里，C表示块，E表示散列引用。 我们将频繁地写z∈G而不是z∈C。

past(z,G) ⊂ C denotes the subset of blocks reachable from z, and similarly future(z,G)⊂ C denotes the subset of blocks from which z is reachable; these are blocks that were provably created before and after z, correspondingly. Note that an edge in the DAG points back in time, from  the  new  block  to  previously created blocks which it extends. A node does not consider a block as valid until it receives its entire past set. We denote by cone(z,G) the set of blocks that the DAG directly orders with respect to z: cone(z,G) := past (z,G) ∪ {z} ∪ future (z,G), and by anticone (z) the  complementary  of cone (z,G).  The  set past (b,G) is  fixed  once  and  for all at the creation of b (in sharp contrast to future (z,G) and anticone (z,G) that may grow as blocks are added later to the DAG), hence we can simply write past (b) without noting the context.
past（z，G）C表示可从z到达的块的子集，并且类似地future（z，G）C表示可从其中z到达的块的子集; 这些是相应地在z之前和之后创建的块。 请注意，DAG中的一条边从时间上指向新块，以及之前创建的块。 一个节点在接收到过去的整个集合之前不会将其视为有效。 我们用锥（z，G）表示DAG关于z直接排序的块集合：cone（z，G）：= past（z，G）∪{z}∪future（z，G）和 通过anticone（z）锥（z，G）的互补。 （b，G）在创建b时一劳永逸地固定（与将来添加到DAG中的块可能增长的未来（z，G）和anticone（z，G）形成鲜明对比）， 因此我们可以简单地写下过去的（b）而不注意上下文。

The unique block genesis is the block created at the inception of the system, and every valid block must have it in its past set. In addition, we relate to a hypothetical block, virtual (G). This block  satisfies past (virtual(G)) = G.  While  its  role  is  merely  methodological, virtual(G) can also be thought of as representing the next block that a node whose current observed DAG is G attempts to create G(v t) denotes  the  block  DAG  observed  by  node v ∈ N at  time t.  This  DAG  represents  the history of all (valid) block-messages received by the node, instantiating the abstract data structure assumed in Section 2.
独特的区块成因是在系统开始时创建的区块，并且每个有效的区块必须在其过去的集合中具有它。 另外，我们涉及一个虚拟块，虚拟（G）。 该块满足过去（虚拟（G））= G。虽然它的作用仅仅是方法论，但虚拟（G）也可以认为代表下一个块，其当前观察到的DAG是G的节点尝试创建G（vt） 表示在时间t由节点v∈N观察到的块DAG。 这个DAG表示节点接收的所有（有效）块消息的历史，实例化第2节中假设的抽象数据结构。

### B. The mining protocol
SPECTRE’s instructions to miners are extremely simple:
1)  When creating or receiving a block, transmit the block to all peers.
2)  When creating a block, embed in its header a list containing the hash of all leaf-blocks (blocks with in-degree 0) in the locally-observed DAG.
Note  that  these  instructions  allow  miners  to  operate  concurrently  irrespective  of  potential conflicts in the contents of their blocks.
SPECTER对矿工的指示非常简单：
1）创建或接收块时，将块发送给所有对等体。
2）创建块时，在其头中嵌入一个列表，其中包含本地观察的DAG中所有叶块（具有度0的块）的散列。
请注意，这些说明允许矿工同时进行操作，而不管他们的块内容有潜在冲突。

### C.  The TxO protocol
Overview. As the block DAG may contain conflicting transactions, we must provide a method for nodes to interpret the DAG and extract from it the set of accepted transactions. Doing so in a  way  that  will  be  agreed  upon  by  all  nodes  (eventually)  is  the  main  challenge  of  SPECTRE. We now describe how this is done.
概述。 由于块DAG可能包含冲突的事务，因此我们必须提供一种方法让节点解释DAG并从中提取已接受的事务集。 这样做的方式将由所有节点（最终）达成一致，这是SPECTER的主要挑战。 我们现在描述这是如何完成的。

The  topology  of  a  block  DAG G induces  a  natural  precedence-relation  over  blocks:  if x is reachable  from y (i.e., x∈past(y))  then x precedes y,  as  it  was  provably  created  before  it. SPECTRE extends this relation into a complete relation over G’s blocks, denoted ≺. This order is immediately translatable into an order over transactions in G: tx1 precedes tx2 if the block containing the former precedes that containing the latter. This relation, in turn, induces a natural subset  of  accepted  transactions: tx is  accepted  if  it  precedes  all  of  its  conflicting  transactions in G.  The  relation ≺ is  generated  by  a  pairwise  vote  procedure  that  occurs  independently  for every pair of blocks. The operation of this layer will be explained in the next subsections.
块DAG G的拓扑在块上引入自然的优先关系：如果x从y（即，x∈past（y））可到达，则x在y之前，因为它可以在其之前被创建。 SPECTER将此关系扩展为G块上的完整关系，记为≺。 如果包含前者的块在包含后者的块之前，该订单可立即转换为G：tx1之前的订单中的订单。 反过来，这个关系引发了一个可接受事务的自然子集：如果它在G中的所有冲突事务之前，则tx被接受。关系≺由配对投票过程生成，该过程独立于每对块进行。 这一层的操作将在下一小节中解释。

Although  we  may  at  times  refer  to ≺ as  though  it  orders  blocks,  we  stress  that ≺ is  not necessarily a transitive relation. It is possible to have a series of blocks that precede each other cyclically. The lack of a total linear ordering over blocks is in fact the way SPECTRE utilizes the weaker consensus requirements of our framework, as a linear order is equivalent to solving the consensus problem [3].
虽然我们有时可能会提到≺好像命令块一样，但我们强调≺不一定是传递关系。 可能会有一系列循环前后的块。 缺少块的总线性排序实际上是SPECTER利用我们框架的较弱共识需求的方式，因为线性排序相当于解决共识问题[3]。

Pairwise  ordering  of  blocks. The  basic  layer  of  SPECTRE  involves  deciding  on  a  pairwise order  over  the  block  DAG.  Fix  two  blocks x,y ∈ G.  In  order  to  decide  if x ≺ y or y ≺ x, we  interpret  the  structure  of  the  DAG  as  representing  an  abstract  vote.  Every  block z ∈ G is considered a voter with respect to the pair (x,y), and its vote is inferred from the structure of the DAG. We represent a vote by a number in {−1, 0, +1}, and we denote z’s voting-profile on all pairs by vote (z,G). vote x,y (z,G) = −1 represents x preceding y (x≺y), vote x,y (z,G) = +1 represents y preceding x, and vote x,y (z,G) = 0 represents a tie. Importantly, vote (z,G) is an asymmetric relation: vote y,x (z,G) = − vote x,y (z,G).
块的成对排序。 SPECTER的基本层涉及确定块DAG上的成对顺序。 修正两个块x，y∈G.为了决定x≺y还是y≺x，我们将DAG的结构解释为表示抽象投票。 每个块z∈G被认为是一个关于对（x，y）的选举人，并且它的投票是从DAG的结构中推断出来的。 我们用{-1,0，+1}中的一个数字来表示投票，并且我们用投票（z，G）表示z在所有对上的投票配置文件。 投票x，y（z，G）= -1代表x之前的y（x≺y），投票x，y（z，G）= +1代表y前面的x，投票x，y（z，G）= 0代表一个领带。 重要的是，vote（z，G）是一个不对称关系：vote y，x（z，G）= - vote x，y（z，G）。

To  simplify  presentation,  we  associate  a  vote  with virtual (G) as  well.  Recall  that  the virtual  block  of G is  a  hypothetical  block  which  satisfies past (virtual (G))  = G.  The  vote of virtual (G) represents  essentially  the  aggregated  vote  of  the  entire  block  DAG.  The  basic rules of z’s vote, for any z ∈ G ∪{virtual (G)}, are as follows:
为了简化演示，我们还将投票与虚拟（G）相关联。 回想一下，G的虚拟块是满足过去（虚拟（G））= G的假设块。虚拟（G）的投票基本上表示整个块DAG的聚合投票。 对于任何z∈G∪{virtual（G）}，z的投票基本规则如下：
1) if z ∈ G is  in future (x) but  not  in future (y) then  it  will  vote  in  favour  of x (i.e.,  for x ≺ y).
 如果z∈G future（x）但 future（y），则它将投票赞成x（即，对于x≺y）。
2) if z ∈ G is in future (x) ∩ future (y) then z’s vote will be determined recursively according to  the  DAG  that  is  reduced  to  its  past,  i.e.,  it  has  the  same  vote  as virtual (past (z)).  If the result of this vote is a tie, z breaks it arbitrarily.
 如果z∈G未来（x）∩future（y），则z的投票将根据减少到其过去的DAG递归确定，即它具有与虚拟（过去（z））相同的投票。 如果这次投票的结果是平局，z就会任意打破。
3) if z∈ G is not in the future of either blocks then it will vote the same way as the vote of the majority of blocks in its own future.
 如果z∈G不在任何区块的未来，那么它将以与未来大多数区块的投票相同的方式投票。
4) if z is the virtual block of G then it will vote the same way as the vote of the majority of blocks in G.
 如果z是G的虚拟块，那么它将以与G中大多数块的投票相同的方式投票。
5) finally,  (for  the  case  where z equals x or y), z votes  for  itself  to  succeed  any  block  in past (z) and to precede any block outside past (z).
 最后（对于z等于x或y的情况），z投票赞成自己继续past（z）中的任何块，并且在past（z）之外的任何块之前投票。

 Intuitively,  the  first  rule  dictates  that  a  block  that  was  honestly  published  gain  votes  over blocks  that  are  secretly  withheld,  as  honest  nodes  keep  adding  new  blocks  to  its  future  set. The second and fourth rules together guarantee majority amplification, as new blocks add votes that  comply  with  and  enhance  previous  decisions.  The  third  rule  is  the  most  subtle;  basically, it allows blocks in past (x) (in addition to those in future (x)) to vote in its favour against y, in case y was withheld for a long time. This is needed to counter a pre-mining attack scheme, which will be described in future sections. Notice that all votes respect the DAG’s topology: If x is reachable from y then all blocks vote unanimously x ≺ y.
 直观地说，第一条规则规定，一个真正发布的区块会获得对隐藏的隐藏区块的投票，因为诚实的节点不断为其未来集合添加新的区块。 第二和第四条规则共同保证大部分放大，因为新的区块增加了符合并加强先前决定的投票。 第三条规则是最微妙的; 基本上，它允许past（x）的区块（除了future（x）的区块）投票赞成反对y，以防y被长时间扣留。 这是对付预挖矿攻击计划所需要的，这将在以后的章节中介绍。 请注意，所有投票都尊重DAG的拓扑结构：如果x是从y到达的，那么所有块都一致投票x≺y。

Figure 1 illustrates the voting procedure with regards to a single pair of blocks (x, y). Additional examples along with intuition regarding this key algorithm are provided in Appendix A.
图1说明了关于一对块（x，y）的投票程序。附录A提供了有关此关键算法的其他示例以及直觉。

Property 4.Once a block is published, the set of blocks that precede it in the pairwise ordering closes fast—w.h.p. it consists only of blocks published before or right after its publication.
属性4.一旦发布块，成对排序之前的块集合将关闭fast-w.h.p。 它仅包含在其发布之前或之后发布的块。

The implications of this guarantee to the security of transactions is immediate, at least at the intuitive level: A user whose transaction is embedded in some published block x can guarantee its safety by waiting some time after x’s publication before accepting it; he is then guaranteed that  any  block  published  later  on  –  and  that  might  contain  a  conflicting  transaction  –  will  be preceded  by x hence  will  not  threaten  the  acceptance  of  his  transaction.  In  Section  5  we  will explain how this guarantee is achieved.
这种保证对交易安全的影响是立竿见影的，至少在直观的层面上是这样的：一个用户的交易被嵌入到某个已发布的块x中，可以通过在x发布之前等待一段时间来保证其安全性，然后再接受它; 那么他可以保证，任何后来发布的区块 - 可能包含冲突的交易 - 都将在x之后，因此不会威胁接受他的交易。 在第5节中，我们将解释如何实现这一保证。

Accepting  transactions. Equipped  with  the  pairwise  relation  over  blocks,  we  now  turn  to construct  the  set  of  accepted  transactions.  To  maintain  consistency,  we  mark  a  transaction  as accepted iff all three conditions below hold true:
接受交易。 通过块上的配对关系，我们现在转而构建一组已接受的交易。 为了保持一致性，如果以下所有三个条件都成立，我们将交易标记为已接受：
1) all of its inputs have been accepted.
2)  all conflicting transactions from its anticone set (i.e., that are not related to it topologically) are contained in blocks that are preceded by the block containing the transaction.
3)  all conflicting transactions from its past set (i.e., that precede it in the DAG, topologically) have been rejected.
1）所有的输入都被接受。
2）所有在它的anticone集合中的（即与拓扑无关的交易）冲突交易都包含在包含该交易的块的前面的块中。
3）所有与past相冲突的交易（即DAG之前的拓扑交易）都被拒绝。

Algorithm  2  implements  these  rules,  and  outputs  a  set  of  accepted  transactions.  It  operates recursively,  and  should  be  initially  called  with TxO(G,G) (we  later  denote  this  simply  by TxO (G)).  In  the  algorithm,  the  notation ZG(tx) stands  for  all  blocks  in G that  contain tx. Some complexity arises due to possible multiple copies of the same transaction in the DAG; we denote by [tx] the equivalence class containing all of tx’s copies.
算法2实现这些规则，并输出一组已接受的事务。 它递归地运行，并且应该首先用TxO（G，G）调用（我们稍后通过TxO（G）简单地表示这一点）。 在算法中，符号ZG（tx）代表G中包含tx的所有块。 由于DAG中可能存在多个相同事务的副本，因此会出现一些复杂性; 我们用[tx]表示包含所有tx副本的等价类。

The  third  part  of  the  SPECTRE  protocol,  namely,  the RobustTxO procedure,  is  rather involved. We defer its description to Appendix C.
SPECTER协议的第三部分，即RobustTxO过程相当复杂。 我们将其描述推迟到附录C.



# APPENDIX C
easure the robustness of this order,
### A. Robustness of the block pairwise ordering 块成对排序的鲁棒性
Assume that in the order of the current observable DAG the block x precedes y. We need a method to measure how likely is it that this relation will persist forever. Algorithm 3 outputs an upper bound on the probability that an attacker will be able to reverse the relation x ≺ y. When the  argument y is  unspecified,  the  interpretation  of  the  algorithm’s  output  is x’s  robustness against  an  unseen  block  (withheld  by  an  attacker  or  yet  to  be  created).  In  the  algorithm, gap (b,G) denotes the size of the set {z∈anticone(b,G): vote z,b (virtual(G))≥0}.  The notation 〈G,z,K〉will be explained in the paragraphs that follow.
假设按照当前可观察的DAG的顺序，块x在y之前。 我们需要一种方法来衡量这种关系将永远持续下去的可能性。 算法3输出攻击者将能够逆转关系x≺y的概率的上界。 当参数y未指定时，算法输出的解释是x针对未被看见的块（由攻击者隐瞒或尚未创建）的鲁棒性。 在算法中，gap（b，G）表示集合{z∈anticone（b，G）的大小：vote z，b（virtual（G））≥0}。 符号<G，z，K>将在下面的段落中解释。
In the algorithms below, we omit for the sake of brevity the following parameters which the user must set by himself: α – maximal size of attacker, d – upper bound on D (the recent delay diameter in the network), λ – the block creation rate.
在下面的算法中，为了简洁起见，我们省略了用户必须自己设置的以下参数：α - 攻击者的最大尺寸，d - D上的上限（网络中最近的延迟直径），λ - 块 创造率。

