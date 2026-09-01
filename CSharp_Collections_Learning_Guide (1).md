# C# Collections Learning Guide

---

## Table of Contents

- I. Direct Access Collections
- II. Sequential Access Collections
- III. Hierarchical Collections
- IV. Group Collections
- V. Best Practices & Tips

---

## I. Direct Access Collections

Direct access collections allow you to access elements by their index or key directly, without traversing other elements.

### 1.1 Array

#### Definition & Characteristics

- Fixed-size collection of elements of the same type
- Zero-indexed (first element at index 0)
- Direct memory access O(1) time complexity
- Mutable - elements can be modified

#### Code Example - Complete Operations

```csharp
// Declaring and initializing arrays
int[] numbers = new int[5];

// INSERT (assign values)
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;

// Array initialization with values
string[] fruits = { "Apple", "Banana", "Orange", "Grape", "Mango" };

// ACCESS (retrieve by index)
int firstNumber = numbers[0];      // 10
string secondFruit = fruits[1];    // "Banana"

// LOOKUP (find index of value - requires custom logic)
int searchValue = 20;
int indexOfValue = -1;
for (int i = 0; i < numbers.Length; i++)
{
    if (numbers[i] == searchValue)
    {
        indexOfValue = i;
        break;
    }
}
Console.WriteLine($"Found at index: {indexOfValue}"); // 1

// DELETE (replace with default value)
numbers[1] = 0; // Remove by setting to default

// Array length
int length = numbers.Length;
```

#### When to Use

Use arrays when you need a fixed-size collection with fast random access. Not ideal for frequent insertions/deletions.

---

### 1.2 String

#### Definition & Characteristics

- Immutable sequence of characters
- Zero-indexed collection
- Each character can be accessed by index
- Reference type in .NET

#### Code Example - Complete Operations

```csharp
// String declaration
string message = "Hello, C#!";

// INSERT (strings are immutable - create new string)
string insert = message.Insert(5, " beautiful");  // "Hello beautiful, C#!"
string concatenate = message + " Welcome!";        // "Hello, C#! Welcome!"

// ACCESS (retrieve by index)
char firstChar = message[0];    // 'H'
char lastChar = message[message.Length - 1]; // '!'

// LOOKUP (find position of substring)
int indexOfC = message.IndexOf("C#");  // 7
bool contains = message.Contains("Hello");  // true

// DELETE (remove substring - create new string)
string delete1 = message.Remove(7, 3);  // "Hello, !"
string delete2 = message.Replace("C#", "");  // "Hello, !"

// String properties and methods
int length = message.Length;
string upper = message.ToUpper();
string lower = message.ToLower();
```

#### When to Use

Use strings for text data. Remember that strings are immutable - every modification creates a new string. Use StringBuilder for frequent modifications.

---

### 1.3 Structure (Custom Collections)

#### Definition & Characteristics

- User-defined composite data type
- Combines multiple fields of different types
- Value type (stored on stack)
- Direct field access

#### Code Example - Complete Operations

```csharp
// Define a struct
public struct Point
{
    public int X;
    public int Y;

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }
}

// INSERT - Create and assign struct values
Point p1 = new Point { X = 10, Y = 20 };
Point p2 = new Point(15, 25);

// Array of structs for multiple insertions
Point[] points = new Point[5];
points[0] = new Point { X = 0, Y = 0 };
points[1] = new Point { X = 10, Y = 20 };
points[2] = new Point { X = 20, Y = 30 };

// ACCESS - Retrieve struct values
int xCoordinate = p1.X;  // 10
int yCoordinate = p1.Y;  // 20
int secondPointX = points[1].X;  // 10

// LOOKUP - Search for specific point
bool isPointExists(Point[] pointArray, int x, int y)
{
    foreach (var p in pointArray)
    {
        if (p.X == x && p.Y == y)
            return true;
    }
    return false;
}

bool found = isPointExists(points, 10, 20);  // true
bool notFound = isPointExists(points, 99, 99);  // false

// DELETE - Remove by replacing with default or clearing
points[0] = default(Point);  // Sets to (0, 0)
// Or shift array elements to remove an entry
Point[] newPoints = new Point[points.Length - 1];
Array.Copy(points, 1, newPoints, 0, newPoints.Length);
```

#### When to Use

Use structures for grouping related data when you need value semantics and stack allocation. Keep structs small and immutable when possible.

---

## II. Sequential Access Collections

Sequential access collections require you to traverse through elements in a specific order (typically the order they were added).

### 2.1 Stack

#### Definition & Characteristics

- Last-In-First-Out (LIFO) data structure
- Push: add element to top
- Pop: remove element from top
- Peek: view top element without removing

#### Code Example - Complete Operations

```csharp
// Create a stack
Stack<int> stack = new Stack<int>();

// INSERT (Push elements onto stack)
stack.Push(10);
stack.Push(20);
stack.Push(30);
stack.Push(40);

// ACCESS (Peek at top without removing)
int top = stack.Peek(); // 40 (top element)

// LOOKUP (check if element exists)
bool contains = stack.Contains(20);  // true
bool containsValue = stack.Contains(999);  // false

// DELETE (Pop removes from top)
int removed1 = stack.Pop();  // 40
int removed2 = stack.Pop();  // 30
Console.WriteLine($"Popped: {removed1}, {removed2}");

// Clear all elements
// stack.Clear();

// Remaining element
int remaining = stack.Peek();  // 20
int count = stack.Count;  // 1
```

#### Real-World Use Cases

- Undo/Redo functionality
- Browser back button
- Expression evaluation
- DFS (Depth-First Search)

---

### 2.2 Queue

#### Definition & Characteristics

- First-In-First-Out (FIFO) data structure
- Enqueue: add element to rear
- Dequeue: remove element from front
- Peek: view front element without removing

#### Code Example - Complete Operations

```csharp
// Create a queue
Queue<string> queue = new Queue<string>();

// INSERT (Enqueue elements)
queue.Enqueue("First");
queue.Enqueue("Second");
queue.Enqueue("Third");
queue.Enqueue("Fourth");

// ACCESS (Peek at front without removing)
string front = queue.Peek(); // "First"

// LOOKUP (check if element exists)
bool contains = queue.Contains("Second");  // true
bool containsValue = queue.Contains("NotThere");  // false

// DELETE (Dequeue removes from front)
string removed1 = queue.Dequeue();  // "First"
string removed2 = queue.Dequeue();  // "Second"
Console.WriteLine($"Dequeued: {removed1}, {removed2}");

// Remaining elements
string next = queue.Peek();  // "Third"
int count = queue.Count;  // 2
```

#### Real-World Use Cases

- Print queue
- Customer service queue
- BFS (Breadth-First Search)
- Scheduling tasks

---

### 2.3 Hash Table

#### Definition & Characteristics

- Key-value pair storage
- Uses hash function for fast lookups
- Not strongly typed (legacy collection)
- O(1) average lookup time

#### Code Example - Complete Operations

```csharp
// Create a hashtable (legacy - use Dictionary<K,V> instead)
Hashtable hashtable = new Hashtable();

// INSERT (Add key-value pairs)
hashtable["Name"] = "John";
hashtable["Age"] = 30;
hashtable["City"] = "New York";
hashtable[1] = "One";

// ACCESS (retrieve by key)
string name = (string)hashtable["Name"];  // "John"
int age = (int)hashtable["Age"];  // 30

// LOOKUP (check if key exists)
bool hasName = hashtable.ContainsKey("Name");  // true
bool hasEmail = hashtable.ContainsKey("Email");  // false
bool hasValue = hashtable.ContainsValue("John");  // true

// DELETE (remove by key)
hashtable.Remove("Age");
hashtable.Remove(1);

// Verify deletion
bool stillExists = hashtable.ContainsKey("Age");  // false
int count = hashtable.Count;  // 2
```

#### Note

Hashtable is a legacy collection. Use Dictionary<K,V> for new code as it provides type safety.

---

### 2.4 Dictionary

#### Definition & Characteristics

- Generic key-value pair storage
- Strongly typed for both keys and values
- Unique keys only
- O(1) average lookup time

#### Code Example - Complete Operations

```csharp
// Create a dictionary
Dictionary<string, int> ages = new Dictionary<string, int>();

// INSERT (Add key-value pairs)
ages["Alice"] = 25;
ages["Bob"] = 30;
ages.Add("Charlie", 35);
ages["Diana"] = 28;

// ACCESS (retrieve by key)
int aliceAge = ages["Alice"];  // 25
int charlieAge = ages["Charlie"];  // 35

// LOOKUP (check if key exists - safe access)
if (ages.TryGetValue("Dave", out int daveAge))
{
    Console.WriteLine($"Dave's age: {daveAge}");
}
else
{
    Console.WriteLine("Dave not found");
}

bool hasAlice = ages.ContainsKey("Alice");  // true
bool hasEve = ages.ContainsKey("Eve");  // false

// DELETE (remove by key)
ages.Remove("Bob");
ages.Remove("Diana");

// Verify deletion
bool bobStillExists = ages.ContainsKey("Bob");  // false
int remaining = ages.Count;  // 2

// View remaining entries
foreach (var kvp in ages)
{
    Console.WriteLine($"{kvp.Key}: {kvp.Value}");
}
```

#### Real-World Use Cases

- Caching
- Configuration settings
- Phone book
- Student grade lookup

---

## III. Hierarchical Collections

Hierarchical collections organize data in a tree-like structure with parent-child relationships.

### 3.1 Tree

#### Definition & Characteristics

- Hierarchical data structure
- Root node at top, child nodes below
- No cycles or circular references
- Each node (except root) has exactly one parent

#### Code Example - Complete Operations

```csharp
// Define a tree node
public class TreeNode<T>
{
    public T Value { get; set; }
    public List<TreeNode<T>> Children { get; set; }

    public TreeNode(T value)
    {
        Value = value;
        Children = new List<TreeNode<T>>();
    }
}

// INSERT - Add nodes to tree
TreeNode<int> root = new TreeNode<int>(1);
root.Children.Add(new TreeNode<int>(2));
root.Children.Add(new TreeNode<int>(3));
root.Children[0].Children.Add(new TreeNode<int>(4));
root.Children[0].Children.Add(new TreeNode<int>(5));
root.Children[1].Children.Add(new TreeNode<int>(6));

// ACCESS - Traverse and retrieve values
int rootValue = root.Value;  // 1
int secondChildValue = root.Children[1].Value;  // 3
int leafValue = root.Children[0].Children[0].Value;  // 4

// ACCESS - Traverse using DFS
public void TraverseDFS(TreeNode<int> node)
{
    Console.WriteLine(node.Value);
    foreach (var child in node.Children)
    {
        TraverseDFS(child);
    }
}

// LOOKUP - Search for a value
public TreeNode<int> SearchTree(TreeNode<int> node, int target)
{
    if (node.Value == target)
        return node;

    foreach (var child in node.Children)
    {
        var result = SearchTree(child, target);
        if (result != null)
            return result;
    }
    return null;
}

TreeNode<int> found = SearchTree(root, 4);  // Returns node with value 4
TreeNode<int> notFound = SearchTree(root, 99);  // Returns null

// DELETE - Remove a child node
bool removed = root.Children[0].Children.Remove(
    root.Children[0].Children.First(n => n.Value == 4)
);
```

---

### 3.1.1 Binary Tree

A specialized tree where each node has at most two children (left and right).

#### Code Example - Complete Operations

```csharp
// Binary tree node
public class BinaryTreeNode<T>
{
    public T Value { get; set; }
    public BinaryTreeNode<T> Left { get; set; }
    public BinaryTreeNode<T> Right { get; set; }

    public BinaryTreeNode(T value)
    {
        Value = value;
        Left = null;
        Right = null;
    }
}

// INSERT (create and add nodes)
BinaryTreeNode<int> root = new BinaryTreeNode<int>(1);
root.Left = new BinaryTreeNode<int>(2);
root.Right = new BinaryTreeNode<int>(3);
root.Left.Left = new BinaryTreeNode<int>(4);
root.Left.Right = new BinaryTreeNode<int>(5);

// ACCESS (traverse and retrieve values)
int rootValue = root.Value;  // 1
int leftChildValue = root.Left.Value;  // 2
int rightChildValue = root.Right.Value;  // 3

// LOOKUP (search for a value)
public bool SearchTree(BinaryTreeNode<int> node, int target)
{
    if (node == null) return false;
    if (node.Value == target) return true;

    return SearchTree(node.Left, target) || SearchTree(node.Right, target);
}

bool found = SearchTree(root, 4);  // true
bool notFound = SearchTree(root, 99);  // false

// DELETE (remove a node - complex operation)
// For binary trees, deletion is more complex as you must maintain structure
// Here's a simple approach for leaf nodes:
if (root.Left.Left != null && root.Left.Left.Value == 4)
{
    root.Left.Left = null;  // Remove leaf node
}
```

#### Uses

- BST (Binary Search Tree)
- Expression trees
- File systems
- Sorting algorithms

---

### 3.2 Heap

#### Definition & Characteristics

- Complete binary tree that satisfies heap property
- Max Heap: parent ≥ children
- Min Heap: parent ≤ children
- O(log n) insertion and deletion

#### Code Example - Complete Operations

```csharp
// C# has PriorityQueue<TElement, TPriority> in .NET 6+
PriorityQueue<string, int> minHeap = new PriorityQueue<string, int>();

// INSERT (add elements with priority)
minHeap.Enqueue("High", 3);
minHeap.Enqueue("Low", 1);
minHeap.Enqueue("Medium", 2);
minHeap.Enqueue("Urgent", 0);
minHeap.Enqueue("Later", 5);

// ACCESS (peek at highest priority without removing)
if (minHeap.TryPeek(out string next, out int priority))
{
    Console.WriteLine($"Next: {next}, Priority: {priority}"); // "Urgent", 0
}

// LOOKUP (check if element exists - limited support in PriorityQueue)
// Note: PriorityQueue doesn't have built-in Contains, but you can iterate
var list = new List<string>();
var tempHeap = new PriorityQueue<string, int>(minHeap.UnorderedItems);
bool found = false;
foreach (var item in tempHeap.UnorderedItems)
{
    if (item.Element == "Medium")
    {
        found = true;
        break;
    }
}
Console.WriteLine($"Found 'Medium': {found}");

// DELETE (remove highest priority element)
string removed1 = minHeap.Dequeue();  // "Urgent" (priority 0)
string removed2 = minHeap.Dequeue();  // "Low" (priority 1)
Console.WriteLine($"Removed: {removed1}, {removed2}");

// Check remaining
int count = minHeap.Count;  // 3
```

#### Uses

- Priority queue
- Dijkstra's algorithm
- Heap sort
- Task scheduling

---

## IV. Group Collections

Group collections organize elements as unordered groups or networks with specific relationships.

### 4.1 Set

#### Definition & Characteristics

- Unordered collection of unique elements
- No duplicates allowed
- O(1) average lookup, add, remove
- Supports set operations: union, intersection, difference

#### Code Example - Complete Operations

```csharp
// Create a HashSet
HashSet<int> numbers = new HashSet<int> { 1, 2, 3, 4, 5 };

// INSERT (add elements)
numbers.Add(6);      // Added successfully
numbers.Add(5);      // Duplicate, won't be added
numbers.Add(7);
numbers.Add(8);

// ACCESS (iterate through set)
Console.WriteLine("Set contents:");
foreach (int num in numbers)
{
    Console.WriteLine(num);  // 1, 2, 3, 4, 5, 6, 7, 8 (order may vary)
}

// LOOKUP (check if element exists)
bool contains3 = numbers.Contains(3);      // true
bool contains10 = numbers.Contains(10);    // false
int count = numbers.Count;                 // 8

// DELETE (remove elements)
numbers.Remove(5);   // Removed successfully
numbers.Remove(10);  // Doesn't exist, returns false
numbers.Remove(7);

// Verify deletions
bool stillHas5 = numbers.Contains(5);   // false
int newCount = numbers.Count;           // 6

// Set operations
HashSet<int> set1 = new HashSet<int> { 1, 2, 3 };
HashSet<int> set2 = new HashSet<int> { 3, 4, 5 };

set1.UnionWith(set2);      // {1, 2, 3, 4, 5}
set1.IntersectWith(set2);  // {3}
set1.ExceptWith(set2);     // Elements in set1 but not in set2
```

#### Uses

- Removing duplicates
- Membership testing
- Mathematical set operations

---

### 4.2 Graph

#### Definition & Characteristics

- Non-hierarchical collection of nodes (vertices) and edges
- Directed: edges point from one node to another
- Undirected: edges are bidirectional
- Can have cycles

#### Code Example - Complete Operations

```csharp
// Graph using Dictionary and List
public class Graph<T>
{
    private Dictionary<T, List<T>> adjacencyList;

    public Graph()
    {
        adjacencyList = new Dictionary<T, List<T>>();
    }

    // INSERT - Add vertex
    public void AddVertex(T vertex)
    {
        if (!adjacencyList.ContainsKey(vertex))
            adjacencyList[vertex] = new List<T>();
    }

    // INSERT - Add edge
    public void AddEdge(T from, T to)
    {
        if (!adjacencyList.ContainsKey(from))
            AddVertex(from);
        if (!adjacencyList.ContainsKey(to))
            AddVertex(to);

        adjacencyList[from].Add(to);
    }

    // ACCESS - Get neighbors of a vertex
    public List<T> GetNeighbors(T vertex)
    {
        return adjacencyList.ContainsKey(vertex) ? 
               adjacencyList[vertex] : new List<T>();
    }

    // LOOKUP - Check if vertex exists
    public bool HasVertex(T vertex)
    {
        return adjacencyList.ContainsKey(vertex);
    }

    // LOOKUP - Check if edge exists
    public bool HasEdge(T from, T to)
    {
        return adjacencyList.ContainsKey(from) && 
               adjacencyList[from].Contains(to);
    }

    // DELETE - Remove edge
    public void RemoveEdge(T from, T to)
    {
        if (adjacencyList.ContainsKey(from))
        {
            adjacencyList[from].Remove(to);
        }
    }

    // DELETE - Remove vertex
    public void RemoveVertex(T vertex)
    {
        if (adjacencyList.ContainsKey(vertex))
        {
            // Remove all edges pointing to this vertex
            foreach (var key in adjacencyList.Keys)
            {
                adjacencyList[key].Remove(vertex);
            }
            // Remove the vertex itself
            adjacencyList.Remove(vertex);
        }
    }
}

// Usage example
var graph = new Graph<string>();

// INSERT
graph.AddVertex("A");
graph.AddVertex("B");
graph.AddVertex("C");
graph.AddEdge("A", "B");
graph.AddEdge("A", "C");
graph.AddEdge("B", "C");

// ACCESS
var neighborsOfA = graph.GetNeighbors("A");  // ["B", "C"]

// LOOKUP
bool hasA = graph.HasVertex("A");         // true
bool hasEdgeAB = graph.HasEdge("A", "B"); // true
bool hasEdgeBA = graph.HasEdge("B", "A"); // false

// DELETE
graph.RemoveEdge("A", "C");
bool hasEdgeAfterDelete = graph.HasEdge("A", "C");  // false
graph.RemoveVertex("B");
```

#### Uses

- Social networks
- Road maps
- Web page links
- Computer networks

---

### 4.3 Network (Weighted Graph)

#### Definition & Characteristics

- Graph where edges have associated weights or costs
- Weighted edges represent distances, costs, or capacities
- Can be directed or undirected
- More complex than simple graphs

#### Code Example - Complete Operations

```csharp
// Edge class for weighted graphs
public class Edge<T>
{
    public T From { get; set; }
    public T To { get; set; }
    public double Weight { get; set; }

    public Edge(T from, T to, double weight)
    {
        From = from;
        To = to;
        Weight = weight;
    }
}

// Weighted graph
public class WeightedGraph<T>
{
    private Dictionary<T, List<Edge<T>>> adjacencyList;

    public WeightedGraph()
    {
        adjacencyList = new Dictionary<T, List<Edge<T>>>();
    }

    // INSERT - Add vertex
    public void AddVertex(T vertex)
    {
        if (!adjacencyList.ContainsKey(vertex))
            adjacencyList[vertex] = new List<Edge<T>>();
    }

    // INSERT - Add weighted edge
    public void AddEdge(T from, T to, double weight)
    {
        if (!adjacencyList.ContainsKey(from))
            AddVertex(from);
        if (!adjacencyList.ContainsKey(to))
            AddVertex(to);

        adjacencyList[from].Add(new Edge<T>(from, to, weight));
    }

    // ACCESS - Get all edges from a vertex
    public List<Edge<T>> GetEdges(T vertex)
    {
        return adjacencyList.ContainsKey(vertex) ? 
               adjacencyList[vertex] : new List<Edge<T>>();
    }

    // LOOKUP - Check if vertex exists
    public bool HasVertex(T vertex)
    {
        return adjacencyList.ContainsKey(vertex);
    }

    // LOOKUP - Get weight of an edge
    public double? GetEdgeWeight(T from, T to)
    {
        if (adjacencyList.ContainsKey(from))
        {
            var edge = adjacencyList[from].FirstOrDefault(e => e.To.Equals(to));
            return edge?.Weight;
        }
        return null;
    }

    // DELETE - Remove edge
    public void RemoveEdge(T from, T to)
    {
        if (adjacencyList.ContainsKey(from))
        {
            adjacencyList[from].RemoveAll(e => e.To.Equals(to));
        }
    }

    // DELETE - Remove vertex
    public void RemoveVertex(T vertex)
    {
        if (adjacencyList.ContainsKey(vertex))
        {
            foreach (var key in adjacencyList.Keys)
            {
                adjacencyList[key].RemoveAll(e => e.To.Equals(vertex));
            }
            adjacencyList.Remove(vertex);
        }
    }
}

// Usage example
var wGraph = new WeightedGraph<string>();

// INSERT
wGraph.AddVertex("New York");
wGraph.AddVertex("Boston");
wGraph.AddVertex("Philadelphia");
wGraph.AddEdge("New York", "Boston", 215);
wGraph.AddEdge("New York", "Philadelphia", 95);
wGraph.AddEdge("Boston", "Philadelphia", 305);

// ACCESS
var edgesFromNY = wGraph.GetEdges("New York");

// LOOKUP
bool hasNY = wGraph.HasVertex("New York");           // true
double? weight = wGraph.GetEdgeWeight("New York", "Boston");  // 215

// DELETE
wGraph.RemoveEdge("New York", "Boston");
double? weightAfterDelete = wGraph.GetEdgeWeight("New York", "Boston");  // null
```

#### Uses

- GPS navigation
- Airline routes
- Network routing
- Supply chains

---

## V. Best Practices & Tips

### Collection Selection Guidelines

- Use generics (List<T>, Dictionary<K,V>) instead of non-generic collections
- Use Dictionary when you need fast key-based lookups
- Use List<T> for dynamic collections with indexed access
- Use HashSet<T> for collections that must not contain duplicates
- Use Stack for LIFO operations, Queue for FIFO operations
- Consider performance: prefer O(1) operations for frequent access patterns
- Profile your code with real data to identify bottlenecks

### Memory & Performance Considerations

- Arrays have fixed memory; use if size is known and doesn't change
- Generic collections allocate memory dynamically; watch for memory leaks
- Dictionary and HashSet use more memory than List due to hashing
- Consider using foreach instead of indexing for sequential access
- Use IEnumerable for read-only collection access in method parameters

### Collection Comparison Table

| Collection      | Access | Lookup | Insert | Delete | Use Case                         |
| --------------- | ------ | ------ | ------ | ------ | -------------------------------- |
| Array           | O(1)   | O(n)   | O(n)   | O(n)   | Fixed-size, fast random access   |
| List<T>         | O(1)   | O(n)   | O(n)   | O(n)   | Dynamic arrays, flexible size    |
| Stack           | O(1)   | O(n)   | O(1)   | O(1)   | LIFO, undo/redo, DFS             |
| Queue           | O(1)   | O(n)   | O(1)   | O(1)   | FIFO, task scheduling, BFS       |
| Dictionary<K,V> | O(1)   | O(1)   | O(1)   | O(1)   | Key-value pairs, fast lookup     |
| HashSet<T>      | N/A    | O(1)   | O(1)   | O(1)   | Unique items, duplicates removal |
| Tree/Graph      | O(n)   | O(n)   | O(1)   | O(1)   | Hierarchical data, networks      |

### LINQ Integration

All C# collections implement IEnumerable, allowing you to use LINQ queries:

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

var evens = numbers.Where(n => n % 2 == 0);
var squared = numbers.Select(n => n * n);
var sum = numbers.Aggregate((a, b) => a + b);
```

---

**End of Learning Guide**
