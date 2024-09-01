# Linked Lists

---

## Definition
- Stores data with nodes that point to other nodes.
Nodes, at its most basic it has one datum and one reference (another node).
- A linked list chains nodes together by pointing one node's reference towards another node.
- In its most basic form, each node contains: data, and a reference (in other words, a link) to the next node in the sequence.
- The `head` of a list is its first node. The `tail` of a list may refer either to the rest of the list after the head, or to the last node in the list.
- In simple words, a linked list consists of nodes where each node contains a data field and a reference(link) to the next node in the list.
- Each element of the LinkedList has the reference(address/pointer) to the next element of the LinkedList.
- The tail node is a special node, where the next pointer is always pointing or linking to a null reference, indicating the end of the list.
- In memory, when you create a node, two blocks of memory wil be allocated, one block contains the data and the other block will contain the address of the next node. You always have a reference to the head node.

## What you need to know
- Designed to optimize insertion and deletion, slow at indexing and searching.
- **Doubly linked list** has nodes that also reference the previous node. The doubly linked list has overcome this limitation by providing an additional pointer that points to the previous node. With the help of the previous pointer, the doubly linked list can be traversed in a backward direction thus making insertion and deletion operation easier to perform. Therefore a double linked list has prev,data,next fields.
- **Circularly linked list** is simple linked list whose tail, the last node, references the head, the first node.
- **Stack**, commonly implemented with linked lists but can be made from arrays too.
    - Stacks are last in, first out (LIFO) data structures.
    - Made with a linked list by having the head be the only place for insertion and removal.
- **Queues**, too can be implemented with a linked list or an array.
    - Queues are a first in, first out (FIFO) data structure.
    - Made with a doubly linked list that only removes from head and adds to tail.
 - To understand it in memory, then check: https://www.youtube.com/watch?v=LYGbeWnYXd8&ab_channel=NesoAcademy, as you can see here head will point to the first address, and ptr will traverse and points to different address, when you add the new node to the last node then head will also contain that new node. That's because the last node which has 3 as data and address 3000 will now point to address 4000.
 - Also check https://www.youtube.com/watch?v=R9PTBwOzceo&ab_channel=NesoAcademy for an introduction




## Complexity

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(1)      | 

In order to access an item or search the list, you must traverse the whole thing. In order to insert or delete nodes, you only need to move the position of pointers.

### Singly linked list
![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Singly-linked-list.svg/408px-Singly-linked-list.svg.png)

### Doubly linked list
![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Doubly-linked-list.svg/610px-Doubly-linked-list.svg.png)

## Single Linked list implementation

```java
package tests;

/**
 * 
 * @author P.Haddad
 * LinkedList
 */
// Linked List contains a Node and each node will contain data and a reference to the next node
/**
 *         Node      
	+----+---------+     
	| data  | null |     
	+----+---------+  
 * 
 */

public class Node {
	Node next; // reference to next object in the sequence (if not referencing then null)
	int data; //data (int,string..)
	
	public Node(int data) {
		this.data = data;
	}
}


// Linked List class, will contain an instance variable of the class Node
 class LinkedList {
	Node head;
	
	// add data, first check if the head is null, if it is then create a new node with data and return. Else then the head is pointing to the 
	// current node, therefore create a while loop that will keep traversing until it reaches the last node (null) and assign next node
	// to be the current node.
	//
	// This method will add a new node at the end of the linked list
	public void append(int data) {
		if(head == null) { // check if the head node is null, if it is create a node and assign it to the head.
			head = new Node(data);
			return;
		}
		Node current = head; // assign head to the current node
		while(current.next != null) { // if the current node points to another node then enter the while loop, and assign current.next to current
			current = current.next;
		}
		current.next = new Node(data);
	}
	
	// this method will add a new node at the beginning
	public void prepend(int data) {
		Node newHead = new Node(data); //create a new head node
		newHead.next = head; //reference the current head node
		head = newHead; // assign the new head node to be the head node of the list
	}
	
	public void deleteWithValue(int data) {
		if(head == null) return; // if null return
		if(head.data == data) { // check if data that needs to be deleted is the head,if it is point the head to the next node.
			head = head.next;
			return;
		}
		Node current = head; //assign head node to current node
		while(current.next != null) { //iterate the linked list
			if(current.next.data == data) { //check if the next node's data is equal to the data passed
				current.next = current.next.next; // if it is equal then let the current node point to the node after it thus deleting the node that has the value passed
				return;
			}
			current = current.next;
		}
	}
	
	public void printList() {
		Node current = head;
		while(current.next != null) {
			System.out.println(current.data);
			current = current.next;
		}
	}
}
```

## Double Linked List implementation

```java
package tests;

public class DoublyLinkedList {  
	  
    //Represent a node of the doubly linked list  
  
    class Node{  
        int data;  
        Node previous;  
        Node next;  
  
        public Node(int data) {  
            this.data = data;  
        }  
    }  
  
    //Represent the head and tail of the doubly linked list  
    Node head, tail = null;  
  
    //addNode() will add a node to the list  
    public void addNode(int data) {  
        //Create a new node  
        Node newNode = new Node(data);  
  
        //If list is empty  
        if(head == null) {  
            //Both head and tail will point to newNode  
            head = tail = newNode;  
            //head's previous will point to null  
            head.previous = null;  
            //tail's next will point to null, as it is the last node of the list  
            tail.next = null;  
        }  
        else {  
            //newNode will be added after tail such that tail's next will point to newNode  
            tail.next = newNode;  
            //newNode's previous will point to tail  
            newNode.previous = tail;  
            //newNode will become new tail  
            tail = newNode;  
            //As it is last node, tail's next will point to null  
            tail.next = null;  
        }  
    }  
  
    //display() will print out the nodes of the list  
    public void display() {  
        //Node current will point to head  
        Node current = head;  
        if(head == null) {  
            System.out.println("List is empty");  
            return;  
        }  
        System.out.println("Nodes of doubly linked list: ");  
        while(current != null) {  
            //Prints each node by incrementing the pointer.  
  
            System.out.print(current.data + " ");  
            current = current.next;  
        }  
    }  
  
    public static void main(String[] args) {  
  
        DoublyLinkedList dList = new DoublyLinkedList();  
        //Add nodes to the list  
        dList.addNode(1);  
        dList.addNode(2);  
        dList.addNode(3);  
        dList.addNode(4);  
        dList.addNode(5);  
  
        //Displays the nodes present in the list  
        dList.display();  
    }  
}  
```
