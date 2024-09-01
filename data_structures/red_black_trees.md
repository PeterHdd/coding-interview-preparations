## Red Black Tree
----

## Definition
- A red-black tree is a kind of self-balancing binary search tree where each node has an extra bit, and that bit is often interpreted as the colour (red or black).
- Red-Black tree is a self balancing BST while the BST can be non-balancing.
- When inserting or deleting, you have to either rotate the tree left or right to satisfy the rules. Always you have to insert red nodes.
- A treeset is of type red black tree.
- These colours are used to ensure that the tree remains balanced during insertions and deletions.
- The root node is black then the children node has to be one red and one black.

## What you need to know
- If a node is red then its children are black.
- Every node has a colour either red or black.
- The root of tree is always black.
- The null nodes are always black nodes, on the left and on the right side they should have the same number of black parent nodes to be balanced.
- There are no two adjacent red nodes (A red node cannot have a red parent or red child).
- Every path from a node (including root) to any of its descendant NULL node has the same number of black nodes.


## Complexity

|Operation|Complexity|
|---------|----------|
|Access   |O(logn)      |
|Search   |O(logn)        |
|Insert   |O(logn)       |
|Delete   |O(logn)      |


### Red black trees
![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/756px-Red-black_tree_example.svg.png)

## Red Black tree Implementation

```java
package tests;
import java.util.Scanner;

/**
 * 
 * @author P.Haddad
 * Red black tree is a self balancing BST, it has a red and a black colored node, the root node is always a black colored node.
 */
public class RedBlackTree {

    private final int RED = 0;
    private final int BLACK = 1;
    public String name = "asd";

    private class Node {

        int key = -1, color = BLACK;
        Node left = nil, right = nil, parent = nil;

        Node(int key) { //key is value
            this.key = key;
        }

		public Node() {
			// TODO Auto-generated constructor stub
		} 
    }

    private final Node nil = new Node(-1); 
    private Node root = nil;

    // print the nodes in the tree, first print left nodes, then root and then print right nodes
    public void printTree(Node node) {  
        if (node == nil) {
            return;
        }
        printTree(node.left);
        System.out.print(((node.color==RED)?"Color: Red ":"Color: Black ")+"Key: "+node.key+" Parent: "+node.parent.key+"\n");
        printTree(node.right);
    }

    // search for a node
    private Node findNode(Node findNode, Node node) {
        if (root == nil) { //check if root node is null
            return null;
        }

        if (findNode.key < node.key) { //check if the value of the node is less than the nodes in tree
            if (node.left != nil) { // if not null, meaning if there are left nodes
                return findNode(findNode, node.left); //call findNode again
            }
        } else if (findNode.key > node.key) { //chcek if the value of the node is greater than the node in tree
            if (node.right != nil) { // if not null, menaing if there are right nodes
                return findNode(findNode, node.right); //call findNode again
            }
        } else if (findNode.key == node.key) { //if equal meaning it's equal to the root
            return node; // return node
        }
        return null; //if doesnt exist return null
    }

    //insert a node in the tree
    private void insert(Node node) {
        Node temp = root;
        if (root == nil) { //check if root is null, meaning no nodes..
            root = node; //assign node to root
            node.color = BLACK; //assign black to root node
            node.parent = nil; //assign nil to parent node
        } else {
            node.color = RED; //if root is not null, then add a red colored node
            while (true) {
                if (node.key < temp.key) { //if the value of the new node less than the root
                    if (temp.left == nil) { //check if left is null
                        temp.left = node; //assign new node to left
                        node.parent = temp; //assign parent node to the new added left node
                        break;
                    } else {
                        temp = temp.left; //if not null, then assign
                    }
                } else if (node.key >= temp.key) { //same as left
                    if (temp.right == nil) {
                        temp.right = node;
                        node.parent = temp;
                        break;
                    } else {
                        temp = temp.right;
                    }
                }
            }
            fixTree(node); //here we call fixTree, because if we insert two red color after each other then it wont be a red black tree anymore
        }
    }

    //Takes as argument the newly inserted node
    private void fixTree(Node node) {
        while (node.parent.color == RED) { //check if the parent node of the newly added node is red
            Node uncle = nil; //assign uncle node to null
            if (node.parent == node.parent.parent.left) { //ex: if you have 2 reds and root node, then check if the parent of the red node is equal to itself,
            											//since node.parent.parent.left will give you the left node under the grandfather's node assuming we have 3 nodes
            	uncle = node.parent.parent.right; //assign right node to uncle

                if (uncle != nil && uncle.color == RED) { //check if uncle color is red and not null
                    node.parent.color = BLACK; //assign black color to parent node
                    uncle.color = BLACK; //assign black color to uncle
                    node.parent.parent.color = RED; //assign red to grandfather node (root node)
                    node = node.parent.parent; //assign grandfather to node
                    continue;
                } 
                if (node == node.parent.right) { //check if newly added node is equal to parent node on the right
                    //Double rotation needed
                    node = node.parent; //assign parent node to newly added node
                    rotateLeft(node); //rotate left
                } 
                node.parent.color = BLACK; //asign color of parent node to black
                node.parent.parent.color = RED; //assign color of rootnode to red
                //if the "else if" code hasn't executed, this
                //is a case where we only need a single rotation 
                rotateRight(node.parent.parent); //rotate right
            } else { //same as above but opposite positions
                uncle = node.parent.parent.left;
                 if (uncle != nil && uncle.color == RED) {
                    node.parent.color = BLACK;
                    uncle.color = BLACK;
                    node.parent.parent.color = RED;
                    node = node.parent.parent;
                    continue;
                }
                if (node == node.parent.left) {
                    //Double rotation needed
                    node = node.parent;
                    rotateRight(node);
                }
                node.parent.color = BLACK;
                node.parent.parent.color = RED;
                //if the "else if" code hasn't executed, this
                //is a case where we only need a single rotation
                rotateLeft(node.parent.parent);
            }
        }
        root.color = BLACK;
    }

    void rotateLeft(Node node) {
        if (node.parent != nil) {
            if (node == node.parent.left) {
                node.parent.left = node.right;
            } else {
                node.parent.right = node.right;
            }
            node.right.parent = node.parent;
            node.parent = node.right;
            if (node.right.left != nil) {
                node.right.left.parent = node;
            }
            node.right = node.right.left;
            node.parent.left = node;
        } else {//Need to rotate root
            Node right = root.right;
            root.right = right.left;
            right.left.parent = root;
            root.parent = right;
            right.left = root;
            right.parent = nil;
            root = right;
        }
    }

    void rotateRight(Node node) {
        if (node.parent != nil) {
            if (node == node.parent.left) {
                node.parent.left = node.left;
            } else {
                node.parent.right = node.left;
            }

            node.left.parent = node.parent;
            node.parent = node.left;
            if (node.left.right != nil) {
                node.left.right.parent = node;
            }
            node.left = node.left.right;
            node.parent.right = node;
        } else {//Need to rotate root
        	// it will rotate to the right, example parent which is black becomes root and previous root node becomes uncle.
            Node left = root.left;
            root.left = root.left.right;
            left.right.parent = root;
            root.parent = left;
            left.right = root;
            left.parent = nil;
            root = left;
        }
    }

    //Deletes whole tree
    void deleteTree(){
        root = nil;
    }
    
    //Deletion Code .
    
    //This operation doesn't care about the new Node's connections
    //with previous node's left and right. The caller has to take care
    //of that.
    void transplant(Node target, Node with){ 
          if(target.parent == nil){
              root = with;
          }else if(target == target.parent.left){
              target.parent.left = with;
          }else
              target.parent.right = with;
          with.parent = target.parent;
    }
    
    boolean delete(Node z){
        if((z = findNode(z, root))==null)return false;
        Node x;
        Node y = z; // temporary reference y
        int y_original_color = y.color;
        
        if(z.left == nil){
            x = z.right;  
            transplant(z, z.right);  
        }else if(z.right == nil){
            x = z.left;
            transplant(z, z.left); 
        }else{
            y = treeMinimum(z.right);
            y_original_color = y.color;
            x = y.right;
            if(y.parent == z)
                x.parent = y;
            else{
                transplant(y, y.right);
                y.right = z.right;
                y.right.parent = y;
            }
            transplant(z, y);
            y.left = z.left;
            y.left.parent = y;
            y.color = z.color; 
        }
        if(y_original_color==BLACK)
            deleteFixup(x);  
        return true;
    }
    
    void deleteFixup(Node x){
        while(x!=root && x.color == BLACK){ 
            if(x == x.parent.left){
                Node w = x.parent.right;
                if(w.color == RED){
                    w.color = BLACK;
                    x.parent.color = RED;
                    rotateLeft(x.parent);
                    w = x.parent.right;
                }
                if(w.left.color == BLACK && w.right.color == BLACK){
                    w.color = RED;
                    x = x.parent;
                    continue;
                }
                else if(w.right.color == BLACK){
                    w.left.color = BLACK;
                    w.color = RED;
                    rotateRight(w);
                    w = x.parent.right;
                }
                if(w.right.color == RED){
                    w.color = x.parent.color;
                    x.parent.color = BLACK;
                    w.right.color = BLACK;
                    rotateLeft(x.parent);
                    x = root;
                }
            }else{
                Node w = x.parent.left;
                if(w.color == RED){
                    w.color = BLACK;
                    x.parent.color = RED;
                    rotateRight(x.parent);
                    w = x.parent.left;
                }
                if(w.right.color == BLACK && w.left.color == BLACK){
                    w.color = RED;
                    x = x.parent;
                    continue;
                }
                else if(w.left.color == BLACK){
                    w.right.color = BLACK;
                    w.color = RED;
                    rotateLeft(w);
                    w = x.parent.left;
                }
                if(w.left.color == RED){
                    w.color = x.parent.color;
                    x.parent.color = BLACK;
                    w.left.color = BLACK;
                    rotateRight(x.parent);
                    x = root;
                }
            }
        }
        x.color = BLACK; 
    }
    
    Node treeMinimum(Node subTreeRoot){
        while(subTreeRoot.left!=nil){
            subTreeRoot = subTreeRoot.left;
        }
        return subTreeRoot;
    }
    
    public void consoleUI() {
        Scanner scan = new Scanner(System.in);
        while (true) {
            System.out.println("\n1.- Add items\n"
                    + "2.- Delete items\n"
                    + "3.- Check items\n"
                    + "4.- Print tree\n"
                    + "5.- Delete tree\n");
            int choice = scan.nextInt();

            int item;
            Node node;
            switch (choice) {
                case 1:
                    item = scan.nextInt();
                    while (item != -999) {
                        node = new Node(item);
                        insert(node);
                        item = scan.nextInt();
                    }
                    printTree(root);
                    break;
                case 2:
                    item = scan.nextInt();
                    while (item != -999) {
                        node = new Node(item);
                        System.out.print("\nDeleting item " + item);
                        if (delete(node)) {
                            System.out.print(": deleted!");
                        } else {
                            System.out.print(": does not exist!");
                        }
                        item = scan.nextInt();
                    }
                    System.out.println();
                    printTree(root);
                    break;
                case 3:
                    item = scan.nextInt();
                    while (item != -999) {
                        node = new Node(item);
                        System.out.println((findNode(node, root) != null) ? "found" : "not found");
                        item = scan.nextInt();
                    }
                    break;
                case 4:
                    printTree(root);
                    break;
                case 5:
                    deleteTree();
                    System.out.println("Tree deleted!");
                    break;
            }
        }
    }
    public static void main(String[] args) {
        RedBlackTree rbt = new RedBlackTree();
        rbt.consoleUI();
    }
}
/**
 * links: 
 * https://www.geeksforgeeks.org/red-black-tree-set-2-insert/
 * http://www.codebytes.in/2014/10/red-black-tree-java-implementation.html
 */
 ```