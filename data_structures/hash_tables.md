# Hash Tables

## About
- is used to map data of an arbitrary size to data of a fixed size. The values returned by a hash function are called hash values, hash codes, or simply hashes. If two keys map to the same value, a collision occurs.
- In computing, a hash table (hash map) is a data structure that implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index, also called a hash code, into an array of buckets or slots, from which the desired value can be found.
- Basically the values are stored inside an array, each value will have an index. Then using a hash function we give it the key as an input and it will return the index of the value in the array.
Example:

```
keys: Paul, John
values: @ (index 0), & (index 1)
Hash(Paul) => returns index 0 which is value @
Hash(John) => returns index 1 which is value &
```

## What you need to know
- A hash functions are property of the data, be fast to compute, it should always return the same value which means if i use `Hash(Paul)` it should always give index 0, it should minimize collision.
- In Java, if you create an object and print it, then it will return the name of the class and the hashcode of that object.
- In Java, the number returned from the hashcode is just an identifier, this identifier will be used if we add the object inside a hashmap,hashset or hashtable. https://stackoverflow.com/a/16418809/7015400.
- In Java, if we override the `equals()` method then we must override the `hashcode()` method also. The equals method that is in the Object class will check if the objects are equals if they have the same reference in memory. A hash-based collections are organized like a sequence of buckets, and the hash code value of an object is used to determine the bucket where the object would be stored in the array, and the same hash code is used again to find the object’s position in the bucket. Therefore if we override the two methods, then object that contain the same value for the instance variables will be added in one bucket (last object will replace the first one in the bucket), instead of two buckets. https://www.techiedelight.com/why-override-equals-and-hashcode-methods-java/
- In Java, the keys and values are packaged together into a single object (Map.Entry), and that's what's stored in the array. Each entry in the main table / array is called a bucket. Each bucket contains a list of map entries (linked list).
- Hash Map: a hash map is a structure that can map keys to values. A hash map uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.
- In Java, even if the hashcode is the same but in memory address it won't be the same. Also the hashmap will have unique keys. (https://www.reddit.com/r/learnjava/comments/kcfo6b/hashmap_data_structure/).
- In Java, a hash function is specified as the composition of two functions: you first have a hashcode function and then a compression function. The compression function will let the index be in a specific range. https://www.cpp.edu/~ftang/courses/CS240/lectures/hashing.htm
- An algorithm converts an object, typically a string, to a number. Then the number is compressed according to the size of the table and used as an index.
- Different hash function types: direct hashing, modulo-division, folding, midsqaure, rotation, digit extraction, subtraction.
- modolus in math is the remainder when you divide two numbers. EX: 14 mod 12 is 2 since 14/12 = 1 with a remainder of 2.
- First step in hashing is using a hash function to calculate the index and the second step is collision-resolution if it occurs.
- modulo-division or modular hashing:
   - is used when hashing integers, we choose the array size M to be prime, and, for any positive integer key k, compute the remainder when dividing k by M. This function is very easy to compute (k % M, in Java), and is effective in dispersing the keys evenly between 0 and M-1.
 ```
 // refer to https://stackoverflow.com/questions/12684175/what-would-a-compress-method-do-in-a-hash-table
 // it can be key % size. Here it is hash since in java we have a compression function.
   int compress(int hash) { //not numBucket is the size of the array, hash is the returned number from the hashcode in java.
    return hash % numBuckets;
}

// hash function for strings.
int hashFunc(){ //R is a prime number (31 in java)
int hash = 0;
for (int i = 0; i < s.length(); i++)
    hash = (R * hash + s.charAt(i)) % M; //M is the size of the array.
}
```
- Java helps us address the basic problem that every type of data needs a hash function by requiring that every data type must implement a method called `hashCode()` (which returns a 32-bit integer). The implementation of `hashCode()` for an object must be consistent with `equals()`. That is, if `a.equals(b)` is true, then `a.hashCode()` must have the same numerical value as `b.hashCode()`. If the `hashCode()` values are the same, the objects may or may not be equal, and we must use equals() to decide which condition holds. (https://algs4.cs.princeton.edu/34hash/#:~:text=The%20most%20commonly%20used%20method,between%200%20and%20M%2D1.)
- The number 31 is used in string hash function because first it is a prime number and second n*31 is equivalent to (n << 5) - n and shifting is faster than multiplicaiton. https://stackoverflow.com/a/299748/7015400 https://stackoverflow.com/a/3613423/7015400
- In direct hashing: the key is the address without any algorithmic manipulation. Direct hashing is limited, but it can be very powerful because it guarantees that there are no synonyms and therefore no collision. Ex: key is equal to 2 then the hash function will return an index of 2.
- Digit extraction method: Using digit extraction selected digits are extracted from the key and used as the address. Ex: 379452 -> 394 121267 -> 112. Extract the first 3 digits, 394 would be the index.
- In Java, a prime number (31) is used for hash functions. A prime number is a number that cannot be made by another number, example 4 is a composite number since (2 * 2 is 4), 31 is prime. 8 is a composite number since 2 * 4 is 8, so any number that can be recievied only by doing * 1 is a prime. 31 is prime since only way to get it is by doing 31 * 1.
- The LinkedHashMap is just like HashMap with an additional feature of maintaining an order of elements inserted into it. HashMap provided the advantage of quick insertion, search, and deletion but it never maintained the track and order of insertion which the LinkedHashMap provides where the elements can be accessed in their insertion order. 
-  A hash collision can occur when one key returns the same index as another key. To solve a hash collision you can use a linkedlist under each index.
- load factor is (items of table)/(size of table). When the number of entries in the hash table exceeds the product of the load factor and the current capacity, the hash table is rehashed (that is, internal data structures are rebuilt) so that the hash table has approximately twice the number of buckets. The load factor represents at what level the HashMap capacity should be doubled.
- Separate Chaining: in separate chaining, each bucket is independent, and contains a list of entries for each index. The time for hash map operations is the time to find the bucket (constant time), plus the time to iterate through the list
- Open Addressing: in open addressing, when a new entry is inserted, the buckets are examined, starting with the hashed-to-slot and proceeding in some sequence, until an unoccupied slot is found. The name open addressing refers to the fact that the location of an item is not always determined by its hash value
- Seperate chaining is one of the strategies to deal with hash collision by maintiaining a data structure (linked list) to hold all different values which are hashed to a particular value. Basically if two items refer to the same index, then a linkedlist will be created in each bucket.
- Open addressing, or closed hashing, is a method of collision resolution in hash tables. With this method a hash collision is resolved by probing, example linear probing, double probing, quadratic probing.
- Linear probing: if two keys return the same index, then use the next available spot "a higher index". Also if you reach the end of the array then go to the front again. So if index 0,1,2 are already filled and you have another key that returns 0 then you need to put it in index 3.
- open addressing will fail more if you are using a bad hash function, if entries collide it will occupy other entries which will then collide more and so on which will require a larger hash table.

- In java, each object generates its own hashcode, therefore it is required to override both hashcode and equals. When you call `get()` for hashmap, first it will generate the `hashcode()` of the object, then it will get the index by calling the index method, then it will call the `equals()` method to check if the first element’s key with given key, if it is not then it checks second object. If we don't implement `hashcode()` but implement `equals()` then same objects will be in different buckets. If we don't implement `equals()` and only implement `hashcode()`, then they will have the same hashcode if they are the same object, but since we didn't override `equals()` then instead of the second object replacing the first, it will create a hash collision which is bad for time complexity. (https://stackoverflow.com/questions/2265503/why-do-i-need-to-override-the-equals-and-hashcode-methods-in-java).

## Complexity
|Operation|Complexity|
|---------|----------|
|Access   |O(1) -> O(n)|
|Search   |O(1) -> O(n)|
|Insert   |O(1) -> O(n)|
|Delete   |O(1) -> O(n)| 

The complexities of each of the above operations depend on the hashing function used. A perfect hashing function where keys and values are all known before runtime would run at O(1) for all of the above functions. Most are closer to O(n) in actual applications (like those above). 

## Graph

![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/58/Hash_table_4_1_1_0_0_1_0_LL.svg/480px-Hash_table_4_1_1_0_0_1_0_LL.svg.png)

![](https://www.cdn.geeksforgeeks.org/wp-content/uploads/HashingDataStructure-min.png)

### HashMap Implementation

```java
package tests;
// Java program to demonstrate implementation of our 
// own hash table with chaining for collision detection 
/**
 * implementing hashmap using seperate chaining to solve collisions.
 */
import java.util.ArrayList; 
//https://www.geeksforgeeks.org/implementing-our-own-hash-table-with-separate-chaining-in-java/
// A node of chains 
class HashNode<K, V> //hashnode class containing the key and the value
{ 
	K key; 
	V value; 

	// Reference to next node 
	HashNode<K, V> next; //reference to the next node since we are using a linked list

	// Constructor 
	public HashNode(K key, V value) 
	{ 
		this.key = key; 
		this.value = value; 
	} 
} 

// Class to represent entire hash table 
class Map<K, V>  
{ 
	// bucketArray is used to store array of chains 
	private ArrayList<HashNode<K, V>> bucketArray; 

	// Current capacity of array list 
	private int numBuckets; 

	// Current size of array list 
	private int size; 

	// Constructor (Initializes capacity, size and 
	// empty chains. 
	public Map() 
	{ 
		bucketArray = new ArrayList<>();  
		numBuckets = 10; //initial size of the array 10 buckets
		size = 0;  //size represents how many elements are in the array

		// Create empty chains 
		for (int i = 0; i < numBuckets; i++) //adding empty elements to array
			bucketArray.add(null); 
	} 

	public int size() { return size; } 
	public boolean isEmpty() { return size() == 0; } 

	// This implements hash function to find index 
	// for a key 
	private int getBucketIndex(K key)  //hash functions, which gets the hashcode and then uses modolo to return a index.
	{ 
		int hashCode = key.hashCode(); 
		int index = hashCode % numBuckets; 
		return index; 
	} 

	// Method to remove a given key 
	public V remove(K key) 
	{ 
		// 1. Apply hash function to find index for given key 
		int bucketIndex = getBucketIndex(key); 

		// Get head of chain 
		HashNode<K, V> head = bucketArray.get(bucketIndex); //get head , head is null if there is no element at that position

		// Search for key in its chain 
		HashNode<K, V> prev = null; 
		while (head != null) 
		{ 
			// If Key found 
			if (head.key.equals(key)) //if equal, get out of loop
				break; 

			// Else keep moving in chain 
			prev = head; 
			head = head.next; 
		} 

		// If key was not there 
		if (head == null) 
			return null; 

		// Reduce size 
		size--; //since u removed an element then decrement the size

		// Remove key 
		if (prev != null) 
			prev.next = head.next; 
		else
			bucketArray.set(bucketIndex, head.next); 

		return head.value; 
	} 

	// Returns value for a key 
	public V get(K key) 
	{ 
		// Find head of chain for given key 
		int bucketIndex = getBucketIndex(key);  //hash function
		HashNode<K, V> head = bucketArray.get(bucketIndex);  //head is null if there is no element at that index

		// Search key in chain 
		while (head != null) 
		{ 
			if (head.key.equals(key)) //check if key is equal to the key of the head, then return value
				return head.value; 
			head = head.next; //else move to the next node in the chain
		} 

		// If key not found 
		return null; 
	} 

	// Adds a key value pair to hash 
	//the array represents the hashtable
	// the hashnode is basically the nodes in the linkedlist in case of chaining.
	public void add(K key, V value) 
	{ 
		// Find head of chain for given key 
		int bucketIndex = getBucketIndex(key); //get the index using hash function
		HashNode<K, V> head = bucketArray.get(bucketIndex); //head is null if there is no element at that index
		//if there is already an element in that index, then head wont be null.

		// Check if key is already present 
		while (head != null) //if not null enter here
		{ //A map cannot contain duplicate keys; each key can map to at most one value.
			//If the map previously contained a mapping for the key, the old value is replaced by the specified value
			//therefore if the keys are equal then the value will only be replaced without chaining a linked list.
			if (head.key.equals(key)) //if the keys are equal
			{ 
				head.value = value; //assign the new value to the head
				return; //get out of the add method
			} 
			head = head.next; //if not equal then chain,head will point to the next node
		} 

		// Insert key in chain 
		size++;  //increment size
		head = bucketArray.get(bucketIndex); 
		HashNode<K, V> newNode = new HashNode<K, V>(key, value); //create new node
		newNode.next = head;  //assign head to the new node
		bucketArray.set(bucketIndex, newNode); 

		// If load factor goes beyond threshold, then 
		// double hash table size 
		if ((1.0*size)/numBuckets >= 0.7) 
		{ 
			ArrayList<HashNode<K, V>> temp = bucketArray; 
			bucketArray = new ArrayList<>(); 
			numBuckets = 2 * numBuckets; 
			size = 0; 
			for (int i = 0; i < numBuckets; i++) 
				bucketArray.add(null); 

			for (HashNode<K, V> headNode : temp) 
			{ 
				while (headNode != null) 
				{ 
					//We double the size of the array list and then recursively call add function on existing keys because,
					//in our case hash value generated uses the size of the array to compress the inbuilt JVM hash code we use ,so we need to fetch new indices for the existing keys.
					add(headNode.key, headNode.value); 
					headNode = headNode.next; 
				} 
			} 
		} 
	} 

	// Driver method to test Map class 
	public static void main(String[] args) 
	{ 
		Map<String, Integer>map = new Map<>(); 
		map.add("this",1 ); 
		map.add("coder",2 ); 
		map.add("this",4 ); 
		map.add("hi",5 ); 
		System.out.println(map.size()); 
		System.out.println(map.remove("this")); 
		System.out.println(map.remove("this")); 
		System.out.println(map.size()); 
		System.out.println(map.isEmpty()); 
	} 
} 
```

### Linear Probing Implementation

```java
package tests;
/**
 *   Java Program to implement Linear Probing Hash Table
 *   https://www.sanfoundry.com/java-program-implement-hash-tables-linear-probing/
 **/ 
 
import java.util.Scanner;
 
 
/** Class LinearProbingHashTable **/
class LinearProbingHashTable
{
    private int currentSize, maxSize;   //currentsize of hashtable, and maxsize    
    private String[] keys;   //array of keys
    private String[] vals;    //array of values
 
    /** Constructor **/
    public LinearProbingHashTable(int capacity) 
    {
        currentSize = 0;
        maxSize = capacity; //assign capacity to maxsize
        keys = new String[maxSize]; //add size to array of keys and values
        vals = new String[maxSize];
    }  
 
    /** Function to clear hash table **/
    public void makeEmpty()
    {
        currentSize = 0;
        keys = new String[maxSize];
        vals = new String[maxSize];
    }
 
    /** Function to get size of hash table **/
    public int getSize() 
    {
        return currentSize;
    }
 
    /** Function to check if hash table is full **/
    public boolean isFull() 
    {
        return currentSize == maxSize;
    }
 
    /** Function to check if hash table is empty **/
    public boolean isEmpty() 
    {
        return getSize() == 0;
    }
 
    /** Fucntion to check if hash table contains a key **/
    public boolean contains(String key) 
    {
        return get(key) !=  null;
    }
 
    /** Functiont to get hash code of a given key **/
    private int hash(String key) //hash function
    {
        return key.hashCode() % maxSize;
    }    
 
    /** Function to insert key-value pair **/
    public void insert(String key, String val)
    {                
        int tmp = hash(key); //hash function, if u get the same index, then it enters the do while and does this i = (i + 1) % maxSize; which will add the new element in a higher index.
        int i = tmp;
        do
        {
            if (keys[i] == null) //if it doesnt exists in the hashtable
            {
                keys[i] = key; //add key to the index
                vals[i] = val;//add value to the index
                currentSize++;//increment size by 1
                return; //get out of method
            }
            if (keys[i].equals(key)) //if the key at that index is the same as the key getting added, then replace the value
            { 
                vals[i] = val; 
                return; 
            }            
            i = (i + 1) % maxSize;            
        } while (i != tmp);       
    }
 
    /** Function to get value for a given key **/
    public String get(String key) 
    {
        int i = hash(key);
        while (keys[i] != null)
        {
            if (keys[i].equals(key))
                return vals[i];
            i = (i + 1) % maxSize;
        }            
        return null;
    }
 
    /** Function to remove key and its value **/
    public void remove(String key) 
    {
        if (!contains(key)) 
            return;
 
        /** find position key and delete **/
        int i = hash(key);
        while (!key.equals(keys[i])) 
            i = (i + 1) % maxSize;        
        keys[i] = vals[i] = null;
 
        /** rehash all keys **/        
        for (i = (i + 1) % maxSize; keys[i] != null; i = (i + 1) % maxSize)
        {
            String tmp1 = keys[i], tmp2 = vals[i];
            keys[i] = vals[i] = null;
            currentSize--;  
            insert(tmp1, tmp2);            
        }
        currentSize--;        
    }       
 
    /** Function to print HashTable **/
    public void printHashTable()
    {
        System.out.println("\nHash Table: ");
        for (int i = 0; i < maxSize; i++)
            if (keys[i] != null)
                System.out.println(keys[i] +" "+ vals[i]);
        System.out.println();
    }   
}
 
/** Class LinearProbingHashTableTest **/
public class LinearProbingHashTableTest
{
    public static void main(String[] args)
    {
        Scanner scan = new Scanner(System.in);
        System.out.println("Hash Table Test\n\n");
        System.out.println("Enter size");
        /** maxSizeake object of LinearProbingHashTable **/
        LinearProbingHashTable lpht = new LinearProbingHashTable(scan.nextInt() );
 
        char ch;
        /**  Perform LinearProbingHashTable operations  **/
        do    
        {
            System.out.println("\nHash Table Operations\n");
            System.out.println("1. insert ");
            System.out.println("2. remove");
            System.out.println("3. get");            
            System.out.println("4. clear");
            System.out.println("5. size");
 
            int choice = scan.nextInt();            
            switch (choice)
            {
            case 1 : 
                System.out.println("Enter key and value");
                lpht.insert(scan.next(), scan.next() ); 
                break;                          
            case 2 :                 
                System.out.println("Enter key");
                lpht.remove( scan.next() ); 
                break;                        
            case 3 : 
                System.out.println("Enter key");
                System.out.println("Value = "+ lpht.get( scan.next() )); 
                break;                                   
            case 4 : 
                lpht.makeEmpty();
                System.out.println("Hash Table Cleared\n");
                break;
            case 5 : 
                System.out.println("Size = "+ lpht.getSize() );
                break;         
            default : 
                System.out.println("Wrong Entry \n ");
                break;   
            }
            /** Display hash table **/
            lpht.printHashTable();  
 
            System.out.println("\nDo you want to continue (Type y or n) \n");
            ch = scan.next().charAt(0);                        
        } while (ch == 'Y'|| ch == 'y');  
    }
}
```
