## Fundamantal Tree DS (Directed Tree)
A tree is a hierarchical data structure that consists of nodes connected by edges.  
## Terminology
|Term|Definition|
|----|----------|
|Node| A single element in a tree|
|Root| The topmost node(starting point of tree)|
|Parent| A node that has child nodes|
|Child| A node that is a descendant of another node|
|Sibling| Nodes that share the same parent|
|Leaf| A node without children|
|Edge| A connection between two nodes|
|Height| The longest path from root to a leaf|
|Depth| Distance)no of node) of a node from the root|
|Level| Distance of a node from the root|
|Path| Sequence of cosucative edges between source to destination|
|Anccestor|Any predesessor node on the path from root to that node|
|Descendant|Any successor node on the path from that node to leaf node|
|Subtree| Containing node with all its descendeant|
|Degree of node| No. of children of that node|
|Degree of tree| Max. Degree of any node in that tree|
  
no. of nodes= (n-1) edge  
## Type of Trees
#### General Tree
A tree where a node have any number of children.  
#### Binary Tree
Each tree has at most 2 children.
- **Full Binary Tree** -Each node has 0 to 2 children.
- **Complete Binary Tree**: All levels are full except possible the last one.
  ```no. of leaf nodes=no. of internal nodes+1```
- **Perfect Binary Tree** All leaf nodes are at same level, and every node's has exactly two children.
- **Degenerate Binary Tree** : Each internal node has one child. Ex: Left skewed binary tree.
#### Binary Search Tree (BST)
- left subtree has smaller value then right sub tree

#### Balanced Trees
Tree where the height difference between subtrees is minimized.  
Examples:  
- **AVL Tree**: Self balancing BST (height diff<=1)
- **Red Black Tree**: Used in databased & Linux Kernel
#### Heap
A complete binary tree where
- **Max Heap**: Parent is greater than children.
- **Min Heap**: Parent is smaller than children.

## Binary Tree
Representation of Node
Node : [left-link , value , right-link];  

**Max number of nodes at level i = $2^i$**  
**Maximum number of node at height h = $2^{(h+1)} - 1$**   
**Minimum number of node at height h = h+1**  


