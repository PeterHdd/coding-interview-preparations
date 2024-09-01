## Tree Traversals
- Trees can be traversed in different ways. Following are the generally used ways for traversing trees.
- Depth First Traversals:
    - (a) Inorder (Left, Root, Right) : 4 2 5 1 3
    - (b) Preorder (Root, Left, Right) : 1 2 4 5 3
    - (c) Postorder (Left, Right, Root) : 4 5 2 3 1
- Breadth First or Level Order Traversal : 1 2 3 4 5
- Basically in level order traversal, first you go to the root then to the children on both sides then to the subchildren. It starts at the tree root, and explores all of the neighbor nodes at the present depth prior to moving on to the nodes at the next depth level.
- Check the image at the bottom for traversal: https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/.
- O(n) time complexity since we go through each node and O(n) space complexity since the stack space in worst case can contain the height of the binary tree.

## Implementation

```java
package tests;

//Java program for different tree traversals also known tree search

/* Class containing left and right child of current 
node and key value*/
class Node 
{ 
	int key; 
	Node left, right; 

	public Node(int item) 
	{ 
		key = item; 
		left = right = null; 
	} 
} 

class BinaryTree 
{ 
	// Root of Binary Tree 
	Node root; 

	BinaryTree() 
	{ 
		root = null; 
	} 

	/* Given a binary tree, print its nodes according to the 
	"bottom-up" postorder traversal. */
	void printPostorder(Node node) 
	{ 
		if (node == null) 
			return; 

		// first recur on left subtree 
		printPostorder(node.left); 

		// then recur on right subtree 
		printPostorder(node.right); 

		// now deal with the node 
		System.out.print(node.key + " "); 
	} 

	/* Given a binary tree, print its nodes in inorder*/
	void printInorder(Node node) 
	{ 
		if (node == null) 
			return; 

		/* first recur on left child */
		printInorder(node.left); 

		/* then print the data of node */
		System.out.print(node.key + " "); 

		/* now recur on right child */
		printInorder(node.right); 
	} 

	/* Given a binary tree, print its nodes in preorder*/
	void printPreorder(Node node) 
	{ 
		if (node == null) 
			return; 

		/* first print data of node */
		System.out.print(node.key + " "); 

		/* then recur on left sutree */
		printPreorder(node.left); 

		/* now recur on right subtree */
		printPreorder(node.right); 
	} 

	// Wrappers over above recursive functions 
	void printPostorder() {	 printPostorder(root); } 
	void printInorder() {	 printInorder(root); } 
	void printPreorder() {	 printPreorder(root); } 

	// Driver method 
	public static void main(String[] args) 
	{ 
		BinaryTree tree = new BinaryTree(); 
		tree.root = new Node(1); 
		tree.root.left = new Node(2); 
		tree.root.right = new Node(3); 
		tree.root.left.left = new Node(4); 
		tree.root.left.right = new Node(5); 

		System.out.println("Preorder traversal of binary tree is "); 
		tree.printPreorder(); 

		System.out.println("\nInorder traversal of binary tree is "); 
		tree.printInorder(); 

		System.out.println("\nPostorder traversal of binary tree is "); 
		tree.printPostorder(); 
	} 
} 
```

Tree Traversals:

inorder traversal:
```java
    public List<Integer> inorderTraversal(TreeNode root){
    List<Integer> list = new ArrayList<>();
        if(root == null){return list;}
        Stack<TreeNode> stack = new Stack<>(); 
        TreeNode curr = root;
        while(!stack.isEmpty() || curr != null){
            if(curr != null){
            stack.push(curr);
            curr = curr.left;
            } else {
                curr = stack.pop();
                list.add(curr.val);
                curr = curr.right;
            }
        }
        return list;
    }
```

preorder traversal:
```java
    public List<Integer> preorderTraversal(TreeNode root){
        if(root == null){return new ArrayList<>();}
         Stack<TreeNode> stack = new Stack<>();
         List<Integer> list = new ArrayList<>();
         stack.add(root);
        
        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            list.add(node.val);
            if(node.right != null){
                stack.push(node.right);
            }
            if(node.left != null){
                stack.push(node.left);
            }
        }
        return list;
    }
```

postorder traversal:
```java
 public List<Integer> postorderTraversal(TreeNode root){
    LinkedList<Integer> list = new LinkedList<>();
        if(root == null){return list;}
        Stack<TreeNode> stack = new Stack<>(); 
        stack.push(root);
        while(!stack.isEmpty()){
                TreeNode node = stack.pop();
                list.addFirst(node.val);
                if(node.left != null){
                    stack.push(node.left);
                }
                if(node.right != null){
                    stack.push(node.right);
                }
        }
        return list;
    }
```

## Difference between DFS and BFS
- Trees: they are graphs with no "cycles" so you won't have to keep track of the nodes you have visited during a search, to not visit them again. That's how BFS/DFS implementation for trees can be simplified. You can simply use a recursive function to implement DFS on trees because of this.