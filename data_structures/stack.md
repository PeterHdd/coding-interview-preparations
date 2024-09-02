# Stacks

---

## About

- A Stack is a collection of elements, with two principle operations: push, which adds to the collection, and pop, which removes the most recently added element.
- A peek operation may give access to the top without modifying the stack.
- The push and pop operations occur only at one end of the structure, referred to as the top of the stack. This data structure makes it possible to implement a stack as a singly linked list and a pointer to the top element.
- Last in, first out data structure (LIFO): the most recently added object is the first to be removed



Back buttons, undo functionality, and function calls in programming are usually implemented using stacks.

## Complexity

The time complexity of stack operations depends on the implementation of a stack. Some implementations use arrays or array lists, which mean that the operations have similar complexities to those of an array. Others use nodes and pointers or linked lists and therefore would have similar complexities.


|Operation|Complexity|
|---------|----------|
|Access   |O(n)      |
|Search   |O(n)      |
|Insert   |O(1)      |
|Delete   |O(1)      | 

In order to access an item or search for one we would have to traverse the linked list. Inserting an item will always happen from the top, so it will always happen in constant time.


## Graph

![](http://legacy.earlham.edu/~ltnguyen14/cs%20web/pics/stack.png) 


## Stack implementation


<details>
<summary> Java Implementation </summary>

```java
package tests;


public class Stack {
	private static class Node {
		private int data;
		private Node next;
		
		public Node(int data) {
			this.data = data;
		}
	}
	
	private Node top; // remove/add here
	
	public boolean isEmpty() { //if top is null then return true
		return top == null;
	}
	public int peek() { //check if top is null if not return the data
		return top.data;
	}
	public void push(int data) {
		Node node = new Node(data); //create new node
		node.next = top; // the new nodes points to the current top
		top = node; //the top will point to the newly added node
	}
	public int pop() {
		int data = top.data; //get the top data
		top = top.next; // here top will refer to the second node, thus the first will be removed
		return data;
	}
	

}
```

</details>

<details>
<summary>Python Implementation </summary>

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class Stack:
    def __init__(self):
        self.head = None

    def isempty(self):
        if self.head == None:
            return True
        else:
            return False

    def push(self, data):

        if self.head == None:
            self.head = Node(data)
        else:
            newnode = Node(data)
            newnode.next = self.head
            self.head = newnode

    # Remove element that is the current head (start of the stack)
    def pop(self):

        if self.isempty():
            return None

        else:
            poppednode = self.head
            self.head = self.head.next
            poppednode.next = None
            return poppednode.data

    # Returns the head node data
    def peek(self):

        if self.isempty():
            return None

        else:
            return self.head.data

    # Prints out the stack
    def display(self):

        iternode = self.head
        if self.isempty():
            print("Stack Underflow")
        else:
            while(iternode != None):
                print(iternode.data, end="")
                iternode = iternode.next
                if(iternode != None):
                    print(" -> ", end="")
            return


# Creating a stack
stack = Stack()

# Pushing elements onto the stack
stack.push(10)
stack.push(20)
stack.push(30)

# Displaying the stack
stack.display()

# Peeking at the top element
print("\nTop element:", stack.peek())

# Popping elements from the stack
print("Popped element:", stack.pop())
print("Popped element:", stack.pop())

# Displaying the updated stack
stack.display()


```

</details>