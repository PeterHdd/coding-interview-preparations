## Binary Tree
---

### Definition
- Is a tree like data structure where every node has at most two children.
- There is one left and right child node.
- A binary tree is a type of Tree, in which each node has 0 to 2 child nodes (left and right, which can be null).

### What you need to know
- Designed to optimize searching and sorting.
- A degenerate tree is an unbalanced tree, which if entirely one-sided, is essentially a linked list.
- They are comparably simple to implement than other data structures.
- Used to make binary search trees.
- A binary tree that uses comparable keys to assign which direction a child is.
- Left child has a key smaller than its parent node.
- Right child has a key greater than its parent node.
- There can be no duplicate node.
- Because of the above it is more likely to be used as a data structure than a binary tree.

### Binary Search Tree
- A binary tree is used to make a binary search tree. In BST, the left nodes are less than the root nodes which is also less than all of the right nodes.
- Good for searching since we know that right side is bigger than root.
- Insertion works just like finding an element, first if we have the number 19 we check if it is bigger than root, then it goes to the right then we check if 19 is bigger than the node in the right if not we go to the left one until we find an null node.
- You can have a balance BST and unbalance BST, if it's unbalance meaning the right side or the left side has more nodes than the other side, then insertion and finding will be `O(n)`. If it is balanced then insertion will be `O(logn)`.
- A binary search tree, sometimes called BST, is a type of binary tree which maintains the property that the value in each node must be greater than or equal to any value stored in the left sub-tree, and less than or equal to any value stored in the right sub-tree.
- Traversing, walking through a tree:
    - preorder traversal:
        - visit the root node first
        - visit the left node and then the right node
    - inorder traversal:
        - visit the left node then
        - visit the root node
        - visit the right node
    - postorder traversal:
        - visit the left node then
        - visit the right node
        - visit the root node

Usually in BST we use inorder traversal.

## Complexity

|Operation|Complexity|
|---------|----------|
|Access   |O(logn)      |
|Search   |O(logn)        |
|Insert   |O(logn)       |
|Delete   |O(logn)      | 

### Implementation of BST

<details>
<summary> Java Implementation </summary>

```java
package tests;

/**
 * 
 * @author P.Haddad
 * Binary search tree, contains a root node and a left and right nodes. The node without children is called leaf node.
 *  The root nodes have to be greater than the left node.
 */
public class BinarySearchTree {

}

class Node {
	Node left, right; //create left and right node
	int data; //the data that each node will have
	
	public Node(int data) {
		this.data = data;
	}
	
	public void insert(int value) { //insertion method.
		if(value <= data) { // check if value passed is less than data
			if(left == null) { //if left is null, then create a left node with value
				left = new Node(value);
			}
			else {
				left.insert(value); //if left is not null, then recursively call insert again.
			}
		} else {
			if(right == null) {
				right = new Node(value);
			} else {
				right.insert(value);
			}
		}
	}
	
	public boolean contains(int value) {
		if(value == data) {
			return true;
		} else if(value < data) {
			if(left == null) {
				return false;
			} else {
				return left.contains(value);
			}
		} else {
			if(right == null) {
				return false;
			} else {
				return right.contains(value);
			}
		}
	}
	
	public void printInOrderTraversal() { // inorder then it will print first left, then root, then right.
		if(left != null) {
			left.printInOrderTraversal();
		}
		System.out.println(data);
		if(right != null) {
			right.printInOrderTraversal();
		}
	}
}
```

</details>

<details>
<summary> Python Implementation </summary>

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

class BinarySearchTree:
    def __init__(self):
        self.root = None
    
    def insert(self, value):
        if not self.root:
            self.root = Node(value)
        else:
            self._insert_recursive(self.root, value)
    
    def _insert_recursive(self, current_node, value):
        if value < current_node.value:
            if current_node.left is None:
                current_node.left = Node(value)
            else:
                self._insert_recursive(current_node.left, value)
        elif value > current_node.value:
            if current_node.right is None:
                current_node.right = Node(value)
            else:
                self._insert_recursive(current_node.right, value)
    
    def search(self, value):
        return self._search_recursive(self.root, value)
    
    def _search_recursive(self, current_node, value):
        if current_node is None or current_node.value == value:
            return current_node
        if value < current_node.value:
            return self._search_recursive(current_node.left, value)
        return self._search_recursive(current_node.right, value)
    
    def inorder_traversal(self):
        result = []
        self._inorder_recursive(self.root, result)
        return result
    
    def _inorder_recursive(self, node, result):
        if node:
            self._inorder_recursive(node.left, result)
            result.append(node.value)
            self._inorder_recursive(node.right, result)

# Create a binary search tree
bst = BinarySearchTree()

# Insert some values
bst.insert(5)
bst.insert(3)
bst.insert(7)
bst.insert(1)
bst.insert(9)

# Search for a value
node = bst.search(7)
if node:
    print(f"Found: {node.value}")
else:
    print("Not found")

# Perform inorder traversal
print("Inorder traversal:", bst.inorder_traversal())
```

</details>