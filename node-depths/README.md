# Node Depths

The distance between a node in a binary tree and the tree's root is called node's depth.
Write a function that takes a binary tree and return the sum of it's nodes' depths.
Each `BinaryTree` node has an integer `value`, a `left` child node, and a `right` child node. Children nodes can either be BinaryTree nodes themselves or `Node` / `Null`

### Sample input:
```
TREE:
        _____1____
       /          \
      2__        __3_
     /   \      /    \
    4     5    6      7
   / \
  8   9
```
### Sample output:

```sh
16
// The depth of the node with value 2 is 1.
// The depth of the node with value 3 is 1.
// The depth of the node with value 4 is 1.
// The depth of the node with value 5 is 1.
// Etc..
// Summing all og these depths yields 16.
```

### My solution:

#### 1/ Inductive reasoning:


##### (for level 0)
D0= 0
> root depth is zero

##### (for level 1)
level = 1
D(level)= level * N
> While is the number of child nodes: 
N in [0..2] and Node_left + Node_right => N
##### (for level 2)
level =2
D2(level)=D(level-1)+ D(level) + D(level) 
>summ of prevous n-1 plus the right and left: D(level-1)+ D_left(level) + D_right(level)
##### (for level 3)
level =3
D3(level)=D2(level-1)+ D(level) + D(level)
##### (for level 4)
level =4
D4(level)=D3(level-1)+ D(level) + D(level)

##### (for level n)
level = n
Dn(level)=Dn-1(level-1)+ D(level) + D(level)
##### (for level n+1)
level = n + 1
Dn+1(level+1)=Dn(level)+ D(level+1) + D(level+1)

#### 1/ recursion implementation:

```java
class Program {
  // Dn+1(l+1)=Dn(l)+ D(l+1) + D(l+1)
  public static int nodeDepths(BinaryTree root) {
    return  nodeDepths(root,1);
  }
	// recursion
  public static int nodeDepths(BinaryTree root,int level) {
    if(root == null) return 0;
    int n = getChildNodesNumber(root);
    return (level *n) + nodeDepths(root.left,level+1) + nodeDepths(root.right,level+1);
  }
	// number of child nodes
  public static int getChildNodesNumber(BinaryTree root) {
    if(root.left==null && root.right==null)
      return 0;
    if(root.left!=null && root.right!=null)
      return 2;
    return 1;
  }
  static class BinaryTree {
    int value;
    BinaryTree left;
    BinaryTree right;

    public BinaryTree(int value) {
      this.value = value;
      left = null;
      right = null;
    }
  }
}
```
