### [计算和存储功率的不同形式因素](https://bristolcrypto.blogspot.com/2014/10/52-things-q3-computational-and-storage.html)

```
Computational and storage power of different form factors

Q3: Estimate the relative computational and storage capabilities of

    a smart-card
    a micro-controller (i.e. a sensor node)
    an embedded or mobile computer (e.g., a mobile phone or PDA)
    a laptop- or desktop-class computer.

Q3 估计以下设备的相对计算和存储能力
    - 一张智能卡
    - 微控制器（即传感器节点）
    - 嵌入式或移动计算机（例如，移动电话或PDA）
    - 一台笔记本电脑或台式电脑。
```

To measure the computational capability of a device we could assess the clock speed of its processors. This may be misleading if the processor enables some form of parallelism---two cores running at 2 GHz obviously possess more computational power than a single core running at 2 GHz, and so finding a direct quantitative measure is not a realistic expectation. For specific devices like general purpose graphics cards, often the total FLOPS (floating point operations per second) the device is capable of sustaining is reported (for either single or double precision arithmetic) but even this measure is not a particularly reliable choice when applied to any given problem---indeed, some services facilitate a comparison by benchmarking the performance of different devices on a variety of problem instances---see, for example, CompuBench. Fortunately the range of capabilities of the devices included in the question makes a sufficient answer less dependent on quantitative metrics.

为了测量设备的计算能力，我们可以评估其处理器的时钟速度。如果处理器支持某种形式的并行处理，这可能会产生误导 - 两个以2 GHz运行的内核显然拥有比以2 GHz运行的单内核更高的计算能力，因此找到一个直接的定量测量并不是一个现实的期望。对于像通用图形卡这样的特定设备，通常报告设备能够维持的FLOPS（每秒浮点运算）能力（无论是单精度算法还是双精度算法），但即使采用此方法，该度量也不是特别可靠的选择任何给定的问题---实际上，一些服务通过基准测试不同设备在各种问题实例上的性能来促进比较---例如参见CompuBench。幸运的是，问题中所包含设备的功能范围足以满足量化指标的要求。

A measure for the storage capabilities of each device is much simpler to find: we can simply compare the approximate number of bytes of information the device is capable of holding on permanent storage.

对每个设备的存储能力的衡量要简单得多：我们可以简单地比较设备能够保存在永久存储上的大致信息字节数。

A smart-card is the least computationally powerful device: obviously clock speeds vary for different implementations, but one might expect to see around a 20 MHz core speed. In terms of storage, a typical smart-card might have around 2 kilobytes (KiB) available.

智能卡是计算能力最低的设备：显然不同的实施方式的时钟速度会有所不同，但人们可能会预计会看到20 MHz左右的核心速度。在存储方面，典型的智能卡可能有大约2千字节（KiB）可用。

A microcontroller is "a small computer on a single integrated circuit containing a processor core, memory, and programmable input/output peripherals" [1]. The range of storage and compute capability available will vary significantly according to the exact definition of microcontroller, but taking the suggested sensor node as an example, a typical microcontroller is likely to have similar computational capabilities as a smart-card and slightly more storage available, perhaps in the order of a few KiB to a few megabytes (MiB).

微控制器是“包含处理器内核，存储器和可编程输入/输出外设的单个集成电路上的小型计算机”[1]。根据微控制器的确切定义，可用的存储和计算能力的范围会有很大差异，但以建议的传感器节点为例，典型的微控制器可能具有与智能卡相似的计算能力，也许是几个KiB到几兆字节（MiB）的顺序。

A mobile computer such as a mobile phone has significantly more storage and computing power, and the amount of power available is rapidly increasing over time. Taking the 2008 iPhone and the 2013 Nexus 5 phone as an example, the iPhone used a 412 MHz 32-bit RISC ARM core, and the Nexus 5 CPU used is a 2.3 GHz quad-core processor. In terms of storage, if we ignore the ability of some phones to use removable storage, then a high-end phone in 2013 might expect to provide in the order of 16 to 32 gigabytes (GiB) of storage.

诸如移动电话之类的移动计算机具有显着更多的存储和计算能力，并且随着时间的推移，可用的功率量正在迅速增加。以2008 iPhone和2013 Nexus 5手机为例，iPhone使用了412 MHz 32位RISC ARM内核，所用的Nexus 5 CPU为2.3 GHz四核处理器。在存储方面，如果我们忽略某些电话使用可移动存储的能力，那么2013年的高端手机可能会提供16至32千兆字节（GiB）的存储量。

Finally, most laptop or desktop class computers are likely to have more processing power than a mobile phone: the high-end Intel "Haswell" i7 4960K processor contains 4 cores each clocked at 4 GHz, and the AMD "Piledriver" FX-9590 CPU contains 8 cores at 4.7 GHz---note that a direct comparison between these two processors requires more than just assessing core counts and clock speeds! There are other factors that can affect the computing capabilities of a desktop or laptop computer---in particular, the addition of a graphics processing unit can, for certain problems, provide a large increase in performance. The storage capacity of a laptop or desktop can vary tremendously, but a typical amount of storage in a consumer machine might be between hundreds of gigabytes and several terabytes (TiB)---the largest single hard drive capacities are now around 8 TiB.

最后，大多数笔记本电脑或台式计算机的处理能力可能会高于手机：高端英特尔“Haswell”i7 4960K处理器包含4个核心，每个核心的时钟频率为4 GHz，AMD“Piledriver”FX-9590 CPU包含8个4.7 GHz内核 - 注意，这两个处理器之间的直接比较不仅仅需要评估内核计数和时钟速度！还有其他一些因素可能会影响台式机或笔记本电脑的计算能力 - 特别是，对于某些问题，添加图形处理单元可以大大提高性能。笔记本电脑或台式机的存储容量可能会有很大的差异，但消费机中的典型存储容量可能在数百千兆字节和几千兆字节（TiB）之间---最大的单个硬盘容量现在约为8千兆字节。

[1] https://en.wikipedia.org/wiki/Microcontroller

