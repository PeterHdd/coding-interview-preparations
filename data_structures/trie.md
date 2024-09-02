## Trie
----

## Definition
- A trie, sometimes called a radix or prefix tree, is a kind of search tree that is used to store a dynamic set or associative array where the keys are usually Strings. No node in the tree stores the key associated with that node; instead, its position in the tree defines the key with which it is associated. All the descendants of a node have a common prefix of the String associated with that node, and the root is associated with the empty String.

## What you need to know
- A trie is a special tree that can compactly store strings.
So each node will contain a character to make up a full word, and at the end we use the * to say that this is the end of the word.
- It is great for word validation.
- So when building a trie, you need to see if a character is common in another word also.
- The worst case complexity for insertion and search for a trie is O(M) where M is the length of a key

## Trie Implementation

<details>
<summary> Java Implementation </summary>

```java
package tests;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
 
// A class to represent Trie
//https://www.techiedelight.com/implement-trie-data-structure-java/
class Trie
{
    // define alphabet size (26 characters for a - z)
    private static final int CHAR_SIZE = 26;
 
    private boolean isLeaf; //boolean flag to check if we reached the end of word or not
    private List<Trie> children = null;
 
    // Constructor
    Trie() {
        isLeaf = false;
        children = new ArrayList<>(Collections.nCopies(CHAR_SIZE, null));
    }
 
    // Iterative function to insert a string in Trie Data Structure
    public void insert(String key)
    {
        System.out.println("Inserting \"" + key + "\"");
 
        // start from root node
        Trie curr = this;
 
        // do for each character of the key
        for (char c: key.toCharArray())
        {
            // create a new Trie node if path does not exist
        	System.out.println(c - 'a'); ///if c= 't' then t - a = 116 - 97 = 19 thats why you do - 'a' because the size of the list is 26
            if (curr.children.get(c - 'a') == null)
                curr.children.set(c - 'a', new Trie());
 
            // go to the next node
            curr = curr.children.get(c - 'a');
        }
 
        // mark current node as leaf
        curr.isLeaf = true;
    }
 
    // Iterative function to search a key in Trie. It returns true
    // if the key is found in the Trie, else it returns false
    public boolean search(String key)
    {
        System.out.print("Searching \"" + key + "\" : ");
 
        Trie curr = this;
 
        // do for each character of the key
        for (char c: key.toCharArray())
        {
            // go to the next node
            curr = curr.children.get(c - 'a');
 
            // if string is invalid (reached end of path in Trie)
            if (curr == null)
                return false;
        }
 
        // return true if current node is a leaf node and we have reached
        // the end of the string
        return curr.isLeaf;
    }
}
 
public class MainTrie
{
    // Memory efficient implementation of Trie Data Structure in Java
    public static void main (String[] args)
    {
        // construct a new Trie node
        Trie head = new Trie();
 
        head.insert("techie");
        head.insert("techi");
        head.insert("tech");
 
        System.out.println(head.search("tech"));            // true
        System.out.println(head.search("techi"));           // true
        System.out.println(head.search("techie"));          // true
        System.out.println(head.search("techiedelight"));   // false
 
        head.insert("techiedelight");
 
        System.out.println(head.search("tech"));            // true
        System.out.println(head.search("techi"));           // true
        System.out.println(head.search("techie"));          // true
        System.out.println(head.search("techiedelight"));   // true
    }
}
```

</details>

<details>
<summary> Python Implementation </summary>

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True
    
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word
    
    def starts_with(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True

trie = Trie()
trie.insert("apple")
print(trie.search("apple"))  # True
print(trie.search("app"))    # False
print(trie.starts_with("app"))  # True

```
</details>