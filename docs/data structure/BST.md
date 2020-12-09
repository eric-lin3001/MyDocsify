1. BST is short for 'binary search tree'

```java
TreeNode parentNode;
TreeNode leftNode;
TreeNode rightNode;
```

特点：对于BST中的每个node，都必须满足parentNode>leftNode,parentNode<rightNode



2. Definition of HEIGHT:

   1) height of a BST: length of the longest path from the root down to leaf.

   2) height of a node: lenght of the longest path from the node down to leaf.

3. What is 'balance':

   the height of the tree is log(n).