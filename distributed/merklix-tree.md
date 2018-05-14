### 使用 Merklix Tree 进行分块验证 （Raidx Tree and Merkle Tree 结合）
[原始地址](https://www.deadalnix.me/2016/11/06/using-merklix-tree-to-shard-block-validation/)

[Merklix Tree](https://www.deadalnix.me/2016/09/24/introducing-merklix-tree-as-an-unordered-merkle-tree-on-steroid/)

#### Merkle Tree
![Merkle Tree](../static/Merkle-tree.png)

#### Radix Tree

#### Merklix Tree
无序的Merkle树

##### 新特性
1. 无论树以何种方式创建，最终的结果都是一样的
2. 插入和删除是ln（n）
3. 可以生成一个证明，证明一个元素包含在集合中而不产生集合

用一个Key（不是必要写出来的）去标记所有element在树中的位置。与Merkle不一样，这样的Key可以是分散的。通过使每个节点成为所有元素的子树，在它们的Key中具有共同的前缀，可以使用基数结构来存储元素。
