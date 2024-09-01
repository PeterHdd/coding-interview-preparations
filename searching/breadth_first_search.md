# Breadth First Search
----
#### Definition
- An algorithm that searches a tree (or graph) by searching levels of the tree first, starting at the root.
- Breadth First Search (BFS) is an algorithm for traversing or searching layerwise in tree or graph data structures.
- Can be used to find shortest path, or in Social Networking Websites we can find people with certain distance.
- The algorithm makes sure that every node is visited not more than once.
- It finds every node on the same level, most often moving left to right.
- While doing this it tracks the children nodes of the nodes on the current level.
- When finished examining a level it moves to the left most node on the next level.
- The bottom-right most node is evaluated last (the node that is deepest and is farthest right of it's level).
#### What you need to know
- Optimal for searching a tree that is wider than it is deep.
- Uses a queue to store information about the tree while it traverses a tree.
- Because it uses a queue it is more memory intensive than depth first search.
- The queue uses more memory because it needs to stores pointers
- Both BFS and DFS are used in graphs and binary tree. In binary tree and graph BFS is a level order traversal while DFS is a pre order traversal.
#### Steps to follow
- BFS follows the following 4 steps:
    1-  Begin the search algorithm, by knowing the key which is to be searched. Once the key/element to be searched is decided the searching begins with the root (source) first.
    2- Visit the contiguous unvisited vertex. Mark it as visited. Display it (if needed). If this is the required key, stop. Else, add it in a queue.
    3- On the off chance that no neighboring vertex is discovered, expel the first vertex from the Queue.
    4- Repeat step 2 and 3 until the queue is empty.
- The above algorithm is a search algorithm that identifies whether a node exists in the graph. We can convert the algorithm to traversal algorithm to find all the reachable nodes from a given node.
- If you check the code, we would have an adjacency list (a linked list having an array as each element), then we create another array that will contain all false values(boolean), and a queue, and we add the root node to the queue and mark it as visited `visited[s]=true;`. Then since the linkedlist contains an array, and each array will contain the adjancent vertices therefore we loop in the adjancent list and get the vertices next to the root, enqueue them and mark them as visited. Then we repeat again for other arrays.
- For time complexity explanation check: https://stackoverflow.com/a/26551061/7015400
- Regarding time complexity: Every node is visited once(enqueued once). Also, every edge (x,y) is "crossed" twice: one time when node y is checked from x to see if it i;s visited (if not visited, then y would be visited from x), and another time, when we back track from y to x. Therefore it's O(V+E)
- for visual of adjancy list(http://codingbison.com/data-structures-in-c/data-structures-in-c-adjacency-lists.html)
- An Example:
```
    A
   / \
  B   C
 /   / \
D   E   F
```
- A breadth first traversal would visit the node in this order: A, B, C, D, E, F
- usually implemented using queue.

#### Time Complexity
- Search: Breadth First Search: O(V + E)
- E is number of edges
- V is number of vertices
- Space complexity is O(|V|) as well - since at worst case you need to hold all vertices in the queue.


## BFS Implementation

<details>
<summary>
Java Implementation
</summary>

```java
package tests;

import java.io.*;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.Scanner; 
  
////BFS Implementation In Java
//https://www.interviewbit.com/tutorial/breadth-first-search/#breadth-first-search
// This class represents a directed graph using adjacency list 
// representation 
class Graph 
{ 
    private int V;   // No. of vertices 
    private LinkedList<Integer> adj[]; //Adjacency Lists 
  
    // Constructor 
    Graph(int v) 
    { 
        V = v; 
        adj = new LinkedList[v]; 
        for (int i=0; i<v; ++i) 
            adj[i] = new LinkedList(); 
    } 
  
    // Function which adds an edge from v -> w 
    void addEdge(int v,int w) 
    { 
        adj[v].add(w); 
    } 
  
    // Function which prints BFS traversal from a given source 's' 
    void BFS(int s) 
    { 
        // mark all vertices as false, (i.e. they are not visited yet)
        boolean visited[] = new boolean[V]; 
  
        // Create a new queue for BFS
        LinkedList<Integer> queue = new LinkedList<Integer>(); 
  
        // Mark the current node as visited and enqueue it 
        visited[s]=true; 
        queue.add(s); 
  
        while (queue.size() > 0) 
        { 
            // pop a vertex from queue and print it 
            s = queue.poll(); 
            System.out.print(s+" "); 
  
            //Traverse all the adjacent vertices of current vertex,
            //check if they are not visited yet, mark them visited and push them into the queue.
            Iterator<Integer> it = adj[s].listIterator(); 
            while (it.hasNext() == true) 
            { 
                int n = it.next(); 
                if (!visited[n]) 
                { 
                    visited[n] = true; 
                    queue.add(n); 
                } 
            } 
        } 
    } 
  

} 

class Main {
        // Driver method to Create and Traverse Graph
    public static void main(String args[]) 
    { 
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter Number of vertices");
        int vertices = sc.nextInt();
        
        Graph g = new Graph(vertices);
        
        System.out.println("Enter Number of edges");
        int edges = sc.nextInt();
        int i;
        
        int source, destination;
        System.out.println("Enter Source <space> Destination (0-indexing)");
        
        for(i = 0; i < edges; i++){
            source = sc.nextInt();
            destination = sc.nextInt();
            if(source >= vertices || destination >= vertices){
                System.out.println("Invalid Edge");
                i--;
            }
            
            g.addEdge(source, destination);
        }
        
        System.out.println("Enter starting vertex");
        int start = sc.nextInt();
        
        System.out.println("Following is Breadth First Traversal, starting from vertex " + start); 
  
        g.BFS(start); 
    } 
}
```

</details>

<details>
<summary>
Python Implementation
</summary>

```python
from collections import deque

# BFS from given source s
def bfs(adj, s, visited):
  
    # Create a queue for BFS
    q = deque()

    # Mark the source node as visited and enqueue it
    visited[s] = True
    q.append(s)

    # Iterate over the queue
    while q:
      
        # Dequeue a vertex from queue and print it
        curr = q.popleft()
        print(curr, end=" ")

        # Get all adjacent vertices of the dequeued 
        # vertex. If an adjacent has not been visited, 
        # mark it visited and enqueue it
        for x in adj[curr]:
            if not visited[x]:
                visited[x] = True
                q.append(x)

# Function to add an edge to the graph
def add_edge(adj, u, v):
    adj[u].append(v)
    adj[v].append(u)

# Example usage
if __name__ == "__main__":
  
    # Number of vertices in the graph
    V = 5

    # Adjacency list representation of the graph
    adj = [[] for _ in range(V)]

    # Add edges to the graph
    add_edge(adj, 0, 1)
    add_edge(adj, 0, 2)
    add_edge(adj, 1, 3)
    add_edge(adj, 1, 4)
    add_edge(adj, 2, 4)

    # Mark all the vertices as not visited
    visited = [False] * V

    # Perform BFS traversal starting from vertex 0
    print("BFS starting from 0: ")
    bfs(adj, 0, visited)
```
</details>


## Typical BFS Example:

- https://leetcode.com/problems/number-of-provinces/solution/

Given a 2d array: [[1,1,0],[1,1,0],[0,0,1]]
You need to find the group of directly or indirectly connected cities. They are connected if they have 1. So in this case:

  0  1  2
0 [1,1,0]
1 [1,1,0]
2 [0,0,1]

Here, both 0 and 1 are connected while 2 is not connected.

- In case of Breadth First Search, we start from a particular node and visit all its directly connected nodes first. After all the direct neighbours have been visited, we apply the same process to the neighbour nodes as well. Thus, we exhaust the nodes of a graph on a level by level basis.

- We make use of a visited array to keep a track of the already visited nodes. We increment the countcount of connected components whenever we need to start off with a new node as the root node for applying BFS which hasn't been already visited.

```
public class Solution {
    public int findCircleNum(int[][] M) {
        int[] visited = new int[M.length];
        int count = 0;
        Queue < Integer > queue = new LinkedList < > ();
        for (int i = 0; i < M.length; i++) {
            if (visited[i] == 0) {
                queue.add(i);
                while (!queue.isEmpty()) {
                    int s = queue.remove();
                    visited[s] = 1;
                    for (int j = 0; j < M.length; j++) {
                        if (M[s][j] == 1 && visited[j] == 0)
                            queue.add(j);
                    }
                }
                count++;
            }
        }
        return count;
    }
}
```
Create a queue and add the first element as visited then loop in the queue and remove the element and mark the element as visited. and loop again and add the elements.