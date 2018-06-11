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
   
##### 2. 构建稳固安全的邻居信息

##### 3. 安全维护路由表
