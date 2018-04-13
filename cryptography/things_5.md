### [复杂度类NP](https://bristolcrypto.blogspot.com/2014/11/52-things-number-5-what-is-meant-by.html)

```
Q5 What is meant by the complexity class NP ?
Q5 复杂度类NP含义是什么？

```

Last week, Ryan introduced us to complexity classes, and in particular to P:
- P  is the class of languages decidable in polynomial time by a deterministic Turing machine.

This week, we introduce another complexity class:
- NP is the class of languages decidable in polynomial time by a nondeterministic Turing machine.

上周，Ryan向我们介绍了复杂类课程，特别是P：
- P 是确定性图灵机在多项式时间内可确定的语言类。

本周，我们介绍另一个复杂类：
- NP 是一种非确定性图灵机在多项式时间内可确定的语言类。

#### What is a Nondeterministic Turing Machine (NDTM)?
#### 什么是非确定性图灵机（NDTM）？
Well, an NDTM is a Turing Machine for which the transition function can have multiple values for the same tape value/state pair (meaning it is not technically a function any more, so the correct thing would be to call it a transition relation). Thus evaluation of an NDTM on any particular input can be thought of as a tree, branching at each point the transition function provides more than one possible value. Now, an NDTM evaluates all of these possible branches at once, and accepts if at least one of these computations halts in the accept state. This definition generalizes from language membership to decision to computational problems in the same way as P did in last weeks blog.

NDTM是一个图灵机，对于它来说，转换函数对于同一个磁带值/状态对可以有多个值（这意味着它在技术上不再是一个函数，所以正确的做法是将其称为转换关系）。 因此，对任何特定输入的NDTM的评估可以被认为是一棵树，在每个点处，分支转换函数提供了多于一个可能的值。 现在，NDTM一次评估所有这些可能的分支，并接受这些计算中至少有一个是否在接受状态下停止。 这个定义从语言成员到决策到计算问题的泛化，就像P在上周的博客中一样。

#### Some Examples of NP problems
#### NP问题的一些例子
We begin with an easy example: path finding. Given a directed graph (on n vertices) is there a path from vertex A to vertex B. How do we know this is in NP? Well, there is an NDTM that solves it, which basically works by simply trying every route by branching each time there is a junction. If one of these branches (ie one of the trial routes) reaches B, then that branch terminates in the accept state. Any branch that does not reach B within n steps (ie after traversing n edges) terminates in the reject state. Since any path will involve at most n-1 edges, any valid route will be detected, and so this machine correctly decides whether the path exists.

我们从一个简单的例子开始：寻路。 给定一个有向图（在n个顶点上）有一条从顶点A到顶点B的路径。我们怎么知道这是NP？ 那么，有一个NDTM可以解决这个问题，它基本上是通过在每次有分支时通过分支尝试每条路径来工作的。 如果其中一个分支（即其中一条试验路线）达到B，则该分支终止于接受状态。 任何在n步内未达到B的分支（即在遍历n个边之后）终止于拒绝状态。 由于任何路径最多会涉及n-1条边，因此将检测到任何有效的路由，因此此机器会正确判断路径是否存在。

One of the key examples of an NP problem is the satisfiability problem:
- SAT: Given an expression in n boolean variables, is there an assignment of the variables such that the expression evaluates to True?

NP问题的一个关键例子是可满足性问题：
- SAT：给定n个布尔变量中的表达式，是否有变量赋值，以使表达式求值为True？

For example, the expression (A∧B)∨(A∧¬B) is satisfiable, with one valid assignment being A=B=True. Note that in it's standard form, SAT is a decision problem: it suffices to decide whether such an assignment exists, we don't have to find it.

例如，表达式 (A∧B)∨(A∧¬B) 可以满足，一个有效赋值是A = B = True。 请注意，在标准形式中，SAT是一个决策问题：决定是否存在这样的任务就足够了，我们不需要找到它。

#### Ok, so there are problems in NP. What is interesting about it?
#### OK，所以NP是有问题的。 有趣的是什么？
Firstly, we see that P ？= NP since a DTM is an NDTM that just happens not to ever branch (in fact, our first example can actually be solved by a DTM and so is within P). So, the real question is what sort of things can we do in NP that we couldn't do in P? Well, this is the root of the P=?NP millenium problem, which is a major open problem. There are certainly problems that we have found that are known to be in NP that we do not know to be in P, but perhaps future research will show that these are also in P.

首先，我们看到 P ？= NP 自DTM是一个NDTM，它恰好不会分支（事实上，我们的第一个例子实际上可以通过DTM解决，因此在P内）。所以，真正的问题是我们可以在NP中做什么样的事情，我们在P中无法做到？那么，这是P =？NP千年问题的根源，这是一个重大的开放问题。当然，我们发现存在一些问题，我们发现这些问题存在于NP中，而我们不知道这些问题存在于P中，但是也许未来的研究将显示这些问题也出现在P中。

Lots of interesting cryptographic systems (particularly in the public key setting) are secure based on the assumption that a computational problem is "hard", which generally means "at least as hard as any problem in NP". That is, many schemes are based on problems which we think are difficult to solve, and that if you can create an algorithm that solves them you could also use this algorithm to solve lots of other problems that we currently believe to be difficult.

许多有趣的密码系统（特别是在公钥设置中）基于计算问题是“硬”的假设是安全的，这通常意味着“至少与NP中的任何问题一样困难”。也就是说，许多方案都基于我们认为难以解决的问题，并且如果您可以创建一个可以解决这些问题的算法，那么您也可以使用此算法来解决许多其他我们目前认为很困难的问题。

The Cook-Levin theorem provides an interesting result in this direction: No problem in NP is any harder than SAT. What his means is that if I had an oracle (basically an algorithm that I can see the input/output of but none of the workings) that solved SAT, by asking it to solve cleverly constructed queries I could use it to solve any other NP problem. This made SAT the first example of an NP-complete problem. So, to show that a problem X is at least as hard as solving an NP problem (it is NP-hard), it suffices to show that if I could solve X, I could use it to solve SAT.

Cook-Levin定理在这个方向上提供了一个有趣的结果：在NP中没有问题比SAT更难。他的意思是，如果我有一个解决SAT问题的oracle（基本上是一种算法，我可以看到输入/输出但没有任何工作），通过要求它解决巧妙构造的查询，我可以使用它来解决任何其他NP问题。这使得SAT成为NP完全问题的第一个例子。因此，为了表明问题X至少与解决NP问题一样困难（这是NP难题），只要证明如果我能解决X，就可以用它来解决SAT。
