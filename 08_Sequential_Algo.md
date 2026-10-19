# Algorithm Analysis and Sequential Search

---

# I. Learning Objectives

At the end of this lesson, students should be able to:

1. Explain why algorithms need to be analyzed.
  
2. Identify the operations performed by an algorithm.
  
3. Determine how the amount of work changes as the input size increases.
  
4. Explain the basic idea of algorithm efficiency.
  
5. Identify simple algorithmic complexity patterns:
  
  - O(1)
    
  - O(n)
    
  - O(n²)
    
6. Write an algorithm for sequential search.
  
7. Trace a sequential search algorithm.
  
8. Implement sequential search using C#.
  
9. Explain the best-case and worst-case behavior of sequential search.
  

---

# II. From Algorithm to Algorithm Analysis

## 1. Review: What Is an Algorithm?

An algorithm is a sequence of steps used to solve a problem.

For example:

**Problem:** Find a particular student number from a list of students.

A possible algorithm is:

1. Start with the first student.
  
2. Check the student number.
  
3. If it matches the target, stop.
  
4. Otherwise, check the next student.
  
5. Continue until the student is found or there are no more students.
  

This algorithm can solve the problem.

But there is another question:

> **How much work does the algorithm perform?**

This leads us to **algorithm analysis**.

---

# III. Why Analyze Algorithms?

Consider two algorithms that solve the same problem.

Both produce the correct answer.

However:

- Algorithm A may perform 10 operations.
  
- Algorithm B may perform 1,000 operations.
  

Both are correct, but Algorithm A may be more efficient.

This becomes more important when the amount of data increases.

For example:

```text
10 records
100 records
1,000 records
10,000 records
1,000,000 records
```

An algorithm that works well with 10 records may not work efficiently with 1,000,000 records.

Therefore, when studying algorithms, we ask:

> **How does the amount of work grow as the input becomes larger?**

---

# IV. Input Size

The amount of data given to an algorithm is called the **input size**.

We commonly represent input size using:

```text
n
```

For example:

```text
5 students       → n = 5
100 students     → n = 100
1,000 students   → n = 1,000
```

The value of `n` helps us describe how an algorithm behaves as the amount of data increases.

---

# V. Counting Operations

One simple way to analyze an algorithm is to count how many times an important operation is performed.

Consider:

```text
1. Read a number.
2. Display the number.
```

The algorithm performs a fixed number of steps regardless of how large another collection might be.

Now consider:

```text
1. Read the first number.
2. Read the second number.
3. Read the third number.
...
```

If there are more values, more operations are required.

This difference is important.

---

# VI. Constant Time — O(1)

Consider:

```csharp
int first = numbers[0];
```

The program accesses one specific element.

Whether the array contains:

```text
10 elements
100 elements
10,000 elements
1,000,000 elements
```

the statement still accesses one element.

We describe this as:

```text
O(1)
```

### O(1) means:

> The amount of work remains approximately constant as the input size increases.

Examples:

```csharp
numbers[0]
numbers[5]
```

when the position is directly known.

---

# VII. Linear Time — O(n)

Consider:

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

The loop processes every element.

If there are:

```text
5 elements  → approximately 5 iterations
10 elements → approximately 10 iterations
100 elements → approximately 100 iterations
```

The amount of work grows with the input size.

We describe this as:

```text
O(n)
```

### O(n) means:

> The amount of work grows approximately in proportion to the input size.

---

# VIII. Quadratic Time — O(n²)

Consider nested loops:

```csharp
for (int i = 0; i < n; i++)
{
    for (int j = 0; j < n; j++)
    {
        Console.WriteLine("*");
    }
}
```

The outer loop runs `n` times.

For every iteration of the outer loop, the inner loop also runs `n` times.

Therefore:

```text
n × n = n²
```

We describe this as:

```text
O(n²)
```

---

# IX. Comparing O(1), O(n), and O(n²)

| Complexity | General Meaning | Example |
| --- | --- | --- |
| O(1) | Constant | Access one known array element |
| O(n) | Linear | Process every element once |
| O(n²) | Quadratic | Nested loops |

As `n` becomes larger:

```text
O(1)   → zero growth
O(n)   → grows with n
O(n²)  → grows much faster
```

For now, the goal is not to memorize every possible Big-O notation.

The goal is to understand:

> **How does the amount of work change when the input becomes larger?**

---

# X. Practice: Identify the Pattern

## Problem 1

```csharp
int value = numbers[3];
```

Question:

What is the basic complexity?

---

## Problem 2

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

Question:

What is the basic complexity?

---

## Problem 3

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    for (int j = 0; j < numbers.Length; j++)
    {
        Console.WriteLine(numbers[i] + numbers[j]);
    }
}
```

Question:

What is the basic complexity?

---

# XI. Sequential Search

Now we will apply algorithm analysis to an actual problem.

Suppose we have the following student numbers:

```text
2026-0001
2026-0002
2026-0003
2026-0004
2026-0005
```

We want to find:

```text
2026-0004
```

How can we find it?

One simple approach is to check the student numbers one at a time.

This is called:

# Sequential Search

---

# XII. What Is Sequential Search?

**Sequential Search** is a searching algorithm that checks elements one at a time, starting from the beginning of the collection.

The basic process is:

```text
Start
  ↓
Check first element
  ↓
Is it the target?
  ├── Yes → Found
  └── No
       ↓
Check next element
       ↓
Repeat
```

The search ends when:

1. The target is found, or
  
2. All elements have been checked.
  

---

# XIII. Example

Given:

```text
10, 25, 30, 45, 50
```

Search for:

```text
45
```

The algorithm checks:

```text
10 → Not found
25 → Not found
30 → Not found
45 → Found
```

The target is found after 4 comparisons.

---

# XIV. Write the Algorithm

### Problem

Given a collection of values and a target value, determine whether the target exists in the collection.

### Algorithm

```text
1. Start at the first element.
2. Compare the current element with the target.
3. If the current element is equal to the target:
      Report that the target was found.
      Stop.
4. Otherwise, move to the next element.
5. Repeat until all elements have been checked.
6. If all elements have been checked and the target was not found:
      Report that the target was not found.
7. End.
```

---

# XV. Pseudocode

```text
START

INPUT array
INPUT target

FOR each element in array

    IF element equals target THEN
        DISPLAY "Target found"
        STOP
    END IF

END FOR

DISPLAY "Target not found"

END
```

---

# XVI. Trace the Algorithm

Given:

```text
Array:
10, 25, 30, 45, 50

Target:
45
```

Trace:

| Step | Current Value | Target | Result |
| --- | --- | --- | --- |
| 1   | 10  | 45  | Not found |
| 2   | 25  | 45  | Not found |
| 3   | 30  | 45  | Not found |
| 4   | 45  | 45  | Found |

Output:

```text
Target found.
```

---

# XVII. When the Target Is Not Found

Given:

```text
Array:
10, 25, 30, 45, 50

Target:
70
```

Trace:

| Step | Current Value | Target | Result |
| --- | --- | --- | --- |
| 1   | 10  | 70  | Not found |
| 2   | 25  | 70  | Not found |
| 3   | 30  | 70  | Not found |
| 4   | 45  | 70  | Not found |
| 5   | 50  | 70  | Not found |

Output:

```text
Target not found.
```

---

# XVIII. Best Case

Consider:

```text
10, 25, 30, 45, 50
↑
Target = 10
```

The target is the first element.

Only one comparison is needed.

Therefore, the best case is:

```text
O(1)
```

---

# XIX. Worst Case

Consider:

```text
10, 25, 30, 45, 50
                  ↑
             Target = 50
```

The algorithm checks every element before finding the target.

The same thing happens if the target does not exist:

```text
Target = 70
```

Every element must be checked.

Therefore, the worst case is:

```text
O(n)
```

---

# XX. Why Is Sequential Search O(n)?

Suppose there are:

```text
5 elements
```

The algorithm may perform up to:

```text
5 comparisons
```

If there are:

```text
100 elements
```

it may perform up to:

```text
100 comparisons
```

If there are:

```text
1,000 elements
```

it may perform up to:

```text
1,000 comparisons
```

Therefore, the amount of work grows with the number of elements.

This is:

```text
O(n)
```

---

# XXI. Important Observation

Sequential search does **not** require the data to be sorted.

For example:

```text
2026-0007
2026-0002
2026-0015
2026-0004
2026-0001
```

We can still search for:

```text
2026-0004
```

by checking the values one at a time.

This is one reason sequential search is simple and useful.

---

# XXII. Sequential Search in C#

```csharp
int[] numbers = { 10, 25, 30, 45, 50 };

int target = 45;
bool found = false;

for (int i = 0; i < numbers.Length; i++)
{
    if (numbers[i] == target)
    {
        found = true;
        break;
    }
}

if (found)
{
    Console.WriteLine("Target found.");
}
else
{
    Console.WriteLine("Target not found.");
}
```

---

# XXIII. Understanding the Code

### The data

```csharp
int[] numbers = { 10, 25, 30, 45, 50 };
```

The array contains the values we want to search.

### The target

```csharp
int target = 45;
```

This is the value we are looking for.

### The flag

```csharp
bool found = false;
```

This records whether the target has been found.

### The loop

```csharp
for (int i = 0; i < numbers.Length; i++)
```

The loop moves through the array one element at a time.

### The comparison

```csharp
if (numbers[i] == target)
```

This determines whether the current value matches the target.

### Stop the search

```csharp
break;
```

Once the target is found, there is no reason to continue searching.

---

# XXIV. Trace the C# Program

Given:

```text
numbers = { 10, 25, 30, 45, 50 }
target = 45
```

| i   | numbers[i] | Comparison | found |
| --- | --- | --- | --- |
| 0   | 10  | 10 == 45 → false | false |
| 1   | 25  | 25 == 45 → false | false |
| 2   | 30  | 30 == 45 → false | false |
| 3   | 45  | 45 == 45 → true | true |

At this point:

```csharp
break;
```

is executed.

Output:

```text
Target found.
```

---

# XXV. Practice Set

## Practice 1 — Search for a Student

Given the following student numbers:

```text
2026-0001
2026-0002
2026-0003
2026-0004
2026-0005
```

Search for:

```text
2026-0004
```

Expected output:

```text
Student found.
```

Task:

a. Write an algorithm that searches for the student number.

b. Trace the algorithm.

c. How many comparisons are performed?

---

## Practice 2 — Search for a Grade

Given:

```text
85, 72, 90, 68, 77, 91
```

Search for:

```text
68
```

Expected output:

```text
Grade found.
```

Task:

a. Write an algorithm.

b. Trace the algorithm.

c. How many comparisons are performed?

---

## Practice 3 — Value Not Found

Given:

```text
15, 22, 31, 44, 50
```

Search for:

```text
40
```

Expected output:

```text
Value not found.
```

Task:

a. Write an algorithm.

b. Trace the algorithm.

c. How many comparisons are performed?

---

## Practice 4 — Count Occurrences

Given:

```text
85, 90, 75, 90, 88, 90, 70, 85
```

Find how many times `90` appears.

Expected output:

```text
Number of students with grade 90: 3
```

Task:

a. Write an algorithm.

b. Trace the algorithm.

c. Identify the operation that is repeatedly performed.

---

## Practice 5 — First Failing Grade

Given:

```text
85, 82, 78, 71, 90, 68
```

A student is considered failing if the grade is below `75`.

Find the first failing grade.

Expected output:

```text
First failing grade: 71
```

Task:

a. Write an algorithm.

b. Trace the algorithm.

c. How many comparisons are performed?

---

# XXVI. Practice: Analyze the Algorithm

For each code fragment, identify whether it is approximately:

```text
O(1)
O(n)
O(n²)
```

### A

```csharp
int value = numbers[0];
```

### B

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

### C

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    for (int j = 0; j < numbers.Length; j++)
    {
        Console.WriteLine(numbers[i] + numbers[j]);
    }
}
```

---

# XXVII. Discussion Questions

1. Why should we analyze an algorithm instead of only checking whether it produces the correct answer?
  
2. What does `n` represent in algorithm analysis?
  
3. What is the difference between O(1) and O(n)?
  
4. Why does a loop that processes every element have an O(n) pattern?
  
5. Why does a nested loop often have an O(n²) pattern?
  
6. Why can sequential search work even when the data is not sorted?
  
7. What is the best case of sequential search?
  
8. What is the worst case of sequential search?
  
9. Why is sequential search generally classified as O(n)?
  

---

# XXVIII. Key Takeaways

## Algorithm Analysis

An algorithm should not only be correct.

We should also consider how much work it performs.

The input size is commonly represented by:

```text
n
```

Basic complexity patterns:

```text
O(1)  → constant
O(n)  → linear
O(n²) → quadratic
```

---

## Sequential Search

Sequential search:

1. Starts at the beginning.
  
2. Checks one element at a time.
  
3. Compares the current element with the target.
  
4. Stops when the target is found.
  
5. Stops after all elements have been checked if the target does not exist.
  

Best case:

```text
O(1)
```

Worst case:

```text
O(n)
```

Overall, sequential search is commonly described as:

```text
O(n)
```

---

# XXIX. Important DSA Connection

Remember:

> **A data structure organizes data. An algorithm operates on that data.**

For example:

```text
Array
  ↓
Sequential Search
  ↓
Find a value
```

The array provides the data structure.

Sequential search provides the procedure for finding the data.

This connection is central to Data Structures and Algorithms.

---

# XXX. Transition to Next Week

Sequential search works by checking elements one at a time.

But what if the data is **sorted**?

Can we search more efficiently than checking every element?

Next, we will study:

# Binary Search

Binary search uses a different strategy:

```text
Check the middle
       ↓
Eliminate half of the search space
       ↓
Check the remaining half
       ↓
Repeat
```

This leads to a much more efficient search for appropriately sorted data.
