### [我们如何将NP解释为可以在多项式时间内检验证明的一组定理？](https://bristolcrypto.blogspot.com/2014/11/52-things-number-6-how-can-we-interpret.html)

```
Q6 How can we interpret NP as the set of theorems whose proofs can be checked in polynomial time?
Q6 我们如何将NP解释为可以在多项式时间内检验证明的一组定理？
```

This question is very much a follow up question to the previous one. Last week Guy answered the question of 'What is meant by the complexity class NP?', while this week I will be answering the related question of 'How can we interpret NP as the set of theorems whose proofs can be checked in polynomial time?'.

这个问题是前一个问题的后续问题。 上个星期，Guy回答了“复杂类NP是什么意思”的问题，而本周我将回答相关问题“我们如何解释NP作为一组定理，其证明可以用多项式时间来检验？”。

Now to me this is a more intuitive definition of what it means for a problem to be in NP. Not only is it a more intuitive definition but it should (hopefully) also be clearer as to why this is a complexity class that is useful both for cryptography and the wider world. Now before we go into what we can use the class of problems for, the definition is as follows:

现在对我来说，这是一个更直观的定义，说明NP中的问题意味着什么。 它不仅是一个更直观的定义，而且它应该（希望）也更清晰，为什么这是一个对密码学和更广泛的世界都有用的复杂类。在我们进入我们可以使用的问题类之前，定义如下：

```
NP is the class of languages that have polynomial time verifiers.
NP是具有多项式时间验证器的语言类。
```

OK but what does this actually mean? Basically if we have an element x and we want to know if x∈L (where L is some NP language) we have a prover P which given x outputs a witness w, this may take exponential time to find w given x. Then if we give x and w to our verifier V, V can tell if x∈L in polynomial time.

好的，但这实际上意味着什么？基本上，如果我们有一个元素x，并且我们想知道是否x∈L（其中L是某种NP语言），我们有一个证明者P，它给出x输出证人w，这可能需要指数时间来找到给定的x。那么，如果我们将x和w给予我们的验证者V，那么V可以在多项式时间内判断x∈L。

This definition seems very different from the one given last week but they are in fact equivalent. Informally they are equivalent because the witness w can just be the sequence of decisions the NDT made at each branching point to show that x∈L. For a (slightly) more formal proof of their equalence [1] is a reasonable online source (with references to textbooks).

这个定义与上周给出的定义非常不同，但它们实际上是等价的。非正式地，它们是等价的，因为证人w可以是NDT在每个分支点做出的决定序列，以表明x∈L。对于一个（略）更正式的等式证明[1]是一个合理的在线来源（参考教科书）。

So why might this be useful in cryptography? Well essentially we have a class of languages which can take exponential time to check if you do not know a witness but with a witness it can be done in polynomial time. This has the 'feel' of a lot of cryptographic algorithms - take Encryption (formalisation to follow in future weeks blogs) for example; you want it to be exponentially hard to get the message from ciphertext without the key (similar to a witness) but with the key you want it to be efficient (polynomial time) to extract the message.

那么为什么这可能会在密码学中有用呢？基本上，我们有一类语言可以花费指数的时间来检查你是否不知道证人，但是证人可以在多项式时间内完成。这有很多加密算法的“感觉” - 例如，采用加密技术（未来几周的博客将采用正式化）;你希望它是指数级地难以从没有密钥的密文（类似于证人）获得密文的信息，但是希望它有效的密钥（多项式时间）来提取消息。

A warning: While it sounds like a good move to use an NP problem for cryptography it may not be as simple as it first appears. This is because languages are in NP based on the worse case complexity where as for encryption we need it to be hard on average. For example we may have an NP language which has one element that takes exponential time to solve but all others are really efficient to solve - this will not make a good basis for an encryption scheme because we want encryption to be secure for all messages not just one.

警告：虽然这听起来像是一个很好的举动来使用密码学的NP问题，但它可能并不像第一次出现那样简单。这是因为语言是基于最坏情况复杂度的NP，而对于加密我们需要它平均很难。例如，我们可能有一种NP语言，其中一种元素需要指数时间来解决，但其他所有解决方案都非常有效 - 这不会为加密方案奠定良好的基础，因为我们希望加密对所有消息都是安全的，而不仅仅是一。

Now I am aware that integer factorization isn't known to be NP-complete and isn't known to be in P (See Ryan's blog here for a description) but it makes for a nice example of the point I am trying to make about choosing your NP instances carefully. In general finding a factor of a number is easy (half of them are divisible by two!) but if we choose something sensible we can make it hard to factor. Let us focus on numbers of the form N=p⋅q for p,q prime (a.k.a numbers with only two proper factors). Now if either of these numbers is small then it is again easy, so we want the numbers to be of equal size (this is what we do for RSA). From this it is possible to build an encryption scheme over the top.

现在我意识到整数因子分解并不是NP完全的，并且不知道是在P中（请参阅Ryan的博客以获取描述），但它提供了一个很好的例子，说明了我正试图提出的观点仔细选择你的NP实例。一般来说，找出一个数字的因素很容易（其中一半可以被两个整除！）但是如果我们选择一些合理的东西，我们可以使其难以分解。让我们把注意力集中在p，q素数（只有两个适当因子的a.k.a数）的形式N =p⋅q的数字上。现在，如果这些数字中的任何一个都很小，那么它很容易，所以我们希望这些数字具有相同的大小（这是我们为RSA所做的）。由此可以在顶层建立一个加密方案。

- [1] - http://en.wikipedia.org/wiki/NP_(complexity)#Equivalence_of_definitions
