# Binary Search Tree (BST) [Java]
Data Structure

- A BST contains nodes and 2 pointers for each node

## Components of a BST
- Root: The root of a tree is the top most node of a tree
- Edge: Edge acts as a link between the parent node and the child node
- Leaf: A node that has no children
- Depth: The depth of a node is the distance from the root to the particular node that was passed from the BST
- Height: The height of the node is the distance from that node to the deepest node of the tree
- Height of the BST: The height of the tree is the maximum height of any node.

## Node class
A tree node contains:
- Data (the value that is passed in when a new node is created)
- A pointer to the nodes left child
- A pointer to the nodes right child

## Example Node class
```java
class Node
{
    int data;
    Node left, right;
    
    public Node(int val) 
    {
        data = val;
        left = right = null;
    }
}
```

## Example BST Class

```java
class BinaryTree 
{
    Node root; // From the Node class
    
    BinaryTree(int key) 
    {
        root = new Node(key);
    }
    
    //Default Constructor
    BinaryTree() 
    {
        root = null;
    }
}
```