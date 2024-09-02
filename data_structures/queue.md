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

<details>
<summary> Java Implementation </summary>

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

</details>

<details>
<summary> Python Implementation </summary>

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class Queue:
    def __init__(self):
        self.front = None
        self.rear = None
        self.size = 0

    def is_empty(self):
        return self.front is None

    def enqueue(self, item):
        new_node = Node(item)
        if self.is_empty():
            self.front = self.rear = new_node
        else:
            self.rear.next = new_node
            self.rear = new_node
        self.size += 1

    def dequeue(self):
        if self.is_empty():
            raise IndexError("Queue is empty")
        item = self.front.data
        self.front = self.front.next
        self.size -= 1
        if self.front is None:
            self.rear = None
        return item

    def front_item(self):
        if self.is_empty():
            raise IndexError("Queue is empty")
        return self.front.data

    def get_size(self):
        return self.size

    def __str__(self):
        if self.is_empty():
            return "[]"
        current = self.front
        items = []
        while current:
            items.append(str(current.data))
            current = current.next
        return "[" + " <- ".join(items) + "]"

# Create a new queue
my_queue = Queue()

# Enqueue some items
my_queue.enqueue("Task 1")
my_queue.enqueue("Task 2")
my_queue.enqueue("Task 3")

# Display the queue
print("Queue:", my_queue)  # Output: Queue: ['Task 1' <- 'Task 2' <- 'Task 3']

# Check the size
print("Size:", my_queue.get_size())  # Output: Size: 3

# Check the front item
print("Front item:", my_queue.front_item())  # Output: Front item: Task 1

# Dequeue an item
dequeued_item = my_queue.dequeue()
print("Dequeued:", dequeued_item)  # Output: Dequeued: Task 1

# Display the updated queue
print("Updated queue:", my_queue)  # Output: Updated queue: ['Task 2' <- 'Task 3']

# Check if the queue is empty
print("Is empty?", my_queue.is_empty())  # Output: Is empty? False

# Dequeue remaining items
print(my_queue.dequeue())  # Output: Task 2
print(my_queue.dequeue())  # Output: Task 3

# Try to dequeue from an empty queue
try:
    my_queue.dequeue()
except IndexError as e:
    print("Error:", e)  # Output: Error: Queue is empty
```

</details>