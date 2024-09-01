# Trees

---

## About

- A recursive data structure
- In computer science, a tree is a widely used abstract data type that simulates a hierarchical tree structure, with a root value and subtrees of children with a parent node, represented as a set of linked nodes.
- A tree data structure can be defined recursively as a collection of nodes (starting at a root node), where each node is a data structure consisting of a value, together with a list of references to nodes (the "children"), with the constraints that no reference is duplicated, and none points to the root.
- A Tree is an undirected, connected, acyclic graph
- A tree has only one root node and many child node. If a child does not have any children then it is called Leaf node.
- The depth of a node is the number of edges from the node to the tree's root node. A root node will have a depth of 0.
- The height of a node is the number of edges on the longest path from the node to a leaf. A leaf node will have a height of 0.
- A balanced tree is a tree that have the left and right subtree balanced and the height only differs by one node maximum.
- A tree can be unbalanced which means you have to rotate, if the unbalance is in the left subtree then you do a right rotation, if the unbalance is in the left subtree then you do a left rotation. Usually, the median elements becomes the top element(root) or middle. You can do a combination of rotations. To do rotation, you need to add a temp Node that will let you rotate the tree.
- Rotation:
    - right child node, `right subtree => left rotation`
    - left child node, `left subtree => right rotation`
    - right child node, `left subtree => right left rotation`
    - left child node, `right subtree => left right rotation`

Trees have nodes and vertices without any cycles. They are also directed - the parents point down to the children rather than having bidirectional relationships. 

The most common tree is a binary tree - where where every node has at most two children.


## Glossary
* **Root** - the top node of the tree.
* **Child** - a node below the parent.
* **Parent** - a node above a child. Note - a node can be both a parent and a child!
* **Siblings** - nodes with the same parent.
* **Leaf** - a node with no children.
* **Branch** - a node with a child.
* **Edge** - Connection between nodes.


## Tree Visual
```
          A                     
        ↙   ↘              
      B       C                
    ↙  ↘
   D    E
```
