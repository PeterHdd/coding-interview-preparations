# Graphs

----

## Definition
- Graphs are non-linear data structures that can show any type of relationship. Many data structures fall under the parent category of graphs -- like linked lists and trees. 
- Graphs have nodes (also called vertices) and edges.
- The node holds the data and then the edges point to related nodes. There are two types of edges: directed and undirected. Directed edges point in a direction whereas undirected edges point both ways.
- A pair (x,y) is referred to as an edge, which communicates that the x vertex connects to the y vertex.
- A graph G(V,E) consists of two sets, a set of vertices (V), and a set of edges (E).

## What you need to know
- Any tree is also a graph.
- node or vertices - data in the graph
- Edges - connections between nodes.
- Directed - edges point in a direction.
- Undirected - edges point in both directions.
- Euler Path - path that visits each edge just once. A graph must have either zero or two vertices with an odd degree to have an euler path.
- cycle - circle made of edges.
- Tree is special form of graph i.e. minimally connected graph and having only one path between any two vertices.
- In graph there can be more than one path i.e. graph can have uni-directional or bi-directional paths (edges) between nodes
- Graphs are used to represent networks. The networks may include paths in a city or telephone network or circuit network
- Undirected Graph: In an undirected graph, nodes are connected by edges that are all bidirectional. For example if an edge connects node 1 and 2, we can traverse from node 1 to node 2, and from node 2 to 1.
- Directed Graph: In a directed graph, nodes are connected by directed edges – they only go in one direction. For example, if an edge connects node 1 and 2, but the arrow head points towards 2, we can only traverse from node 1 to node 2 – not in the opposite direction.
- To represent a graph we can either use Adjacency list or Adjacency matrix.
- To create an Adjacency list, an array of linked lists is used. The size of the array is equal to the number of nodes.A single index, array[i] represents the list of nodes adjacent to the ith node.
- An Adjacency Matrix is a 2D array of size V x V where V is the number of nodes in a graph. A slot matrix[i][j] = 1 indicates that there is an edge from node i to node j.
- Weighted: In a weighted graph, each edge is assigned a weight or cost. (https://www.hackerearth.com/practice/algorithms/graphs/graph-representation/tutorial/).
- Using a graph you can find a shortest path from one point to another. An example of graph is facebook friends, where each node represents a person, in the graph you can find the recommended friends of one person, by checking the mutual friends of that person:
```
P1 <--> P2 <––> P3
```
So here P2 is a friend of P1, and P3 is recommended to P1.

- Adjacency list consumes O(V+E) while matrix is O(V^2), so space wise list is better. Insertion is both O(1), deletion of an edge in matrix is O(1) while in list it is O(E).
- So basically in an adjacency list, you create an array of linked list equal to the number of vertices, for example V ={1,2,3,4} then list[0] = 1, list[1] = 2. If vertices 1 points to vertices 2 then in the list, list[1] will point to vertice 2..etc..
- The list size is equal to the number of vertex(n). So if vertex are equal to 4 then we will have 4 array of list.
- So each vertex will have its own list, so list[0] = 0 -> 1 -> 2 -> 3 (https://www.log2base2.com/data-structures/graph/adjacency-list-representation-of-graph.html)


Good examples of graphs in use are Facebook friends, Twitter following (which would be directed), or a map of Metro stops.

There are many ways to store a graph data structure. You can use pointers and nodes, or you could use an adjacency list or matrix.


## Example Graph
```
     A –→ B ←–––– C → D ↔ E
     ↑    ↕     ↙ ↑     ↘
     F –→ G → H ← I ––––→ J
           ↓     ↘ ↑
           K       L
```
Image from [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures/blob/master/itsy-bitsy-data-structures.js).

## Glossary

* **Edges** - connections between nodes.
* **Directed** - edges point in a direction.
* **Undirected** - edges point in both directions.
* **Euler Path** - path that visits each edge just once. A graph must have either zero or two vertices with an odd degree to have an euler path. 
* **cycle** - circle made of edges.


## Adjacency List Implementation

```java
package tests;

/* ===== ===== =====
Theory of Programming
Adjacency List with weight
GitHub - https://github.com/VamsiSangam/theoryofprogramming
Code Contributor - Vamsi Sangam
===== ===== ===== */

import java.util.Scanner;

class AdjacencyNode
{
    /**
     * vertex - destination vertex of the edge
     * weight - weight of the edge
     * next - next node of the linked list
     */
    int vertex, weight;
    AdjacencyNode next;

    public AdjacencyNode(int vertex, int weight) {
        this.vertex = vertex;
        this.weight = weight;
    }
}

public class AdjacencyListDemo
{
    public static void main(String[] args)
    {
        int vertices, edges, v1, v2, w;
        Scanner in = new Scanner(System.in);
        
        System.out.print("Enter the number of vertices - ");
        vertices = in.nextInt();
        System.out.print("Enter the number of edges - ");
        edges = in.nextInt();
        
        // Creating Adjacency List. Size is made |V| + 1 to
        // use the array by 1-indexing, for simplicity
        AdjacencyNode[] adjacencyList = new AdjacencyNode[vertices + 1];
        
        System.out.println("Enter " + edges + " edges. Three integers v1, v2, w -");
        
        for (int i = 0; i < edges; ++i) {
            // Scanning edge v1 -> v2 of weight 'w'
            v1 = in.nextInt();
            v2 = in.nextInt();
            w = in.nextInt();
            
            // Adding edge v1 -> v2
            adjacencyList[v1] = addEdge(adjacencyList[v1], new AdjacencyNode(v2, w));
            
            // To add edge v2 -> v1, uncomment line below
            // adjacencyList[v2] = addEdge(adjacencyList[v2], v1, w);
        }
        
        // Printing adjacency list
        print(adjacencyList);
        
        System.out.println("Input the edge to delete. Three integers v1, v2, w -");
        v1 = in.nextInt();
        v2 = in.nextInt();
        w = in.nextInt();
        
        adjacencyList[v1] = deleteEdge(adjacencyList[v1], new AdjacencyNode(v2, w));
        print(adjacencyList);
    }
    
    /**
     * Adds a new node in the linked list. Follows head insertion for O(1) performance.
     * 
     * @param oldHead head of the linked list to which new node is to be added
     * @param newEdge new edge to be added
     * @return new head of the linked list
     */
    public static AdjacencyNode addEdge(AdjacencyNode oldHead, AdjacencyNode newEdge)
    {
        // Add the new node to the start of linked list
        newEdge.next = oldHead;
        
        return newEdge;
    }
    
    public static AdjacencyNode deleteEdge(AdjacencyNode adjacencyList, AdjacencyNode edgeToBeRemoved)
    {
    	AdjacencyNode head = adjacencyList;
        
        // Checking if head is edgeToBeRemoved
        if (head != null && head.vertex == edgeToBeRemoved.vertex && head.weight == edgeToBeRemoved.weight) {
            return head.next;
        }
        
        AdjacencyNode trav = head;
        
        while (trav != null) {
        	AdjacencyNode travNext = trav.next;

            if (travNext != null) {
                // check of travNext is equal to edgeToBeRemoved

                if (travNext.vertex == edgeToBeRemoved.vertex && travNext.weight == edgeToBeRemoved.weight) {
                    // Remove travNext node
                    trav.next = travNext.next;
                    return head;
                }
            }
            
            trav = travNext;
        }
        
        return head;
    }
    
    public static void print(AdjacencyNode[] adjacencyList)
    {
        for (int i = 1; i < adjacencyList.length; ++i) {
        	AdjacencyNode trav = adjacencyList[i];
            
            System.out.print("adjacencyList[" + i + "] -> ");
            
            while (trav != null) {
                System.out.print(trav.vertex + "(" + trav.weight + ") -> ");
                trav = trav.next;
            }
            
            System.out.println("NULL");
        }
    }
}
```

## Another Implementation

```java
// Java code to demonstrate Graph representation
// using ArrayList in Java

import java.util.*;

class Graph {

    // A utility function to add an edge in an
    // undirected graph
    static void addEdge(ArrayList<ArrayList<Integer> > adj,
                        int u, int v)
    {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    // A utility function to print the adjacency list
    // representation of graph
    static void printGraph(ArrayList<ArrayList<Integer> > adj)
    {
        for (int i = 0; i < adj.size(); i++) {
            System.out.println("\nAdjacency list of vertex" + i);
            System.out.print("head");
            for (int j = 0; j < adj.get(i).size(); j++) {
                System.out.print(" -> "+adj.get(i).get(j));
            }
            System.out.println();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Creating a graph with 5 vertices
        int V = 5;
        ArrayList<ArrayList<Integer> > adj
                = new ArrayList<ArrayList<Integer> >(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        // Adding edges one by one
        addEdge(adj, 0, 1);
        addEdge(adj, 0, 4);
        addEdge(adj, 1, 2);
        addEdge(adj, 1, 3);
       addEdge(adj, 1, 4);
       addEdge(adj, 2, 3);
       addEdge(adj, 3, 4);

        printGraph(adj);
    }
}
```
- The adjacency list will represent a graph, it will contain an array of lists. The size of the array is equal to the number of vertices. Therefore if we have 4 vertices, then the size of the array will be 4. For example the above prints:

```
Adjacency list of vertex0
head -> 1 -> 4

Adjacency list of vertex1
head -> 0 -> 2 -> 3 -> 4

Adjacency list of vertex2
head -> 1 -> 3

Adjacency list of vertex3
head -> 1 -> 2 -> 4

Adjacency list of vertex4
head -> 0 -> 1 -> 3
```
- Each vertices will have it's own list. The list is done by adding edges, each edge contains two vertices (u,v).
- Adding an edge is done by inserting both of the vertices connected by that edge in each others list. For example, if an edge between (u, v) has to be added, then u is stored in v’s vector list and v is stored in u’s vector list.
- Deleting an edge: To delete edge between (u, v), u’s adjacency list is traversed until v is found and it is removed from it. The same operation is performed for v.




## Some Notes:

![Group 2](https://user-images.githubusercontent.com/29070108/136663906-cd7433f1-845d-41b6-8570-d49cda20058a.png)

So let's assume this graph. A graph can either be represented using adjacent matrix or adjacent list. So in a matrix it will look like this:

<img width="252" alt="Screen Shot 2021-10-09 at 6 13 34 PM" src="https://user-images.githubusercontent.com/29070108/136664031-8dba191c-45ca-41e9-8d6b-d90956fe49a7.png">

As you can see here, we add "1" everywhere we have a path or a connection. Since we don't have a circular connection (1 connected to itself for example) we add 0 on position (0,0). Since 1 is connected to 2, then we add 1 at position (1,2). Since this is a undirected graph then (2,1) is also connected.

In an adjacent list, it will be connected like the following:

<img width="788" alt="Screen Shot 2021-10-09 at 6 24 21 PM" src="https://user-images.githubusercontent.com/29070108/136664552-b41387a9-5001-4995-bd1e-2e74a26a77c5.png">

The list is represented using a linkedlist usually `LinkedList<List<Integer>>` or `Map<Integer, List<Integer>>`, this can be used in both BFS and DFS

- All graph questions are usually solved using either BFS or DFS, with some additional condition.
- If it's a graph and it's more than 2 elements per array ([[1,1,0],[1,1,0],[0,0,1]]), then you don't have to use `Map<Integer, List<Integer>>` to add in adjancy list. Use a boolean array visited, iterate and increment the answer (https://leetcode.com/problems/number-of-provinces/)
- If it's a directed graph then also dont use `Map<Integer, List<Integer>>`, try to use dfs to solve it normally.

### Differences:

- Matrix space complexity is O(|V|2), while list is O(|V|+|E|), since n the worst case, if a graph is connected O(V) is required for a vertex and O(E) is required for storing neighbours corresponding to every vertex.
- Insertion of vertex time complexity is O(|V|2) in matrix, while in list it's O(1) since it's linked list.
- Removing a vertex time complexty is O(|V|2) in matrix, while in list it's O(|V|+|E|).


