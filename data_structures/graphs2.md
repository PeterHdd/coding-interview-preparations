## Disjoint Sets

- The disjoint set data structure is also known as union-find data structure and merge-find set. It is a data structure that contains a collection of disjoint or non-overlapping sets. The disjoint set means that when the set is partitioned into the disjoint subsets.
- Disjoint is mainly used in directed graph
- Disjoint set has 2 main operation, union and find. For example:
S1 = {1,2,3,4}
S2 = {5,6,7,8}
- Here both of those are not connected, so I can use the find operation to find in which set each number is.
- To perform union operation, you need to add an edge between the two sets. For example: (4,8)
- It is mainly used to detect a cycle in a graph.
- It is used to check if two vertices are connected or not.
- It has two important functions, find and union. The find function finds the root node of a given vertex. The union function unions two vertices and makes their root nodes the same.
- There are two implementations of disjoint sets, one of them is called quick find, in this case, the time complexity of the find function will be O(1). However, the union function will take more time with the time complexity of O(N).
- Implementation with Quick Union: compared with the Quick Find implementation, the time complexity of the union function is better. Meanwhile, the find function will take more time in this case.

## Thoery Example

Given: u = {1,2,3,4,5,6,7,8}

All the edges are connected to each other and you need to detect cycle. So, you need to implement find and union. So first we would have the following sets after performing find:

S1 = {1,2}
S2 = {3,4}
S3 = {5,6}
S4 = {7,8}

Now take the two edges (2,4), they are in two different sets, so perform union then you would have:
S5 = {1,2,3,4}

Now go to the other edge (2,5), perform union and you would have:

S6 = {1,2,3,4,5,6}
So now if you take (1,3), you would find them all in the same set which means this is a cycle. So now take (6,8) and you can see they are in different sets, so perform union:

S7 = {1,2,3,4,5,6,7,8}

## Quick Find
- Quick Find implementation of a Disjoint Set and cover its two basic operations along with their complexity: find and union

```java
// UnionFind.class
class UnionFind {
    private int[] root;

    public UnionFind(int size) {
        root = new int[size];
        for (int i = 0; i < size; i++) {
            root[i] = i;
        }
    }

    public int find(int x) {
        return root[x];
    }
		
    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            for (int i = 0; i < root.length; i++) {
                if (root[i] == rootY) {
                    root[i] = rootX;
                }
            }
        }
    }

    public boolean connected(int x, int y) {
        return find(x) == find(y);
    }
}

// App.java
// Test Case
public class App {
    public static void main(String[] args) throws Exception {
        UnionFind uf = new UnionFind(10);
        // 1-2-5-6-7 3-8-9 4
        uf.union(1, 2);
        uf.union(2, 5);
        uf.union(5, 6);
        uf.union(6, 7);
        uf.union(3, 8);
        uf.union(8, 9);
        System.out.println(uf.connected(1, 5)); // true
        System.out.println(uf.connected(5, 7)); // true
        System.out.println(uf.connected(4, 9)); // false
        // 1-2-5-6-7 3-8-9-4
        uf.union(9, 4);
        System.out.println(uf.connected(4, 9)); // true
    }
}
```

|Operation|Complexity|
|---------|----------|
|Union-find Constructor	   |O(N)      |
|Find   |O(1)      |
|Union   |O(n)      |
|Connected   |O(1)      | 

Space compelexity : O(n)

## Summary

- The main idea of a “disjoint set” is to have all connected vertices have the same parent node or root node, whether directly or indirectly connected. To check if two vertices are connected, we only need to check if they have the same root node.

- The two most important functions for the “disjoint set” data structure are the `find` function and the `union` function. The find function locates the root node of a given vertex. The union function connects two previously unconnected vertices by giving them the same root node. There is another important function named connected, which checks the “connectivity” of two vertices. The find and union functions are essential for any question that uses the “disjoint set” data structure.