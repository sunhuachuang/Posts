### [处理器的区别](https://bristolcrypto.blogspot.com/2014/10/52-things-number-1-different-types-of.html)

```
1. 以下几点有什么区别？
   - 通用处理器。
   - 带指令集扩展的通用处理器。
   - 专用处理器（或协处理器）。
   - 一个FPGA。
```

 This is the first in a series of blog posts to address the list of '52 Things Every PhD Student Should Know' to do Cryptography. The set of questions has been compiled to give PhD candidates a sense of what they should know by the end of their first year - and as an early warning system to advise PhD students they should get out while they still can! In any case, we will be presenting answers to each of the questions over the next year and I have been volunteered for the (dubious) honour of blogging the very first 'thing'. The first topic is on computer architecture and is presented as the following question:

    What is the difference between the following?
    - A general-purpose processor.
    - A general-purpose processor with instruction-set extensions.
    - A special-purpose processor (or co-processor).
    - An FPGA.


There is no strict definition of a general-purpose processor, however, it is widely accepted that a processor is general if it is Turing-complete. This captures any processor that is able to compute anything actually computable (i.e. can solve any problem a Turing machine can). I will not delve into the definition of a Turing machine but if I've already lost you then I would recommend brushing up on your Theory of Computation [1]. Note though that this definition has no concept of performance or instruction-set capabilities and, in fact, some researchers have gone through the trouble of proving that you may only need a single instruction to be Turing-complete [2]. In the context of modern processors, most programmable CPUs are considered general purpose.

The cost of being general-purpose usually comes at a penalty in performance. Specifically, a general-purpose processor may be able to compute anything computable but, it will never excel at complex repeated tasks. Given a task that is repeated regularly on a general-purpose processor in a wide variety of applications, a processor designer may incorporate instruction-set extensions to the base micro-architecture to accommodate the task. Functionally, there may be no difference in the micro-architecture capabilities but practically there may be huge performance gains for the end-user.

As we're all cryptographers here, I will stick to a crypto example for instruction-set extensions. Consider a desktop machine with an AES encrypted disk. Any reads from secondary storage require a CPU interrupt to decrypt the data blocks before being cached. Given disk access from a cache miss is already considered terrible, add the decryption routine over the top and you have a bottleneck worth making you re-consider your disk encryption. It should be clear here that AES is our complex repeated task and given a general-purpose CPU with a simple instruction-set, we have no choice but to implement the decryption as a linear stream operations. Intel and AMD both recognised the demand for disk encryption and the penalty AES adds to secondary storage access and have (since circa 2010) produced the AES-NI x86 instruction-set extension to accelerate disk encryption on the their line of desktop CPUs.

If you want to fully accelerate any computation, the most optimal result will always be a special-purpose processor or an Application-specific integrated circuit (ASIC). Here we lose a significant portion of the flexibility granted by a general-purpose processor in exchange for performance gains. These types of processors are often tightly-coupled to a general-purpose processor, hence the term co-processor. Note, a co-processor may indeed be in the same package as a general-purpose processor but not necessarily integrated into the general-purpose architecture. Once again, if we turn to modern processor architectures, Intel and AMD have both integrated sound cards, graphics processors and DSP engines into their CPUs for some time now. The additional functionality is exposed via special-purpose registers and the co-processor treated as a separate component which the general-purpose processor must manage.

Finally we turn to Field-Programmable Gate Arrays (FPGAs). The middle-ground between ASIC and general-purpose processors. If an application demands high-performance throughput but also requires (infrequent) modification then an FPGA is probably the answer. To understand how an FPGA works, consider a (very) large electronics breadboard with thousands of logic-gates and lookup tables (multiplexers attached to memory) placed all around the breadboard. If you describe an application as a set of gates and timing constraints then you can wire it together on the breadboard and produce a circuit that will evaluate your application. An FPGA affords the flexibility of being re-programmable whilst producing the dedicated logic to evaluate a target application. The key difference to a general-purpose program is how you design and build your application. In order to get the most out of the hardware you must describe the application as a set of hardware components and events using a hardware description language (Verilog or VHDL). This process is frequently used to prototype general-purpose and special-purpose processors on FPGAs before production. However, it is not without its drawbacks. Designing a program with low-level building blocks becomes very cumbersome for large applications. In addition, the energy consumption and hardware costs are generally higher in comparison to a general-purpose embedded IC. Recently, FPGA manufacturer Xilinx have begun shipping FPGAs with ARM general-purpose cores integrated within a single package [3]. This now makes FPGAs available to the ARM core as a flexible co-processor. As a result, you can build dedicated logic to evaluate your crypto primitives and hence accelerate cryptographic applications.

In summary, general-purpose processors are capable of computing anything computable. Similarly for a general-purpose processor with instruction-set extensions and it may perform better in particular applications. A special-purpose (or co-processor) is very fast at a particular task but is unable to compute anything outside of that. An FPGA can be used to build all of the above hardware but sacrifices speed for flexibility over an ASIC solution.


[1] http://www.amazon.co.uk/Introduction-Theory-Computation-Michael-Sipser/dp/0619217642
[2] http://www.cl.cam.ac.uk/~sd601/papers/mov.pdf
[3] http://www.xilinx.com/products/zynq-7000/extensible-virtual-platform.htm
