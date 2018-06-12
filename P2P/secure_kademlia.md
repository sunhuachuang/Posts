### S/Kademlia: A Practicable Approach Towards Secure Key-Based Routing
### S/Kademlia：实现安全密钥路由的可行方法
[原始论文](https://ieeexplore.ieee.org/document/4447808/)

#### 针对Kademlia攻击
- 在下层网络的攻击，包括IP/TCP攻击形式，监听，窃取，伪造数据包
- 在覆盖网络上的攻击
  - Elicpse Attack 日蚀攻击 —— 防护要求：1. 不能免费生成ID，必须付出代价；2. 不能随意更改别人的路由表
  - Sybil Attack 女巫攻击 —— 防护要求：1. 无法完全杜绝，只能减弱；2. 付出代价生成ID
  - Churn Attack 搅动攻击 反复生成或者调整自己的ID —— 防护要求：1. 优先考虑长时间在先的节点
  - Adversarial Routing 对抗路由 —— 防护要求：1. 设计多条路径选择和长度优化算法
- 其他的攻击
  - Denial-of-Service (DoS)
  - Attacks on data storage
  
#### 设计
##### 1. 安全的生成ID
1. Hash函数主体
   - 针对硬件的信息(IP, PORT)
   - 针对公钥(Public Key) —— 优先选择
2. 签名强度
   - Weak Sign 只对IP地址等信息进行签名
   - Strong Sign 对整个消息体进行签名

3. 签名可信
   - CA 第三方可信机构的签名 —— 联盟链形式可行
   - Crypto puzzle sign 解决密码学难题 (PoW) —— 公链形式可行
   
##### 2. 构建稳固安全的sibling信息
- **sibling**:可靠存储着DHT中的确定的K-V信息的那些节点
- 因此，在S/Kademlia中，路由表由包含距离为d且具有 2^(i-1) ≤ d < 2^i, 0 ≤ i ≤ n 的节点的n个k桶的列表组成。大小η·s。由于新引入的同级列表，特殊子树处理可以省略。由于Kademlia中的路由表通过传入的查找请求隐式刷新，并且我们sibling表中的许多节点必须存储在Kademlia的k-桶中，因此维护sibling表的额外通信开销很小。

##### 3. 安全维护路由表
Kademlia使用被动方法来维护路由表。由于异或度量确保所有迭代查找沿着相同的路径收敛，Kademlia可以从传入的RPC中了解新节点的存在。为了保护S/Kademlia中的路由表维护，我们将信令消息分类到以下类：传入签名的RPC请求，响应或未签名的消息。每条消息都包含发件人地址。如果消息是弱签名或强签名，则该地址不能伪造或与另一个nodeId相关联。如果发件人地址有效并且来自RPC响应，我们称该发件人地址有效，如果该邮件已签名并且主动有效。 Kademlia使用这些发件人地址来维护他们的路由表。

当活动有效的发件人地址未满时，会立即将其添加到相应的存储区中。如果nodeId前缀在适当的位数χ中不同（例如，x> 32），则有效的发件人地址只能添加到存储桶中。这是必要的，因为攻击者可以很容易地生成与受害者nodeId共享前缀并溢出他的桶的nodeId，因为靠近自己的nodeId的桶只在Kademlia中稀疏填充。来自未签名消息的发件人地址将被忽略。如果消息包含有关其他节点的更多信息，则可以通过调用它们上的ping RPC来添加每个节点。如果一个节点已经存在于路由表中，它将在桶的尾部移动。

##### 4. 通过不相交的路径进行查找
我们已经展示了使用多条不相交路径来查找具有对抗节点的网络中的密钥的重要性。原始的Kademlia查找通过FIND_NODE RPC迭代查询α节点，以找到与目标密钥最近的k个节点。α是系统范围的冗余参数，在每个步骤中，将来自先前RPC的返回节点合并到排序列表中，从中选择下一个α节点。这种方法的一个主要缺点是，只要查询单个敌对节点，查找就会失败。

我们将此算法扩展为使用d不相交路径，从而提高了具有对抗节点的网络中的查找成功率。发起者通过从其本地路由表中取出距离目的密钥的k个最近节点并将其分布到d个独立的查找桶中来开始查找。从那里继续进行类似于传统Kademlia查找的d个并行查找。查找是独立的，除了一个重要的事实，即每个节点在整个查找过程中仅使用一次，以确保生成的路径真正不相交。通过使用同级列表，查找不会收敛于单个节点，而是终止于邻近邻居，这些邻居都知道目标密钥的完整同胞。因此，即使邻居的k-1是敌对的，查找仍然是成功的。

#### 评估
在本节中，我们用[OverSim](http://netsec.cs.uoregon.edu/gi2007/papers/1569026972.pdf)评估S/Kademlia，这是一个用于覆盖模拟的灵活框架。我们描述了仿真设置和程序，并最终描述了我们的仿真结果。

##### Simulation assumptions 模拟假设
We simulate adversarial nodes with the following assumptions: An adversarial node returns data that compromises the network in a worst case scenario. So in the case of a FIND_NODE RPC the worst behaviour would only return other collaborating nodes which are closer to the target nodeId. The adversarial also harvest other existing valid nodeIds in order to map them to a false transport addresses. This is the worst case since other reactions like an empty result or invalid data can be detected and the node would be removed from the network, i.e. the node would be considered as a stale contact. 

On the other hand we assume that well behaving nodes return adversarial node information in an equally distributed manner. This assumption is confirmed in section 4 because it is nearly impossible for an adversarial node to influence other nodes’ routing tables. 

With these assumptions we expect that a lookup of a node or siblings is successful if no adversarial node is on one path to the responsible node. In the case of a parallel lookup on multiple paths we simply stop pursuing each path that hit an adversarial node and the lookup is only considered successful, if one path is free of any adversarial nodes.

我们用以下假设模拟敌对节点：敌对节点在最坏情况下返回损害网络的数据。因此，在FIND_NODE RPC的情况下，最差的行为只会返回更接近目标nodeId的其他协作节点。对手还会收获其他现有的有效nodeIds，以便将它们映射到虚假的传输地址。这是最坏的情况，因为可以检测到诸如空结果或无效数据之类的其他反应，并且将该节点从网络中移除，即该节点将被视为陈旧联系人。另一方面，我们假设良好行为的节点以平均分布的方式返回对抗节点信息。这个假设在第4节中得到证实，因为敌对节点几乎不可能影响其他节点的路由表。通过这些假设，我们预计如果没有对抗节点位于负责节点的一条路径上，则节点或兄弟节点的查找是成功的。在多条路径上进行并行查找的情况下，我们只需停止追踪遇到敌对节点的每条路径，并且只有一条路径没有任何敌对节点时，才会将查找视为成功。

##### Simulation procedure 模拟过程
To keep the simulation efficient we first create a static Kademlia overlay network with N nodes that is fully stabilized. Then we continue by processing N node lookups and evaluate the fraction of successful queries. This process is repeated with increasing adversarial nodes by 5% until 90% of the nodes are adversarial. Since we do not evaluate churn all simulations are done with a parameter of α = 1 and we assume that the network stays in a stable state after the bootstrapping phase, but under the influence of adversarial nodes.

为了保持仿真效率，我们首先创建一个静态Kademlia覆盖网络，其中包含N个完全稳定的节点。 然后我们继续处理N个节点查找并评估成功查询的比例。 随着对抗节点增加5％重复该过程，直到90％的节点是对抗的。 由于我们不评估流失，所有仿真都是在α= 1的参数下完成的，并且我们假定网络在引导阶段后保持稳定状态，但是在对抗节点的影响下。

##### Results
We simulated two setups with a network size of N = 10000 nodes, s = 16 siblings using d ∈{1, 2, 4, 8} disjoint paths. In Figure 4 we show the fraction of success- ful lookups dependant on the number of adversarial nodes for a fixed bucket size of k = 16. For d = 1 the lookup process is similar to a standard Kademlia lookup. The figure clearly shows that by increasing the number of parallel disjoint paths d the fraction of successful lookups can be considerably improved. In this case the communication overhead increases linearly with d. We also see that with k = 16 there is enough redundancy in the k-buckets to actually create d disjoint paths. 

我们使用d∈{1，2，4，8}不相交的路径模拟了网络规模为N = 10000个节点，s = 16个兄弟的两个设置。在图4中，我们展示了对于k = 16的固定桶大小，取决于敌对节点数量的成功查找的比例。对于d = 1，查找过程类似于标准的Kademlia查找。该图清楚地表明，通过增加并行不相交路径的数量d，成功查找的比例可以大大提高。在这种情况下，通信开销随着d线性增加。我们还可以看到，当k = 16时，k桶中有足够的冗余来实际创建不相交的路径。

In the second setup we adapted k = 2·d to the number of disjoint paths to keep a minimum of redundancy in the routing tables and consequently reduce communication overhead. The results in figure 5 show, that a smaller k leads to a smaller fraction of successful lookups compared to figure 4. The reason for this is the increased average path length due to the smaller routing table as shown in the path length distribution diagram. 

在第二种设置中，我们将k = 2·d调整为不相交路径的数量，以保持路由表中的最小冗余度，并因此减少通信开销。图5中的结果显示，与图4相比，较小的k导致成功查找的一小部分。其原因是由于路径表中较小的路由表增加了平均路径长度，如路径长度分布图中所示。

We conclude that d = 4..8 with a k = 8..16 is a good choice for S/Kademlia. Higher values of d and k seem not worth the additional communication costs. Larger values for k would also increase the probability that a large fraction of buckets are not full for a long time. This unnecessarily makes the routing table more vulnerable to Eclipse attacks. 

我们得出结论，d = 4..8，k = 8..16对S / Kademlia来说是个不错的选择。较高的d和k值似乎不值得额外的通信成本。较大的k值也会增加很大一部分桶长时间不满的概率。这不必要地使路由表更容易受到Eclipse攻击。

Since we present simulations with N = 10000 nodes only, one might argue that this is a rather small number of nodes and not comparable to huge networks. In fact the path length highly corelates with the fraction of successful lookups. On the other hand the network topology can be easily tuned to have a smaller diameter and therefore a shorter average path length. This is usually done by considering multiple bits b of the nodeId in each step. So the network can be tuned to the level of security needed in different scenarios.

由于我们仅提供了N = 10000个节点的模拟，有人可能会认为这是一个相当少的节点，并不能与大型网络相媲美。事实上，路径长度与成功查找的比例高度相关。另一方面，网络拓扑结构可以很容易地调整为具有较小的直径，因此较短的平均路径长度。这通常通过在每个步骤中考虑nodeId的多个位b来完成。因此，可以将网络调整到不同情况下所需的安全级别。

#### 相关工作
Castro et al. study attacks on routing of messages in structured peer-to-peer overlays. They propose several defenses to secure the join process, routing table maintenance and message forwarding. The secure assignment of nodeIds is delegated to a central trusted certification authority. 

卡斯特罗等人。研究对结构化对等覆盖中的消息路由的攻击。他们提出了一些防御措施来确保加入过程，路由表维护和消息转发。将nodeIds的安全分配委托给中央信任的证书颁发机构。

Sit and Morris [16] present a categorization of attacks against peer-to-peer distributed hash tables on the basis of Chord, CAN and Pastry. They state that an important step to defend these attacks is detection by defining verifiable system invariants. For example nodes can detect incorrect lookup routing by verifying that the lookup gets “closer” to the destination key. 

Sit和Morris [16]在Chord，CAN和Pastry的基础上提出了针对点对点分布式哈希表的攻击分类。他们表示，防御这些攻击的重要步骤是通过定义可验证的系统不变量进行检测。例如，节点可以通过验证查找是否“接近”目标密钥来检测不正确的查找路由。

Srivatsa and Liu [17] investigate three security threats in DHT-based P2P systems. First they present an attack on the routing scheme, in which a single adversarial node can block all lookup requests in the absence of alternate paths. Therefore they highlight the importance of several alternate optimal paths in conjunction with the feasibility to detect incorrect lookup results. Furthermore they present an attack on the data placement scheme and show that replication alone is not sufficient to tolerate attacks by adversarial nodes, but has to be combined with cryptographic techniques to be effective. Finally they show that the nodeId selection process has to be restricted to prevent adversarial nodes from corrupting specific data items. 

Srivatsa和Liu [17]研究了基于DHT的P2P系统中的三种安全威胁。首先，他们对路由方案提出攻击，其中单个敌对节点可以在没有备用路径的情况下阻止所有查找请求。因此，他们强调了几种备选最佳路径的重要性，以及检测不正确查找结果的可行性。此外，他们对数据放置方案提出了攻击，并表明单靠复制不足以容忍敌对节点的攻击，但必须与密码技术相结合才能有效。最后，他们显示必须限制nodeId选择过程，以防止敌对节点破坏特定的数据项。

Awerbuch and Scheideler [1] present a theoretical DHT which is provably robust against adversarial join-leave as well as insert-lookup attacks. The design of the DHT is high level and it is an open question how hard it would be to transform their ideas into a practicable protocol. Another DHT which can provably deal with join-leave attacks is S-Chord, though it is limited to a linear number of adversarial join requests. 

Awerbuch和Scheideler [1]提出了一种理论上的DHT，它可以抵抗对抗式加入假以及插入式查找攻击。 DHT的设计是高层次的，它是一个开放的问题，将它们的想法转化为可行的协议是多么困难。另一个可以处理加入 - 离开攻击的DHT是S-Chord，尽管它仅限于线性数量的对抗加入请求。

Cerri et al. focus on attacks that arise from the unlimited choice of nodeIds and exemplify their findings with the Kademlia protocol. They propose to limit free nodeId selection by coupling IP address and port to the nodeId by a hash function. To make it harder for adversarial nodes to attack specific data items, they propose that data items should be stored at a temporary key, which is regularly rotated. This is done by hashing the data item’s key with some temporal information to compute the temporary key.

Cerri等人重点关注无限选择nodeIds引起的攻击，并用Kademlia协议举例说明他们的发现。他们建议通过散列函数将IP地址和端口耦合到nodeId来限制空闲的nodeId选择。为了使敌对节点难以攻击特定的数据项，他们建议将数据项存储在一个临时密钥中，该密钥会定期轮换。这是通过用一些时间信息对数据项的密钥进行散列来计算临时密钥来完成的。

There are several papers in which countermeasures against Sybil attacks are proposed: In Rowaihy et al. present an admission control system for structured peer-to-peer systems. The systems constructs a tree-like hierarchy of cooperative admission control nodes, from which a joining node has to gain admission. Another approach to limit Sybil attacks is to store the IP addresses of participating nodes in a secure DHT. In this way the number of nodeIds per IP address can be limited by querying the DHT if a new node wants to join. 

有几篇文章提出了针对Sybil攻击的对策：在Rowaihy et al。为结构化的点对点系统提供一个准入控制系统。这些系统构建了协作接纳控制节点的树状分层结构，从中加入节点必须获得接纳。限制Sybil攻击的另一种方法是将参与节点的IP地址存储在安全的DHT中。通过这种方式，每个IP地址的nodeIds数量可以通过查询DHT来限制，如果新节点想要加入。

Singh et al. [15] study the impacts of Eclipse attacks on structured overlay networks and propose to defend against this attack by letting nodes audit each others connectivity. The idea is, that a node mounting an Eclipse attack has a node degree higher than average. 

Singh等人[15]研究Eclipse攻击对结构化覆盖网络的影响，并提出通过让节点互相审计连接来抵御这种攻击。这个想法是，一个挂载Eclipse攻击的节点的节点度高于平均值。

Nielson et al. regard the class of rational attacks. They assume that a large fraction of nodes in a peer-to-peer system are selfish and try to maximize their consumption of system ressources while minimizing the use of their own.

Nielson等人视为理性的攻击类。他们认为对等系统中很大一部分节点是自私的，并试图最大限度地消耗系统资源，同时尽量减少自己的使用。

#### 结论
In this paper we presented a secure key-based routing protocol based on Kademlia. Although the elegant routing table maintenance makes Kademlia already insusceptible to some attacks, we have shown that there are several vulnerability that make it easy for adversarial nodes to gain control of the network. 

在本文中，我们提出了一个基于Kademlia的基于安全密钥的路由协议。尽管优雅的路由表维护使得Kademlia已经不易受到某些攻击，但我们已经表明，存在多个易受攻击节点控制网络的漏洞。

We propose several practicable solutions to make Kademlia more resilient.  First we suggest to limit free nodeId generation by using crypto puzzles in combination with public key cryptography. Furthermore we extend the Kademlia routing table by a sibling list. This reduces the complexity of the bucket splitting algorithm and allows a DHT to store data in a safe replicated way. Finally we propose a lookup algorithm which uses multiple disjoint paths to increase the lookup success ratio. 

我们提出几个切实可行的解决方案，使Kademlia更具弹性。首先，我们建议通过结合公钥密码术使用加密谜题来限制免费的nodeId生成。此外，我们通过兄弟列表扩展Kademlia路由表。这降低了桶分裂算法的复杂性，并允许DHT以安全复制的方式存储数据。最后，我们提出了一种查找算法，该算法使用多条不相交路径来提高查找成功率。

The evaluation of S/Kademlia in the simulation framework OverSim has shown, that even with 20% of adversarial nodes still 99% of all lookups are successful if disjoint paths are used. We believe that the proposed extensions to the Kademlia protocol are practical and could be used to easily secure existing Kademlia networks.

在模拟框架OverSim中对S / Kademlia的评估表明，如果使用不相交的路径，即使有20％的敌对节点仍然有99％的所有查找都是成功的。我们相信，对Kademlia协议的建议扩展是实用的，可以用来轻松保护现有的Kademlia网络。
