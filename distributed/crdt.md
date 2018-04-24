### CRDT
CRDT是Conflict-Free Replicated Data Types的缩写，直译的话即“无冲突可复制数据类型”。

[研究论文](https://hal.inria.fr/file/index/docid/555588/filename/techreport.pdf)

[代码实现库erlang](https://github.com/basho/riak_dt)

1. 定义了CRDT
2. 列举了CRDT的两种基本形式，即基于状态的CRDT与基于操作的CRDT。前者存储的是一个个的最终值，类似我们的例子，后者存储的是一个个的操作记录，类似于我们例子里面的推导过程
3. 界定了CRDT能满足最终一致性的边界条件。简单说，设计一个CRDT，只需要验证它是否满足这些边界条件，即可知道它是否能保持最终一致
4. 界定了两类CRDT在系统中应用时，需要的信息交换的边界条件。即回答怎样叫做“收集到足够多的信息”
5. 枚举了当前人类所知的CRDT，包含了计数器(counter)，寄存器(register)，集合(set)和图(graph)等几类
6. 在现实中应该如何应用CRDT，尤其是对于存储空间怎样进行回收的问题

