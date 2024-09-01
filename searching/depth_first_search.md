# Depth First Search
----

#### Definition
- An algorithm that searches a tree (or graph) by searching depth of the tree first, starting at the root.
- It traverses left down a tree until it cannot go further.
- Once it reaches the end of a branch it traverses back up trying the right child of nodes on that branch, and if possible left from the right children.
- When finished examining a branch it moves to the node right of the root then tries to go left on all it's children until it reaches the bottom.
- The right most node is evaluated last (the node that is right of all it's ancestors).
#### What you need to know
- Optimal for searching a tree that is deeper than it is wide.
- Uses a stack to push nodes onto.
- Because a stack is LIFO it does not need to keep track of the nodes pointers and is therefore less memory intensive than breadth first search.
- Once it cannot go further left it begins evaluating the stack.
#### Steps to follow
- DFS follows the following 3 steps:
1- Visit a node “S”.
2- Mark “S” as visited.
3- Recursively visit every unvisited node attached to “S”.
- Since DFS is of recursive nature, this can be implemented using stacks
#### Time Complexity
- Search: Depth First Search: O(|E| + |V|)
- E is number of edges
- V is number of vertices
- O(h) space complexity [worst case], where h is the maximal depth of your tree.
#### Breadth First Search Vs. Depth First Search
- The simple answer to this question is that it depends on the size and shape of the tree.
- For wide, shallow trees use Breadth First Search
- For deep, narrow trees use Depth First Search
#### Nuances
- Because BFS uses queues to store information about the nodes and its children, it could use more memory than is available on your computer. (But you probably won't have to worry about this.)
- If using a DFS on a tree that is very deep you might go unnecessarily deep in the search. See xkcd for more information.
- Breadth First Search tends to be a looping algorithm.
- Depth First Search tends to be a recursive algorithm.
- usually implemented using stack
- Explanation about time complexity for both dfs and bfs (https://stackoverflow.com/a/26551061/7015400)

#### DFS Implemenation

<details>
<summary>
Java Implementation
</summary>

```java
package tests;

import java.io.*;
import java.util.Iterator;
import java.util.LinkedList;
 
//Implementation of DFS in Java:
//https://www.interviewbit.com/tutorial/depth-first-search/#depth-first-search
class Graph
{
    private int numVertices;
    private LinkedList<Integer> adjLists[];
    private boolean visited[];
 
    Graph(int vertices)
    {
        numVertices = vertices;
        adjLists = new LinkedList[vertices];
        visited = new boolean[vertices];
        
        for (int i = 0; i < vertices; i++)
            adjLists[i] = new LinkedList<Integer>();
    }
 
    void addEdge(int source, int destination)
    {
        adjLists[source].add(destination);
    }
 
    void DFS(int vertex)
    {
        visited[vertex] = true;
        System.out.print(vertex + " ");
 
        Iterator itr = adjLists[vertex].listIterator();
        while (itr.hasNext())
        {
            int adj_node = (int) itr.next();
            if (!visited[adj_node])
                DFS(adj_node);
        }
    }
 
 
    public static void main(String args[])
    {
        Graph g = new Graph(4);
 
         g.addEdge(0, 1);
         g.addEdge(0, 2);
         g.addEdge(1, 2);
         g.addEdge(2, 3);
 
        System.out.println("Following is Depth First Traversal");
 
        g.DFS(2);
    }
}
```
</details>

<details>
<summary>
Python Implementation
</summary>

```python
# Python3 program to print DFS traversal
# from a given graph
from collections import defaultdict


# This class represents a directed graph using
# adjacency list representation
class Graph:

	# Constructor
	def __init__(self):

		# Default dictionary to store graph
		self.graph = defaultdict(list)

	
	# Function to add an edge to graph
	def addEdge(self, u, v):
		self.graph[u].append(v)

	
	# A function used by DFS
	def DFSUtil(self, v, visited):

		# Mark the current node as visited
		# and print it
		visited.add(v)
		print(v, end=' ')

		# Recur for all the vertices
		# adjacent to this vertex
		for neighbour in self.graph[v]:
			if neighbour not in visited:
				self.DFSUtil(neighbour, visited)

	
	# The function to do DFS traversal. It uses
	# recursive DFSUtil()
	def DFS(self, v):

		# Create a set to store visited vertices
		visited = set()

		# Call the recursive helper function
		# to print DFS traversal
		self.DFSUtil(v, visited)


# Driver's code
if __name__ == "__main__":
	g = Graph()
	g.addEdge(0, 1)
	g.addEdge(0, 2)
	g.addEdge(1, 2)
	g.addEdge(2, 0)
	g.addEdge(2, 3)
	g.addEdge(3, 3)

	print("Following is Depth First Traversal (starting from vertex 2)")
	
	# Function call
	g.DFS(2)
```
</details>

## Typical DFS Example:

- https://leetcode.com/problems/number-of-provinces/solution/

Given a 2d array:  [[1,1,0],[1,1,0],[0,0,1]]
You need to find the group of directly or indirectly connected cities. They are connected if they have 1. So in this case:

  0  1  2
0 [1,1,0]
1 [1,1,0]
2 [0,0,1]

Here, both 0 and 1 are connected while 2 is not connected.

Steps:

- In order to find the number of connected components in an undirected graph, one of the simplest methods is to make use of Depth First Search starting from every node. We make use of visited array of size `M`. This visited[i] element is used to indicate that the node has already been visited while undergoing a Depth First Search from some node.

- To undergo DFS, we pick up a node and visit all its directly connected nodes. But, as soon as we visit any of those nodes, we recursively apply the same process to them as well. Thus, we try to go as deeper into the levels of the graph as possible starting from a current node first, leaving the other direct neighbour nodes to be visited later on.

Example:

```
class Solution {
    public int findCircleNum(int[][] isConnected) {
        boolean[] visited = new boolean[isConnected.length];
        int count = 0;
        for(int i=0;i<isConnected.length;i++){
            if(!visited[i]){
                findProvince(visited,i,isConnected);
                count++;
            }
        }
        return count;
    }
    
    public void findProvince(boolean[] visited,int j, int[][] isConnected){
        for(int i=0;i<isConnected.length;i++){
            if(isConnected[j][i] == 1 && !visited[i]){
                visited[i] = true;
                findProvince(visited,j,isConnected);
            }
        }
    }
}
```

- Create visited array, then find which node is equal to 1 and call findProvince. Then loop and check if it's equal to 1 and not visited, then make it visited and recursively call again.