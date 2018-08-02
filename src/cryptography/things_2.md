### [多核处理器和矢量处理器有什么区别？](https://bristolcrypto.blogspot.com/2014/10/52-things-number-2-what-is-difference.html)

```
What is the difference between a multi-core processor and a vector processor ?
多核处理器和矢量处理器有什么区别？
```

What is parallel computing?

什么是并行计算？

Before answering this question we first need to consider the conventional “serial” model of processing. Let's do so by imagining some problem we need to solve. The way serial computing solves this problem is by viewing it as a number of steps (instructions) which the processor deals with in sequential order. The processor deals with each of the instructions and then at the end, the answer comes out and the problem is solved. Whilst being a wonderful way of solving the problem it does however imply a bottleneck in the speed of solving it. Namely, the speed of the processor at executing the individual instructions. This is fine if the problem isn’t too large, but what happens when we have to deal with larger problems or want to compute things faster? Is there a way of increasing the speed of computation without the bottleneck of the speed of the processor?

在回答这个问题之前，我们首先需要考虑传统的“串行”处理模型。让我们通过想象一些我们需要解决的问题来做到这一点。串行计算解决此问题的方式是将其视为处理器按顺序处理的若干步骤（指令）。处理器处理每条指令，最后答案出来，问题就解决了。虽然是解决问题的好方法，但它确实意味着解决问题的速度的瓶颈。即，处理器在执行单个指令时的速度。如果问题不是太大，这很好，但是当我们必须处理更大的问题或想要更快地计算事情时会发生什么？在没有处理器速度瓶颈的情况下，是否可以提高计算速度？

The answer as you might have guessed is yes and it comes in the form of something called parallel computing. What parallel computing does to the problem we are trying to solve is to break it down into smaller problems, each of which can be computed separately at the same time. In this way, the problem is distributed over different processing elements which perform each of these different sub problems simultaneously, providing a potentially significant increase in speed of computation – the amount of speed up depends on the algorithm and can be determined by Amdahl's law [1]. So how does this all work? How can you process things in such a way as this? Well two solutions to the problem are multi-core and vector processors.

您可能已经猜到的答案是肯定的，它以一种称为并行计算的形式出现。并行计算对我们试图解决的问题做的是将其分解成更小的问题，每个问题都可以同时单独计算。通过这种方式，问题分布在不同的处理单元上，这些单元同时执行这些不同的子问题中的每一个，提供了计算速度的潜在显着增加 - 加速的量取决于算法并且可以由Amdahl定律[1]。那么这是如何工作的？你如何以这种方式处理事物？那么问题的两个解决方案是多核和矢量处理器。

What is a multi-core processor?

什么是多核心处理器？

A multi-core processor is a single computing component that carries out parallel computing by using multiple serial processors to do different things at the same time. The sub problems of the bigger problem discussed earlier are each solved by a separate processor allowing programs to be computed in parallel. It's like having multiple people working on a project where each person is given a different task to do, but all are contributing to the same project. This might take some extra organising to do, but the overall speed of getting the project completed is going to be faster.

多核处理器是一个单一的计算组件，它通过使用多个串行处理器同时执行不同的事情来执行并行计算。前面讨论的更大问题的子问题每个都通过一个单独的处理器解决，允许程序并行计算。这就像有多个人在一个项目中工作，每个人都有不同的任务要做，但是所有人都参与了同一个项目。这可能需要一些额外的组织才能完成，但完成项目的总体速度将会更快。

What is a vector processor?

什么是矢量处理器？

A vector processor is a processor that computes single instructions (as in a serial processor) but carries them out on multiple data sets that are arranged in one dimensional arrays (unlike a standard serial processor which operates on single data sets). The idea here is that if you are doing the same thing many times to different data sets in a program, rather than executing a single instruction for each piece of data why not do the instruction to all the sets of data once? The acronym SIMD (Single Instruction Multiple Data) is often used to denote instructions that work in this way.

矢量处理器是一种计算单个指令（如串行处理器中的处理器）的处理器，但将它们传输到多维数据集中，这些数据集以一维阵列排列（不像标准串行处理器，它在单一数据集上运行）。这里的想法是，如果你对程序中的不同数据集多次执行相同的操作，而不是对每一块数据执行单条指令，为什么不对所有数据集执行一次指令呢？首字母缩略词SIMD（单指令多数据）通常用于表示以这种方式工作的指令。

What is the difference?

有什么不同？

So that's the general idea, let's sum up with an example. Let's say we want roll 4 big stones across a road and it takes one minute to do each roll. The serial processor rolls them one by one and so takes four minutes. The multi core processor with two cores has two people to roll stones so each one rolls two stones, it takes two minutes. The vector processor gets a long plank of wood, puts it behind all four stones and pushes them all in one, taking one minute. The multi core processor has multiple workers, the vector processor has a way of doing the same thing to multiple things at the same time.

所以这是总体思路，让我们总结一个例子。比方说，我们希望在路上滚动4块大石头，每分钟完成一个。串行处理器将它们一个接一个地滚动，因此需要四分钟。双核多核处理器有两个人滚动石头，每个人滚动两个石头，这需要两分钟。矢量处理器得到一块长木板，把它放在所有四块石头的后面，并将它们全部放入一块，花费一分钟。多核处理器有多个工作者，矢量处理器可以同时对多件事情做同样的事情。

[1] http://en.wikipedia.org/wiki/Amdahl%27s_law（阿姆达尔定律）
