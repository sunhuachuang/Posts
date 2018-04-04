Our work is most similar to the SPECTRE protocol [8]. SPECTRE enjoys both high throughput and  fast  confirmation  times.  
It  uses  the  structure  of  the  DAG  as  representing  an  abstract  vote regarding the order between each pair of blocks. 
One caveat of SPECTRE is that the output of this pairwise ordering may not be extendable to a full linear ordering, due to possible Condorcet cycles. 
PHANTOM solves this issue and provides a linear ordering over the blocks of the DAG.
As such, PHANTOM can support consensus regarding any general computation, also known as Smart Contracts , which SPECTRE cannot. 
Indeed, in order for a computation or contract to be processed  correctly  and  consistently,  the  full  order  of  events  in  the  ledger  is  usually  required, and particularly the order of inputs to the contract.
PHANTOM’s linear ordering does not come without  cost—confirmation  times  are  mush  slower  than  those  in  SPECTRE.  
In  Section  7  we describe how the same system can simultaneously enjoy the best of both protocols.

我们的工作与SPECTER协议最相似[8]。 SPECTER拥有高吞吐量和快速确认时间。
它使用DAG的结构来表示关于每对块之间的顺序的抽象投票。
SPECTER的一个警告是，由于可能的Condorcet循环，这种成对排序的输出可能无法扩展到全线性排序。
PHANTOM解决了这个问题，并提供了DAG块的线性排序。
因此，PHANTOM可以支持关于任何一般计算的共识，也称为智能合同，而SPECTER不能。
事实上，为了正确和一致地处理计算或合同，通常需要分类账中事件的完整顺序，特别是合同输入的顺序。
PHANTOM的线性订购不会在没有成本确认的情况下比SPECTER中的时间慢得多。
在第7节中，我们描述了同一个系统如何同时享受这两种协议中最好的。
