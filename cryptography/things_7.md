### [随机性对计算有什么帮助和什么是BPP？](https://bristolcrypto.blogspot.com/2014/11/52-things-number-7-how-does-randomness.html)

```
Q7 How does randomness help in computation, and what is the class BPP?
Q7 随机性对计算有什么帮助，以及什么是BPP类？
```

So far, during this blog series Ryan has introduced us to complexity classes, and in particular to P:
- P  is the class of languages decidable in polynomial time by a deterministic Turing machine.

到目前为止，在这个博客系列中，Ryan向我们介绍了复杂类，特别是P：
- P是确定性图灵机在多项式时间内可确定的语言类。

Then, Guy introduced us to complexity class NP:
- NP is the class of languages decidable in polynomial time by a nondeterministic Turing machine.

然后，Guy向我们介绍了复杂类NP：
- NP是一种非确定性图灵机在多项式时间内可确定的语言类。

This week I am going to introduce the complexity class BPP:
- BPP is the class of languages that are recognised by a probabilistic polynomial time Turing machine with an error probability of 1/3.

本周我将介绍复杂类BPP：
- BPP是由概率多项式时间图灵机识别的错误概率为1/3的语言类。

#### Probabilistic Turing Machine 概率图灵机
A probabilistic Turing Machine[1] is a type of nondeterministic Turing Machine which randomly chooses between the available transitions at each point according to a probability distribution. What this means is that a probabilistic Turing machine can have stochastic results. On the same input, it could have different run times, accept it on one occasion and reject it on another. It could also never stop. This Turing Machine gives rise to other complexity classes such as RP, ZPP and, the one we're discussing in this post, BPP.

概率图灵机[1]是一种非确定性图灵机，它根据概率分布在每个点的可用转换之间随机选择。 这意味着概率图灵机可以有随机结果。 在相同的输入上，它可能有不同的运行时间，一次接受它，另一次拒绝。 它也永远不会停止。 这个图灵机引出了其他复杂类，如RP，ZPP和我们在这篇文章中讨论的BPP。

#### A little about the complexity class BPP 关于复杂类BPP的一点点内容
So as we have seen from the definition, the class BPP (Bounded-Error probabilistic polynomial time) contains the decision problems that are solvable in polynomial time by a probabilistic Turing machine with error probability 13. Note that this error probability can be chosen to be any value strictly between 0 and 12 due to a result named the amplification lemma which I will not discuss further here. The class BPP contains P, the class of problems solvable in polynomial time by a deterministic Turing Machine, this is due to the fact that a deterministic Turing Machine is a special case of the probabilistic Turing Machine (taking the only possible path with probability 1). As talked about in Guy's post, there is an open (Millennium) problem conjecturing as to whether P = NP. There is a similar question with BPP, being P = BPP? The number of problems known to be in BPP but not known to be in P is decreasing.

正如我们从定义中看到的那样，类BPP（有界误差概率多项式时间）包含可由多项式时间通过概率图灵机以13的错误概率解决的决策问题。注意，这个错误概率可以选择为 由于命名为放大引理的结果，任何值都严格限定在0到12之间，这里我将不再进一步讨论。 BPP类包含P，这是一个确定性图灵机在多项式时间可解的问题类，这是由于确定性图灵机是概率图灵机的一个特例（以概率1采用唯一可能的路径）。 正如Guy的文章所谈到的那样，对于P = NP是否存在一个开放的（千年）问题进行猜测。 BPP有一个类似的问题，即P = BPP？ 已知在BPP中但未知在P中的问题正在减少。

#### An example of a BPP Problem 一个BPP问题的例子
One of the most famous problems known to be in BPP  but not known to be in P was determining whether a number was prime. However, recently (2002) a deterministic polynomial time algorithm was found[2] for this problem meaning that it is indeed in P. Another problem known to be in BPP and currently still not known to be in P is polynomial identity testing[3], the problem of determining whether a polynomial is identically equal to the zero polynomial.

已知的BPP中最着名的问题之一，但不知道在P中是确定一个数字是否为素数。 然而，最近（2002年）发现了一个确定性多项式时间算法[2]，因为这个问题意味着它确实存在于P中。另一个已知的问题是在BPP中，并且目前还不知道在P中是多项式身份测试[3] ，确定多项式是否等于零多项式的问题。

There are still many very important unanswered questions on the topic of Complexity Classes. Some of which, if answered, could have a large impact on shaping the future of Cryptography and Computer Science.

关于复杂类的主题仍然有许多非常重要的未解答的问题。 其中一些如果得到解答，可能会对塑造未来密码学和计算机科学产生巨大影响。

- [1] - http://en.wikipedia.org/wiki/Probabilistic_Turing_machine
- [2] - http://en.wikipedia.org/wiki/AKS_primality_test
- [3] - http://en.wikipedia.org/wiki/Schwartz%E2%80%93Zippel_lemma

