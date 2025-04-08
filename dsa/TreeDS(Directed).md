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

## Inplementation of Binary Tree
```java
class Node{
    int value;
    Node left,right;
}
```
1. Manual
2. Representation using Array
3. Representation using LinkedList
#### Representation of Array (works for compelete Binary tree)
Fill tree level by level

The root is at index 0.
For each node at index i:
Left child → 2 * i + 1  
Right child → 2 * i + 2  
Parent  woild be at → (i - 1)/2  
Traverse the array and build the tree recursively.

- Wasted of storage in arroy for Binary Tree

```java
public Node createTree(int[] arr, int i) {
  if (i >= arr.length) return null;

  Node node = new Node(arr[i]);
  node.left = createTree(arr, 2 * i + 1);  // Left child
  node.right = createTree(arr, 2 * i + 2); // Right child
  return node;
}
```
## Tree Traversal Methods
Traversal means visiting all nodes in a tree.  
1. Depth First serach (DFS)
Goes deep before exploring siblings.
- preorder traversal (root -> left -> right)
- InOrder traversal (left -> root -> right)
- PostOrder Traversal (left -> right -> root)
2. Breadth-First Search (BFS)
  Traverses level by level (also called Level Order Traversal.

#### Preorder traversal
```java
void preOrder(Node node){
  if(root.value==null)return;
  System.out.println(node.value);
  preOrder(node.left);
  preOrder(node.right);
}
```
#### inorder traversal
```java
void inorder(Node node){
  if(node.value==null)return;
  inorder(node.left);
  System.out.println(node.value);
  inorder(node.right);
}
```
#### postordertraversal
```java
void postorder(Node node){
  if(node.value==null)return;
  postorder(node.left);
  postorder(node.right);
  System.out.println(node.value);
}
```
#### Level order traversal
#### Q Construt a Binary tree frpm preorder & Inorder
#### Q Construt a Binary tree frpm postorder & Inorder
#### Q Construt a Binary tree frpm preorder & postorder
- It is not possible to construct uniquie binary tree.
- But unique Complete Binary Tree can be contructed.


**Q. Insert/Remove node from Tree data** 
Deletion:
case-1 0 child
case-2 1 child
case-3 2 child
  1. Inorder predecessor
     largest element in left tree
  2. Inorder successor
     Smallest element from right

