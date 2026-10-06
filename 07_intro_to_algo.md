# Introduction to Algorithms

### Transition: From Data Structures to Algorithms

---

# Learning Goals

At the end of this discussion, you should be able to:

1. Explain what an algorithm is.
2. Identify the parts of a computational problem.
3. Describe a solution as a sequence of steps.
4. Write simple pseudocode.
5. Trace an algorithm using sample data.
6. Translate simple pseudocode into C#.

> **Main idea:** Before writing code, know the steps needed to solve the problem.

---

# Where Are We Now?

So far, we have worked with data structures such as:

- Array
- Struct
- Dictionary
- Queue
- Stack
- Hash

We have learned basic operations such as:

- Add
- Access
- Search
- Update
- Delete
- Display

But knowing a data structure is only part of solving a problem.

### The next question is:

> **How do we use the data structure to solve a problem?**

That is where **algorithms** come in.

---

# What Is an Algorithm?

An **algorithm** is a finite, ordered sequence of steps used to solve a problem or accomplish a task.

An algorithm should tell us:

- What to do
- In what order to do it
- When to stop

### Simple example

Problem:

> Find the largest number among three numbers.

Possible solution:

1. Read three numbers.
2. Compare the numbers.
3. Determine which is largest.
4. Display the largest number.

Those steps form an algorithm.

---

# Algorithm in Everyday Life

Algorithms are not exclusive to programming.

### Example: Making Instant Coffee

1. Get a cup.
2. Add coffee.
3. Add sugar.
4. Add hot water.
5. Stir.
6. Serve.

The important idea is:

> **The steps have an order.**

If we change the order, the result may be different.

---

# Algorithm vs. Program

### Algorithm

Describes **how to solve the problem**.

```text
1. Read two numbers.
2. Add the numbers.
3. Display the result.
```

### Program

Implements the algorithm using a programming language.

```csharp
int a = 10;
int b = 20;

int sum = a + b;

Console.WriteLine(sum);
```

### Remember

> **Algorithm = solution steps**  
> **Program = implementation of those steps**

---

# Problem → Algorithm → Program

The basic process is:

```text
PROBLEM
   ↓
UNDERSTAND THE PROBLEM
   ↓
DESIGN THE ALGORITHM
   ↓
WRITE PSEUDOCODE
   ↓
IMPLEMENT IN C#
   ↓
TEST
```

Do not immediately jump from:

```text
Problem → C# code
```

Instead:

```text
Problem → Algorithm → Code
```

---

# Identify the Problem

Before designing an algorithm, ask:

### 1. What is the input?

What information does the program receive?

### 2. What is the output?

What should the program produce?

### 3. What processing is required?

What must happen to the input to produce the output?

---

# Example: Find the Largest Number

### Problem

Create a program that receives three numbers and displays the largest number.

### Input

```text
10
25
15
```

### Processing

Compare the numbers.

### Output

```text
25
```

Before writing C#, we can describe the solution using steps.

---

# First Algorithm

### Find the Largest of Three Numbers

```text
1. Start
2. Read number A
3. Read number B
4. Read number C
5. Assume A is the largest
6. If B is greater than the largest, make B the largest
7. If C is greater than the largest, make C the largest
8. Display the largest number
9. End
```

This is an algorithm. It is not yet C# code.

---

# What Makes a Good Algorithm?

A useful algorithm should have:

### Clear Steps

Each step should be understandable.

### Correct Order

Steps should happen in the appropriate sequence.

### A Defined Result

The algorithm should produce the required output.

### A Stopping Point

The algorithm should eventually finish.

### Appropriate Processing

The steps should actually solve the problem.

---

# Algorithm Representation

There are several ways to represent an algorithm.

For this course, we will commonly use:

### 1. Natural Language

```text
Read the student's grade.
If the grade is 75 or higher,
display "Passed".
Otherwise, display "Failed".
```

### 2. Pseudocode

```text
START
    READ grade

    IF grade >= 75 THEN
        DISPLAY "Passed"
    ELSE
        DISPLAY "Failed"
    END IF
END
```

### 3. Flowchart

A visual representation of the steps.

### 4. Program Code

The algorithm implemented in a programming language such as C#.

---

# What Is Pseudocode?

**Pseudocode** is a simple way of writing the logic of an algorithm without following the exact syntax of a programming language.

It looks like code, but it is not actual C#.

Example:

```text
START

READ number

IF number > 0 THEN
    DISPLAY "Positive"
ELSE IF number < 0 THEN
    DISPLAY "Negative"
ELSE
    DISPLAY "Zero"
END IF

END
```

---

# Why Use Pseudocode?

Pseudocode allows us to focus on:

> **What should the program do?**

instead of:

> **What is the exact C# syntax?**

This is especially useful when designing an algorithm.

### Remember:

```text
Problem
   ↓
Pseudocode
   ↓
C# Code
```

---

# Common Pseudocode Words

| Pseudocode | Meaning |
| --- | --- |
| START | Begin |
| END | Stop |
| READ | Get input |
| DISPLAY | Show output |
| SET | Assign a value |
| IF  | Make a decision |
| ELSE | Alternative decision |
| FOR | Repeat a known number of times |
| WHILE | Repeat while a condition is true |

These are descriptions of logic, not C# syntax.

---

# Example: Student Search

Now connect the algorithm to the data structures we already studied.

### Problem

Given an array of student numbers, find a particular student number.

```text
Student Numbers:

2026-0001
2026-0002
2026-0003
2026-0004
```

Search for:

```text
2026-0003
```

---

# Search Algorithm

A simple approach is to check each student number one at a time.

```text
START

READ target student number

FOR each student number
    IF student number = target THEN
        DISPLAY "Student found"
        STOP SEARCH
    END IF
END FOR

DISPLAY "Student not found"

END
```

Notice that we have not written C# yet.

We are designing the solution first.

---

# Trace the Algorithm

Tracing means following the algorithm step by step using actual data.

### Data

```text
2026-0001
2026-0002
2026-0003
2026-0004
```

### Target

```text
2026-0003
```

### Trace

| Step | Current Value | Target | Result |
| --- | --- | --- | --- |
| 1   | 2026-0001 | 2026-0003 | Not equal |
| 2   | 2026-0002 | 2026-0003 | Not equal |
| 3   | 2026-0003 | 2026-0003 | Found |

Output:

```text
Student found
```

---

# From Pseudocode to C#

Once the algorithm is clear, we can implement it.

### Pseudocode

```text
FOR each student number
    IF student number = target THEN
        DISPLAY "Student found"
        STOP SEARCH
    END IF
END FOR
```

### C#

```csharp
for (int i = 0; i < students.Length; i++)
{
    if (students[i] == target)
    {
        Console.WriteLine("Student found");
        break;
    }
}
```

The C# code is an implementation of the algorithm.

---

# Another Example: Find Maximum

### Problem

Find the highest value in an array.

```text
[25, 12, 40, 18, 30]
```

### Algorithm

```text
1. Assume the first value is the largest.
2. Check the next value.
3. If it is larger, make it the new largest.
4. Continue until all values have been checked.
5. Display the largest value.
```

Expected output:

```text
Largest value: 40
```

---

# Trace: Find Maximum

Data:

```text
[25, 12, 40, 18, 30]
```

Start:

```text
largest = 25
```

Then:

```text
12 > 25? No
40 > 25? Yes → largest = 40
18 > 40? No
30 > 40? No
```

Final result:

```text
Largest = 40
```

### Practice 01: Count Passing Students

```textile
Given the following grades:

72, 85, 60, 91, 68, 77, 55, 89

A student is considered passing if the grade is 75 or higher.

Expected output: 
Number of students who passed: 4

Task: 
a. Write an algorithm that counts how many students passed.
b. Write the pseudocode
c. Trace the algorithm.
```

### Practice 02: Calculate the Average

```textile
Given the following grades:

80, 75, 90, 85, 70

Task:
a. Write an algorithm that calculates the average of the grades.
b. Write the pseudocode
c. Trace the algorithm.

Expected output:

Average grade: 80
```

### Practice 03: Count Students with a Grade of 90 or Higher

```text
Given the following grades:

92, 85, 90, 76, 95, 88, 91

A student is considered an excellent performer if the grade is 90 or higher.

Expected output:

Number of excellent performers: 4

Task:
a. Write an algorithm that counts how many students have a grade of 90 or higher.
b. Write the pseudocode
c. Trace the algorithm.
```

### Practice 04: Find the First Failing Grade

```text
Given the following grades:

85, 82, 78, 71, 90, 68

A student is considered failing if the grade is below 75.

Expected output:

First failing grade: 71

Task:  
a. Write an algorithm that finds the first failing grade.  
b. Write the pseudocode
c. Trace the algorithm.
```

---

# Algorithm and Data Structure

An algorithm does not exist in isolation.

Algorithms often operate on data stored in a data structure.

Examples:

```text
Array
  +
Search Algorithm
```

```text
Dictionary
  +
Key Lookup
```

```text
Queue
  +
Processing Algorithm
```

```text
Stack
  +
LIFO Processing
```

### Key idea

> **Data structure = how data is organized**  
> **Algorithm = how we process the data**

---

# Choosing an Approach

When given a problem, do not immediately ask:

> "What C# code should I write?"

Ask:

1. What data do I have?
2. How should the data be organized?
3. What operation must I perform?
4. What steps solve the problem?
5. What data structure is appropriate?
6. How can I implement the steps?

---

# Debugging the Algorithm

A program can have correct C# syntax but still have a wrong algorithm.

Example:

```text
Problem:
Find the largest number.

Incorrect algorithm:

1. Read the numbers.
2. Assume the first number is largest.
3. Compare only the second number.
4. Display the largest.
```

What is wrong?

> The algorithm does not check all the numbers.

### Important

Finding errors is not only about finding syntax errors.

We must also check whether the **logic solves the problem**.

---

# Algorithm vs. Syntax

Consider:

```csharp
if (a > b)
{
    largest = a;
}
```

The syntax may be correct.

But is the algorithm correct?

It depends on the problem.

If there are three numbers:

```text
a = 10
b = 20
c = 50
```

checking only `a` and `b` is not enough.

### Lesson

> Correct syntax does not automatically mean a correct solution.

---

# Three Things to Check

When creating an algorithm, check:

### 1. Correctness

Does it produce the correct result?

### 2. Completeness

Does it handle all required cases?

### 3. Termination

Does it eventually stop?

These three questions should become part of your normal problem-solving process.

---

# The DSA Problem-Solving Pattern

From this point forward, use this pattern:

```text
        PROBLEM
           ↓
    Identify Input
           ↓
    Identify Output
           ↓
   Choose Data Structure
           ↓
     Design Algorithm
           ↓
       Pseudocode
           ↓
       Implement
           ↓
         Trace
           ↓
         Test
```

This pattern will be used throughout the rest of the course.

---

# What Comes Next?

Now that we understand how to design algorithms, the next question is:

> **How good is an algorithm?**

Two algorithms may solve the same problem but require different amounts of work.

This leads to:

## Algorithm Analysis

``We will examine:

- Number of operations
- Growth as data increases
- Basic efficiency
- Sequential Search
- Big-O notation

---

# Key Takeaways

Remember these ideas:

1. An **algorithm** is a sequence of steps for solving a problem.
2. A **program** implements an algorithm.
3. **Pseudocode** helps us design logic before writing code.
4. **Tracing** helps us understand and verify an algorithm.
5. A correct program requires both correct syntax and correct logic.
6. **Data structures organize data; algorithms process data.**
7. Good problem solving starts with understanding the problem before writing code.

### Most important:

> **Do not code first. Think first.**

---

#

#
