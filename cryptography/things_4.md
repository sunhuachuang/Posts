### [复杂度类P](https://bristolcrypto.blogspot.com/2014/10/52-things-number-4-complexity-class-p.html)

```
The Complexity Class P
复杂度类P
```

#### Section 1: Complexity and Big O Notation
#### 第一部分: 复杂度与大O表示法

We want to know how difficult a given task is for a computer to do in order to design efficient programs. The trouble is that the processing power of a computer varies massively depending on the hardware (e.g. see last week's '52 Things' blog). So we want a measure of the difficulty of a task that doesn't depend on the specific details of the machine performing the task. One way to do this is to bound the number of operations that a certain model of a computer would take to do it. This is called (time) complexity theory.

我们想知道为了设计高效的程序，计算机要完成的任务是多么困难。 问题在于计算机的处理能力因硬件而异。 所以我们想要衡量一个任务的难度，而这个任务并不依赖于机器执行任务的具体细节。 要做到这一点的一种方法是限制计算机的特定型号执行操作的次数。 这被称为（时间）复杂性理论。

Typically, though, the number of operations required will depend on the input to the task and may vary even with inputs of the same length. As a pertinent example, say we design a computer program which tells you whether or not an integer you input is prime. If we give as input the number 256, the program will probably output 'not prime' sooner than if we had given it the number 323 (even though they both have length 9 when written as binary integers, for example), since the first integer has a very small prime factor (2) and the second has larger factors (17 and 19). Therefore we usually opt for a worst-case analysis where we record the longest running time of all inputs of a particular length. So we obtain an algebraic expression t(n) that reflects the longest running time of all inputs of length n.

但是，通常情况下，所需的操作数量取决于任务的输入，即使输入的长度相同，也可能会有所不同。 作为一个相关的例子，假设我们设计了一个计算机程序，它告诉你你输入的整数是否为素数。 如果我们以256为输入，那么程序可能会比输入数字323更快地输出“not prime”（即使它们的长度为9时，例如写为二进制整数），因为第一个整数 有一个非常小的素因子（2），第二个有更大的因子（17和19）。 因此，我们通常选择最差情况下的分析，记录特定长度的所有输入的最长运行时间。 所以我们得到一个代数表达式t（n），它反映了长度为n的所有输入的最长运行时间。

Furthermore, when the input length n becomes very large, we can neglect all but the most dominant term in the expression and also ignore any constant factors. This is called asymptotic analysis; we assume n is enormous and ask roughly how many steps the model of computation will take to 'finish' when given the worst possible input of length n, writing our answer in the form O(t(n)). For example, if we find that our process takes 6n^3–n^2+1 steps, we write that it is O(n^3), since all other terms can be ignored for very large n.

此外，当输入长度n变得非常大时，我们可以忽略除表达式中最主要的术语之外的所有术语，也忽略任何常数因素。 这被称为渐近分析; 我们假设n是巨大的，并且当给定长度为n的最差可能输入时，计算模型将大致要求“完成”多少个步骤，以O（t（n））的形式写出我们的答案。 例如，如果我们发现我们的过程需要6n^3-n^2 + 1个步骤，我们写它是O（n^3），因为对于非常大的n，所有其他项可以被忽略。

#### Section 2: Turing Machines
#### 第二部分：图灵机器

Now we give the model that is most often used in the kind of calculations performed in Section 1. First, recall that an alphabet is a non-empty finite set and a string is a finite sequence of elements (symbols) from an alphabet. A language is simply a set of strings.

现在我们给出在第1节中进行的计算中最常用的模型。首先，回顾一下，字母表是一个非空的有限集，而字符串是字母表中元素（符号）的有限序列。 语言只是一组字符串。

A Turing machine models what real computers can do. Its 'memory' is an infinitely long tape. At any time, each square of the tape is either blank or contains a symbol from some specified alphabet. The machine has a tape head that can move left or right along the tape, one square at a time, and read from and write to that square. At first, the tape is all blank except for the leftmost n squares which constitute the input (none of which can be blank so that it is clear where the input ends). The tape head starts at the leftmost square, reads the first input symbol and then decides what to do next according to a transition function. The transition function depends on what it reads at the square it is currently on and the state that the machine is currently in (like a record of what it has done so far) and returns

- a new state
- another symbol to write to the square it is on (though this symbol might be the same as what was already written there)
- a direction to move in: left or right.

图灵机模拟真正的电脑可以做什么。它的“记忆”是一个无限长的磁带。在任何时候，磁带的每个方块都是空白的或包含某个指定字母表中的符号。机器有一个磁带头，可以沿着磁带向左或向右移动，一次一个方形，读取并写入该方形。首先，除了构成输入的最左边的n个正方形（其中没有一个可以是空白，以便清楚输入端在哪里）之外，磁带全部空白。磁带头从最左边的方块开始，读取第一个输入符号，然后根据转换函数决定下一步该做什么。转换函数取决于它在当前所在的平方上读取的内容以及机器当前处于的状态（如迄今所做的记录）并返回

- 一个新的状态
- 另一个符号写在它所在的正方形上（虽然这个符号可能与已经写在那里的符号相同）
- 向左或向右移动的方向。

The machine will continue to move one square at a time, read a symbol, evaluate the transition function, write a symbol and move again, until its state becomes some specified accept state or reject state.

机器将一次继续移动一个方块，读取符号，评估转换函数，写入符号并再次移动，直到其状态变为某个指定的接受状态或拒绝状态。

If the machine ends up in the accept state, we say it accepts its input. Similarly it may reject its input. In either case we say the machine halts on its input. But note that it may enter a loop without accepting or rejecting i.e. it may never halt. If a Turing machine accepts every string in some language and rejects all other strings, then we say the machine decides that language. We can think of this as the machine testing whether or not the input string is a member of the language. Given a language, if there is a Turing machine that decides it, we say the language is decidable.

如果机器处于接受状态，我们说它接受它的输入。 同样，它可能会拒绝其输入。 无论哪种情况，我们都会说机器停止输入。 但请注意，它可能会进入循环而不接受或拒绝，即它可能永不停止。 如果图灵机接受某种语言的每个字符串并拒绝所有其他字符串，那么我们说机器决定该语言。 我们可以认为这是机器测试输入字符串是否是该语言的成员。 给定一种语言，如果有一台图灵机来决定它，我们说这种语言是可以确定的。

The power of this model comes from the fact that a Turing machine can do everything that a real computer can do (this is called the Church-Turing thesis [2]). We define the time complexity class TIME(t(n)) to be the collection of all languages that are decidable by an O(t(n)) time Turing machine, then we turn computational problems into questions about language membership (is an input string a member of a certain language? e.g. does this string representing an integer belong to the language of strings representing prime integers?) and can partition computational problems into time complexity classes.

这个模型的强大之处在于图灵机可以完成真实计算机可以完成的任务（这被称为教会图灵论文[2]）。 我们将时间复杂性类TIME（t（n））定义为可由O（t（n））时间图灵机确定的所有语言的集合，然后将计算问题转化为有关语言成员关系的问题 字符串是某种语言的成员？例如，表示整数的字符串是否属于表示整数的字符串的语言？），并且可以将计算问题划分为时间复杂度类。

#### Section 3: The Complexity Class P
#### 第三部分：复杂度类P

Finally, we arrive at the purpose of this blog! If t(n)=n^k for some k>0 then O(t(n)) is called polynomial time. The complexity class P is the class of all languages that are decidable in polynomial time by a Turing machine. Since k could be very large, such Turing machines are not necessarily all practical, (let alone 'fast'!), but this class is a rough model for what can be realistically achieved by a computer. Note that the class P is fundamentally different to those languages where t(n) has n in an exponent, such as 2^n, which grow much, much faster as n increases – so fast that even if you have a decider for some language, you may find that the universe ends before it halts on your input!

最后，我们到达这个博客的目的！如果对于某个k> 0，t（n）= n ^ k，那么O（t（n））称为多项式时间。复杂度等级P是图灵机在多项式时间内可确定的所有语言的类。由于k可能非常大，所以这样的图灵机并不一定都是实用的（更不用说'快速'了！），但是这个类是计算机可以实现的粗略模型。请注意，类P与t（n）具有n的指数形式（如2 ^ n）的语言根本不同，后者随着n的增加而增长得更快，速度更快 - 即使您对某种语言有决定因素，你可能会发现宇宙在它停止输入之前就结束了！

We conclude with an example of a polynomial time problem. Suppose you have a directed graph (a set of nodes and edges where there is at most one edge between any pair of nodes and each edge has an arrow indicating a direction). Then if we encode the graph and the two nodes as a single string, we can form a language consisting of those strings representing a graph and two nodes such that it is possible to follow the edges from the first node and eventually arrive at the second. So a decider for this language will effectively answer the question of whether there is a path from the first node A to the second B, called the path problem, by accepting or rejecting the graph and nodes you input. We give a decider for this language and show that it decides in polynomial time.

- First put a mark on A.
- Scan all the edges of the graph. If you find an edge from a marked node to an unmarked node, mark the unmarked node.
- Repeat the above until you mark no new nodes.
- If B is marked, accept. Otherwise, reject.

我们以一个多项式时间问题的例子来结束。假设你有一个有向图（一组节点和边，其中任何一对节点之间至多有一条边，每条边都有一个指示方向的箭头）。然后，如果我们将图形和两个节点编码为一个单独的字符串，我们可以形成一个由代表一个图形和两个节点的字符串组成的语言，从而可以跟随第一个节点的边缘并最终到达第二个节点。因此，这种语言的决策者将通过接受或拒绝您输入的图和节点来有效地回答是否存在从第一个节点A到第二个B的路径，称为路径问题。我们给这个语言的决定因素，并表明它决定多项式时间。

- 首先在A上划一个标记。
- 扫描图形的所有边缘。如果您发现从标记节点到未标记节点的边缘，请标记未标记节点。
- 重复上述操作直到您不标记新节点。
- 如果B被标记，接受。否则，拒绝。

This process successively marks the nodes that are reachable from A by a path of length 1, then a path of length 2, and so on. So it is clear that a Turing machine implementing the above is a decider for our language. Now we consider the time complexity of this algorithm. If we couldn't do steps 1 and 4 in polynomial time, our machine would be terrible! So we focus on steps 2 and 3. Step 2 involves searching the input and placing a mark on one square, which is clearly polynomial time in the size of the input. Step 3 repeats step 2 no more times than the number of nodes, which is necessarily less than the size of the input (since the input must encode all the nodes of the graph) and is hence polynomial (in particular, linear) in the size of the input. Therefore the whole algorithm is polynomial time and so we say the path problem is in P.

该过程依次标记可从A到达长度为1的路径，然后是长度为2的路径的节点，以此类推。所以很明显，实现上述功能的图灵机是我们语言的决定者。现在我们考虑这个算法的时间复杂度。如果我们不能在多项式时间内执行步骤1和4，那么我们的机器会很糟糕！因此，我们将重点放在步骤2和步骤3.步骤2涉及搜索输入并在一个正方形上放置标记，该标记显然是输入大小的多项式时间。步骤3重复步骤2的次数不超过节点的数量，节点的数量必须小于输入的大小（因为输入必须对图的所有节点进行编码），因此其大小为多项式（特别是线性）的输入。因此整个算法是多项式时间，所以我们说路径问题在P中。

- [1] http://www.amazon.co.uk/Introduction-Theory-Computation-Michael-Sipser/dp/0619217642
- [2] http://en.wikipedia.org/wiki/Church%E2%80%93Turing_thesis
