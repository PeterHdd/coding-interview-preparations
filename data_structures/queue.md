# Queue

---

## About

- A Queue is a collection of elements, supporting two principle operations: enqueue, which inserts an element into the queue, and dequeue, which removes an element from the queue.
- By convention, the end of the sequence at which elements are added is called the back, tail, or rear of the queue, and the end at which elements are removed is called the head or front of the queue, analogously to the words used when people line up to wait for goods or services.
- The operation of adding an element to the rear of the queue is known as enqueue, and the operation of removing an element from the front is known as dequeue.
- Theoretically, one characteristic of a queue is that it does not have a specific capacity. Regardless of how many elements are already contained, a new element can always be added. It can also be empty, at which point removing an element will be impossible until a new element has been added again.
- Often including a peek or front operation that returns the value of the next element to be dequeued without dequeuing it(head element).
- First in, first out data structure (FIFO): the oldest added object is the first to be removed


Software queues are used in a lot of cases like real life queues -- they give service to the task that asked for it first. A printer, for example, usually prints the first job given to it and then queues up the others until it is their turn. Queues are also used for breadth-first searches where each vertex is traversed.

## Complexity
Some implementations use arrays or array lists, which mean that the operations have similar complexities to those of an array. Others use nodes and pointers or doubly linked lists and therefore would have similar complexities to those structures.

|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(1)      | 


![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/300px-Data_Queue.svg.png)


## Queue Implementation

```java
package tests;

/**
 * 
 * @author P.Haddad
 * QUEUE, FIFO: enqueue, which inserts an element into the queue, and dequeue, which removes an element from the queue.
 * At the head items are removed, at the tail items are added.
 */
public class Queue {
	private static class Node {
		private int data;
		private Node next;
		
		public Node(int data) {
			this.data = data;
		}
	}
	
	private Node head; // remove here
	private Node tail; // add here
	
	public boolean isEmpty() { //if head is null then return true
		return head == null;
	}
	public int peek() { //check if head is null if not return the data
		return head.data;
	}
	public void add(int data) {
		Node node = new Node(data);
		if(tail != null) {
			tail.next = node;
		}
		tail = node;
		if(head == null) {
			head = node;
		}
		
	}
	public int remove() {
		int data = head.data;
		head = head.next;
		if(head == null) {
			tail = null;
		}
		return data;
	}
}

```
