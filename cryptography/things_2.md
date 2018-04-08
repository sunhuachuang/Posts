### [多核处理器和矢量处理器有什么区别？](https://bristolcrypto.blogspot.com/2014/10/52-things-number-2-what-is-difference.html)

```
What is the difference between a multi-core processor and a vector processor ?
多核处理器和矢量处理器有什么区别？
```

What is parallel computing?

Before answering this question we first need to consider the conventional “serial” model of processing. Let's do so by imagining some problem we need to solve. The way serial computing solves this problem is by viewing it as a number of steps (instructions) which the processor deals with in sequential order. The processor deals with each of the instructions and then at the end, the answer comes out and the problem is solved. Whilst being a wonderful way of solving the problem it does however imply a bottleneck in the speed of solving it. Namely, the speed of the processor at executing the individual instructions. This is fine if the problem isn’t too large, but what happens when we have to deal with larger problems or want to compute things faster? Is there a way of increasing the speed of computation without the bottleneck of the speed of the processor?

The answer as you might have guessed is yes and it comes in the form of something called parallel computing. What parallel computing does to the problem we are trying to solve is to break it down into smaller problems, each of which can be computed separately at the same time. In this way, the problem is distributed over different processing elements which perform each of these different sub problems simultaneously, providing a potentially significant increase in speed of computation – the amount of speed up depends on the algorithm and can be determined by Amdahl's law [1]. So how does this all work? How can you process things in such a way as this? Well two solutions to the problem are multi-core and vector processors.

What is a multi-core processor?

A multi-core processor is a single computing component that carries out parallel computing by using multiple serial processors to do different things at the same time. The sub problems of the bigger problem discussed earlier are each solved by a separate processor allowing programs to be computed in parallel. It's like having multiple people working on a project where each person is given a different task to do, but all are contributing to the same project. This might take some extra organising to do, but the overall speed of getting the project completed is going to be faster.

What is a vector processor?

A vector processor is a processor that computes single instructions (as in a serial processor) but carries them out on multiple data sets that are arranged in one dimensional arrays (unlike a standard serial processor which operates on single data sets). The idea here is that if you are doing the same thing many times to different data sets in a program, rather than executing a single instruction for each piece of data why not do the instruction to all the sets of data once? The acronym SIMD (Single Instruction Multiple Data) is often used to denote instructions that work in this way.

What is the difference?

So that's the general idea, let's sum up with an example. Let's say we want roll 4 big stones across a road and it takes one minute to do each roll. The serial processor rolls them one by one and so takes four minutes. The multi core processor with two cores has two people to roll stones so each one rolls two stones, it takes two minutes. The vector processor gets a long plank of wood, puts it behind all four stones and pushes them all in one, taking one minute. The multi core processor has multiple workers, the vector processor has a way of doing the same thing to multiple things at the same time.

[1] http://en.wikipedia.org/wiki/Amdahl%27s_law（阿姆达尔定律）
