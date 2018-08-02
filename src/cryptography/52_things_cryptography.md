## 52 Things People Should Know To Do Cryptography
## 密码学52个知识点
What is this?
Cryptography is a highly interdisciplinary area; calling on expertise in Pure Mathematics, Computer Science and Electronic Engineering. At Bristol we cover the full range of these topics and as such our students come with a variety of backgrounds and need to understand a diverse range of topics. Students starting can often feel overwhelmed by the types of knowledge that they feel they need to know; not knowing what they need to remember and what they should not bother remembering.

密码学是一个高度跨学科的领域：包括数学，计算机科学和电子工程方面的知识。在Bristol大学，我们涵盖了所有这些主题，不管我们的学生来自何种背景，都需要了解各种主题。开始的时候，学生往往会对这些知识点不知所措，不知道他们需要记住什么以及他们不应该记住什么。

To aid you, below we have collected a set of 52 short points of things we think that at the end of the first year of a PhD all students should have some familiarity with. There is one point for every week of the year. If you know these things then following seminars, study groups and conference talks will be much easier. It will also help in putting your own work into context. Some of these are somewhat advanced topics, some of these are what one would pick up in certain undergraduate courses. This is deliberate since some are about being a cryptographer, and some are to address the fact that students start with different backgrounds.

为了帮助你，下面我们收集了一系列52个关于我们认为在博士学位第一年结束时的所有学生都应该熟悉的内容。 一年中每周有一分。 如果你知道这些事情，那么在研讨会之后，研究小组和会议谈话将变得更容易。 它也将帮助您将自己的工作置于上下文中。 其中一些是有些高级的话题，其中一些是在某些本科课程中会选择的。 这是故意的，因为学生都是有各自的学习背景，有些人是关于密码学，有些是为了解决这样一个事实。

If at the end of the first year you know the answers to ninety percent of the things we list then you should find that you will get more out of the conferences and talks you attend in your second year. In addition it will be easier to talk to cryptographers (who may be future employers) from other institutions since you will be able to converse with them using a common language. Almost all of the following are discussed in our undergraduate cryptography courses.

如果在第一年结束时，你知道我们列出的百分之九十的答案，那么你应该会发现，你会在第二年参加的会议和谈话中获得更多的回报。 此外，与其他机构的密码学家（可能是未来的雇主）交谈会更容易，因为您可以使用通用语言与他们交谈。 以下几乎所有内容都在我们的本科密码学课程中讨论。

By each section we give a reference to places where the definitions can be found, or where to start your reading. The list of references can be found at the bottom. Not all answers can be found in the references cited, but they should give you a place to start looking.

通过每个部分，我们都会提供可以找到定义的地方或从哪里开始阅读。 参考列表可以在底部找到。 并不是所有的答案都可以在参考文献中找到，但他们应该给你一个开始寻找的地方。

### Computer Engineering ([E])
- 1 What is the difference between the following?
    - general-purpose processor.
    - general-purpose processor with instruction-set extensions.
    - special-purpose processor (or co-processor).
    - An FPGA.
- 2 What is the difference between a multi-core processor and a vector processor?
- 3 Estimate the relative computational and storage capabilities of...
    - a smart-card
    - a micro-controller (i.e. a sensor node)
    - an embedded or mobile computer (e.g., a mobile phone or PDA)
    - a laptop- or desktop-class computer.

### （中文）计算机工程（[E]）
- 1 以下几点有什么区别？
     - 通用处理器。
     - 带指令集扩展的通用处理器。
     - 专用处理器（或协处理器）。
     - 一个FPGA。
- 2 多核处理器和矢量处理器有什么区别？
- 3 估计以下设备的相对计算和存储能力
     - 一张智能卡
     - 微控制器（即传感器节点）
     - 嵌入式或移动计算机（例如，移动电话或PDA）
     - 一台笔记本电脑或台式电脑。

### Theoretical Computer Science ([F])
- 4 What is meant by the complexity class P?
- 5 What is meant by the complexity class NP?
- 6 How can we interpret NP as the set of theorems whose proofs can be checked in polynomial time?
- 7 How does randomness help in computation, and what is the class BPP?
- 8 How does interaction help in computation, and what is the class IP?
- 9 What are Shannon's definitions of entropy and information?

### （中文）理论计算机科学（[F]）
- 4 复杂度类P含义是什么？
- 5 复杂度类NP含义是什么？
- 6 我们如何将NP解释为可以在多项式时间内检验证明的一组定理？
- 7 随机性如何帮助计算，什么是BPP类？
- 8 交互如何帮助计算，什么是类IP？
- 9 香农对熵和信息的定义是什么？

### Mathematical Background ([A,B])
- 10 What is the difference between the RSA and the Strong-RSA problem?
- 11 What are the DLP, CDH and DDH problems?
- 12 What is the elliptic curve group law?
- 13 Outline the use and advantages of projective point representation.
- 14 What is a cryptographic pairing?

### （中文）数学背景（[A，B]）
- 10 RSA和Strong-RSA问题有什么区别？
- 11 什么是DLP，CDH和DDH问题？
- 12 什么是椭圆曲线群法则？
- 13 概述投影点表示的用途和优点。
- 14 什么是密码配对？

### Basic (Practical or Deployed) Cryptographic Schemes and Protocols ([A])
- 15 Describe the key generation, encryption and decryption algorithms for RSA-OAEP and ECIES.
- 16 Describe the key generation, signature and verification algorithms for DSA, Schnorr and RSA-FDH.
- 17 Describe and compare the round structure of DES and AES.
- 18 Draw a diagram (or describe) the ECB, CBC and CTR modes of operation.
- 19 Describe the Shamir secret sharing scheme.
- 20 How are Merkle-Damgaard style hash functions constructed?

### （中文）基本（实用或部署）密码方案和协议（[A]）
- 15 描述RSA-OAEP和ECIES的密钥生成，加密和解密算法。
- 16 描述DSA，Schnorr和RSA-FDH的密钥生成，签名和验证算法。
- 17 描述和比较DES和AES的圆形结构。
- 18 绘制（或描述）ECB，CBC和CTR操作模式的图表。
- 19 描述沙米尔秘密分享计划。
- 20 Merkle-Damgaard风格的哈希函数是如何构建的？

### Cryptographic Implementation Details ([A])
- 21 How does the CRT method improve performance of RSA?
- 22 How do you represent a number and multiply numbers in Montgomery arithmetic?
- 23 Write a C program to implement Montgomery arithmetic.
- 24 Describe the binary, m-ary and sliding window exponentiation algorithms.
- 25 Describe methods for modular reduction using "special" primes that define GF(p) and GF(2^n).
- 26 Describe the NAF scalar multiplication algorithm.

### （中文）加密实现细节（[A]）
- 21 CRT方法如何提高RSA的性能？
- 22 你如何在蒙哥马利算术中表示数字和乘数？
- 23 写一个C程序来实现蒙哥马利算术。
- 24 描述二元，m元和滑动窗口指数运算算法。
- 25 描述使用定义GF（p）和GF（2 ^ n）的“特殊”素数进行模减量的方法。
- 26 描述NAF标量乘法算法。

### Security Definitions and Proofs ([A,B,C])
- 27 What is the AEAD security definition for symmetric key encryption?
- 28 What is the IND-CCA security definition for public key encryption?
- 29 What is the UF-CMA security definition for digital signatures?
- 30 Roughly outline the BR security definition for key agreement?
- 31 Give one proof of something which involves game hopping
- 32 Outline the difference between a game based and a simulation based security definition.

### （中文）安全定义和证明（[A，B，C]）
- 27 对称密钥加密的AEAD安全定义是什么？
- 28 公钥加密的IND-CCA安全定义是什么？
- 29 数字签名的UF-CMA安全定义是什么？
- 30 粗略概述了密钥协议的BR安全定义？
- 31 给出一个涉及游戏跳跃的东西的证明
- 32 概述基于游戏和基于模拟的安全定义之间的区别。

### Mathematical Attacks ([A,B])
- 33 How does the Bellcore attack work against RSA with CRT?
- 34 Describe the Baby-Step/Giant-Step method for breaking DLPs
- 35 Give the rough idea of Pollard rho, Pollard "kangaroo" and parallel Pollard rho attacks on ECDLP.
- 36 What is meant by index calculus algorithms?
- 37 Roughly outline (in two paragraphs only) how the NFS works.

### （中文）数学攻击（[A，B]）
- 33 Bellcore攻击如何利用CRT对抗RSA？
- 34 描述打破DLP的Baby-Step / Giant-Step方法
- 35 给出Pollard rho，Pollard“袋鼠”和平行Pollard rho攻击ECDLP的粗略想法。
- 36 指数演算算法的含义是什么？
- 37 粗略地概述（仅在两段中）NFS的工作原理。

### Practical Attacks ([D])
- 38 What is the difference between a covert channel and a side-channel?
- 39 What is the difference between a side-channel attack and a fault attack?
- 40 What is usually considered the difference between DPA and SPA?
- 41 Are all side channels related to power analysis?
- 42 Look at your C code for Montgomery multiplication above; can you determine where it could leak side channel information?
- 43 Describe some basic (maybe ineffective) defences against side channel attacks proposed in the literature for AES.
- 44 Describe some basic (maybe ineffective) defences against side channel attacks proposed in the literature for ECC.
- 45 Describe some basic (maybe ineffective) defences against side channel attacks proposed in the literature for RSA.

### （中文）实际攻击（[D]）
- 38 隐蔽频道和旁道之间有什么区别？
- 39 旁道攻击和故障攻击有什么区别？
- 40 通常认为DPA和SPA之间的区别是什么？
- 41 所有旁道都与功率分析有关吗？
- 42 看看你的C代码上面的蒙哥马利乘法; 你能确定它可能泄露侧面频道信息的位置吗？
- 43 描述针对AES文献中提出的针对边信道攻击的一些基本（可能无效）的防御措施。
- 44 描述针对ECC的文献中提出的一些针对旁道攻击的基本（可能无效）防御措施。
- 45 描述针对RSA文献中提出的针对边道攻击的一些基本（可能无效）的防御措施。

### Advanced Protocols and Constructions ([A,B])
- 46 What does correctness, soundness and zero-knowledge mean in the context of a Sigma protocol?
- 47 What is the Fiat-Shamir transform?
- 48 What is the purpose and use of a TPM?
- 49 Describe the basic ideas behind IPSec and TLS.
- 50 What is the BLS pairing based signature scheme?
- 51 What is the security model for ID-based encryption, and describe one IBE scheme.
- 52 Pick an advanced application concept such as e-Voting, Auctions or Multi-Party Computation. What are the rough security requirements of such a system?

### （中文）先进的协议和结构（[A，B]）
- 46 在Sigma协议的背景下，正确性，健全性和零知识是什么意思？
- 47 什么是菲亚特 - 沙米尔变换？
- 48 TPM的目的和用途是什么？
- 49 描述IPSec和TLS背后的基本思想。
- 50 什么是BLS配对签名方案？
- 51 基于ID的加密的安全模型是什么，并描述了一个IBE方案。
- 52 选择电子投票，拍卖或多方计算等高级应用程序概念。 这种系统的安全要求是什么？

## Further Reading
- [A] Nigel's book is deliberately informal and tries to give quick flavours of what is important in theory and practice.
- [B] The Katz Lindell book is a better formal introduction to modern theoretical cryptography but it is less good in its treatment of what is important in the real world (e.g. the coverage of AES, ECC, implementation, etc is quite limited).
- [C] Goldreich's two volume book is a very good introduction to the deep theory, but deliberately does not cover practical cryptography.
- [D] Elisabeth's DPA book is the best introduction to all things about side-channels.
- [E] Dan's book is a good starting place for computer architecture and learning VHDL.
- [F] Goldreich's book on complexity theory is a good place to start. Its approach is much more down-to-earth and sensible than other approaches (i.e. P vs NP is presented in terms of is it easier to check or find proofs?)
