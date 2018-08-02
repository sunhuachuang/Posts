### [处理器的区别](https://bristolcrypto.blogspot.com/2014/10/52-things-number-1-different-types-of.html)

```
1. What is the difference between the following?
    - general-purpose processor.
    - general-purpose processor with instruction-set extensions.
    - special-purpose processor (or co-processor).
    - An FPGA.

1. 以下几点有什么区别？
   - 通用处理器。
   - 带指令集扩展的通用处理器。
   - 专用处理器（或协处理器）。
   - 一个FPGA。
```

There is no strict definition of a general-purpose processor, however, it is widely accepted that a processor is general if it is Turing-complete. This captures any processor that is able to compute anything actually computable (i.e. can solve any problem a Turing machine can). I will not delve into the definition of a Turing machine but if I've already lost you then I would recommend brushing up on your Theory of Computation [1]. Note though that this definition has no concept of performance or instruction-set capabilities and, in fact, some researchers have gone through the trouble of proving that you may only need a single instruction to be Turing-complete [2]. In the context of modern processors, most programmable CPUs are considered general purpose.

对通用处理器没有严格的定义，但是，如果处理器是图灵完备的，则该处理器是普遍通用的。这捕获了能够计算任何实际可计算的任何处理器（即，可以解决图灵机可能遇到的任何问题）。 我不会深入研究图灵机的定义，但是如果你完全理解不了我说的东西的化，那么我会建议你刷一下你的计算理论[1]。 请注意，虽然这个定义没有任何性能或指令集功能的概念，事实上，一些研究人员经历了证明您可能只需要一条指令即可完成图灵完成的麻烦[2]。 在现代处理器的情况下，大多数可编程CPU被认为是通用的。

The cost of being general-purpose usually comes at a penalty in performance. Specifically, a general-purpose processor may be able to compute anything computable but, it will never excel at complex repeated tasks. Given a task that is repeated regularly on a general-purpose processor in a wide variety of applications, a processor designer may incorporate instruction-set extensions to the base micro-architecture to accommodate the task. Functionally, there may be no difference in the micro-architecture capabilities but practically there may be huge performance gains for the end-user.

通用性的成本通常会导致性能上的损失。具体来说，通用处理器可能能够计算任何可计算的值，但是，在复杂的重复任务中，它永远不会出类拔萃。 鉴于在各种应用中的通用处理器上定期重复的任务，处理器设计人员可将指令集扩展集成到基本微架构以适应任务。 在功能上，微架构能力可能没有区别，但实际上最终用户可能会获得巨大的性能收益。

As we're all cryptographers here, I will stick to a crypto example for instruction-set extensions. Consider a desktop machine with an AES encrypted disk. Any reads from secondary storage require a CPU interrupt to decrypt the data blocks before being cached. Given disk access from a cache miss is already considered terrible, add the decryption routine over the top and you have a bottleneck worth making you re-consider your disk encryption. It should be clear here that AES is our complex repeated task and given a general-purpose CPU with a simple instruction-set, we have no choice but to implement the decryption as a linear stream operations. Intel and AMD both recognised the demand for disk encryption and the penalty AES adds to secondary storage access and have (since circa 2010) produced the AES-NI x86 instruction-set extension to accelerate disk encryption on the their line of desktop CPUs.

由于我们都是密码技术人员，因此我将坚持使用指令集扩展的加密示例。考虑使用AES加密磁盘的台式机。从辅助存储的任何读取都需要CPU中断才能在缓存之前解密数据块。 考虑到从高速缓存未命中的磁盘访问已被认为是可怕的，请在顶部添加解密例程，并且存在一个值得您重新考虑磁盘加密的瓶颈。 这里应该清楚的是，AES是我们复杂的重复任务，并且通过一个具有简单指令集的通用CPU，我们别无选择，只能将解密作为线性流操作来实现。 英特尔和AMD都认识到磁盘加密的需求以及AES增加二级存储访问的损失，并且（自2010年以来）已经制定了AES-NI x86指令集扩展，以加速其台式机CPU系列上的磁盘加密。

If you want to fully accelerate any computation, the most optimal result will always be a special-purpose processor or an Application-specific integrated circuit (ASIC). Here we lose a significant portion of the flexibility granted by a general-purpose processor in exchange for performance gains. These types of processors are often tightly-coupled to a general-purpose processor, hence the term co-processor. Note, a co-processor may indeed be in the same package as a general-purpose processor but not necessarily integrated into the general-purpose architecture. Once again, if we turn to modern processor architectures, Intel and AMD have both integrated sound cards, graphics processors and DSP engines into their CPUs for some time now. The additional functionality is exposed via special-purpose registers and the co-processor treated as a separate component which the general-purpose processor must manage.

如果您想全面加速任何计算，最佳结果将始终是专用处理器或专用集成电路（ASIC）。 在这里，我们失去了通用处理器授予的灵活性的重要部分，以换取性能提升。 这些类型的处理器通常与通用处理器紧密耦合，因此称为协处理器。 请注意，协处理器可能确实与通用处理器在同一个封装中，但未必集成到通用架构中。 再一次，如果我们转向现代处理器架构，英特尔和AMD现在已经将声卡，图形处理器和DSP引擎集成到了他们的CPU中。 附加功能通过专用寄存器公开，协处理器视为通用处理器必须管理的独立组件。

Finally we turn to Field-Programmable Gate Arrays (FPGAs). The middle-ground between ASIC and general-purpose processors. If an application demands high-performance throughput but also requires (infrequent) modification then an FPGA is probably the answer. To understand how an FPGA works, consider a (very) large electronics breadboard with thousands of logic-gates and lookup tables (multiplexers attached to memory) placed all around the breadboard. If you describe an application as a set of gates and timing constraints then you can wire it together on the breadboard and produce a circuit that will evaluate your application. An FPGA affords the flexibility of being re-programmable whilst producing the dedicated logic to evaluate a target application. The key difference to a general-purpose program is how you design and build your application. In order to get the most out of the hardware you must describe the application as a set of hardware components and events using a hardware description language (Verilog or VHDL). This process is frequently used to prototype general-purpose and special-purpose processors on FPGAs before production. However, it is not without its drawbacks. Designing a program with low-level building blocks becomes very cumbersome for large applications. In addition, the energy consumption and hardware costs are generally higher in comparison to a general-purpose embedded IC. Recently, FPGA manufacturer Xilinx have begun shipping FPGAs with ARM general-purpose cores integrated within a single package [3]. This now makes FPGAs available to the ARM core as a flexible co-processor. As a result, you can build dedicated logic to evaluate your crypto primitives and hence accelerate cryptographic applications.

最后我们转向现场可编程门阵列（FPGA）。 ASIC和通用处理器之间的中间地带。如果一个应用需要高性能的吞吐量，但也需要（不频繁的）修改，那么FPGA可能就是答案。为了理解FPGA的工作原理，考虑一个（非常）大型的电子面包板，在面包板上放置数千个逻辑门和查找表（内存中的多路复用器）。如果您将应用程序描述为一组门和时序约束条件，那么您可以将它连接在面包板上，并生成一个评估应用程序的电路。 FPGA提供了重新编程的灵活性，同时生成用于评估目标应用的专用逻辑。与通用程序的主要区别在于您如何设计和构建您的应用程序。为了充分利用硬件，您必须使用硬件描述语言（Verilog或VHDL）将应用程序描述为一组硬件组件和事件。在生产之前，这个过程经常用于在FPGA上对通用和专用处理器进行原型设计。然而，这并非没有缺点。使用低级构建块设计程序对于大型应用程序来说非常麻烦。另外，与通用嵌入式IC相比，能耗和硬件成本通常较高。最近，FPGA制造商赛灵思公司已经开始提供集成在单个封装内的ARM通用内核的FPGA [3]。现在，这使得FPGA可以作为灵活的协处理器使用FPGA。因此，您可以构建专用逻辑来评估您的加密原语，从而加速加密应用程序。

In summary, general-purpose processors are capable of computing anything computable. Similarly for a general-purpose processor with instruction-set extensions and it may perform better in particular applications. A special-purpose (or co-processor) is very fast at a particular task but is unable to compute anything outside of that. An FPGA can be used to build all of the above hardware but sacrifices speed for flexibility over an ASIC solution.

总之，通用处理器能够计算任何可计算的内容。 类似地，对于具有指令集扩展的通用处理器，它在特定应用中可能表现更好。 特殊用途（或协处理器）在特定任务中速度非常快，但无法计算任何其他内容。 FPGA可用于构建所有上述硬件，但牺牲ASIC解决方案的灵活性。


- [1] http://www.amazon.co.uk/Introduction-Theory-Computation-Michael-Sipser/dp/0619217642
- [2] http://www.cl.cam.ac.uk/~sd601/papers/mov.pdf
- [3] http://www.xilinx.com/products/zynq-7000/extensible-virtual-platform.htm
