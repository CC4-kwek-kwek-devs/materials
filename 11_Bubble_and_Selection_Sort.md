## Week 11 — Sorting Algorithms I: Bubble Sort and Selection Sort

## Learning Objectives
Students should be able to:
1. Explain why data is sorted.
2. Describe Bubble Sort and Selection Sort.
3. Write pseudocode and trace both algorithms.
4. Implement both algorithms in C#.
5. Compare their behavior and basic complexity.

# Part I — Introduction to Sorting

## 1. What Is Sorting?
Sorting arranges data in a specified order.

```text
Unsorted: 78, 92, 65, 85, 70
Ascending: 65, 70, 78, 85, 92
Descending: 92, 85, 78, 70, 65
```

Sorting can make data easier to read, compare, report, and search using algorithms that require sorted data.

# Part II — Bubble Sort

## 2. What Is Bubble Sort?
Bubble Sort repeatedly compares **adjacent elements** and swaps them if they are in the wrong order. In ascending order, swap when the left value is greater than the right value. After each pass, the largest value in the unsorted section moves to its end.

## 3. Worked Example
Sort `5, 3, 8, 4, 2` in ascending order.

**Pass 1**

| Comparison | Action | Array |
|---|---|---|
| 5 and 3 | Swap | 3, 5, 8, 4, 2 |
| 5 and 8 | No swap | 3, 5, 8, 4, 2 |
| 8 and 4 | Swap | 3, 5, 4, 8, 2 |
| 8 and 2 | Swap | 3, 5, 4, 2, 8 |

**Pass 2:** Compare within the remaining unsorted section.
- 3 and 5: no swap → `3, 5, 4, 2, 8`
- 5 and 4: swap → `3, 4, 5, 2, 8`
- 5 and 2: swap → `3, 4, 2, 5, 8`

**Pass 3**
- 3 and 4: no swap → `3, 4, 2, 5, 8`
- 4 and 2: swap → `3, 2, 4, 5, 8`

**Pass 4**
- 3 and 2: swap → `2, 3, 4, 5, 8`

Sorted result: `2, 3, 4, 5, 8`.

## 4. Bubble Sort Pseudocode
```text
FOR pass = 0 TO length - 2
    FOR i = 0 TO length - 2 - pass
        IF array[i] > array[i + 1] THEN
            SWAP array[i] and array[i + 1]
        END IF
    END FOR
END FOR
```

## 5. Bubble Sort in C#
```csharp
int[] numbers = { 5, 3, 8, 4, 2 };

for (int pass = 0; pass < numbers.Length - 1; pass++)
{
    for (int i = 0; i < numbers.Length - 1 - pass; i++)
    {
        if (numbers[i] > numbers[i + 1])
        {
            int temp = numbers[i];
            numbers[i] = numbers[i + 1];
            numbers[i + 1] = temp;
        }
    }
}

for (int i = 0; i < numbers.Length; i++)
{
    Console.Write(numbers[i] + " ");
}
```

Expected output:
```text
2 3 4 5 8
```

## 6. Understanding the Swap
```csharp
int temp = numbers[i];
numbers[i] = numbers[i + 1];
numbers[i + 1] = temp;
```
`temp` preserves one value while the two elements are exchanged.

## 7. Bubble Sort Complexity
For the basic nested-loop version shown:
- Best case: O(n²)
- Average case: O(n²)
- Worst case: O(n²)
- Auxiliary space: O(1)

An optimized version that stops when a pass makes no swaps can achieve O(n) best-case time. That optimization is optional for this lesson.

# Part III — Selection Sort

## 8. What Is Selection Sort?
Selection Sort repeatedly finds the smallest value in the unsorted section and places it at the beginning of that section.

Steps:
1. Assume the first unsorted element is the minimum.
2. Search the remaining unsorted elements for a smaller value.
3. Swap the minimum with the first unsorted element.
4. Repeat for the next position.

## 9. Worked Example
Sort `5, 3, 8, 4, 2`.

- **Pass 1:** Minimum is 2. Swap with 5 → `2, 3, 8, 4, 5`
- **Pass 2:** Minimum of `3, 8, 4, 5` is 3 → `2, 3, 8, 4, 5`
- **Pass 3:** Minimum of `8, 4, 5` is 4. Swap with 8 → `2, 3, 4, 8, 5`
- **Pass 4:** Minimum of `8, 5` is 5. Swap with 8 → `2, 3, 4, 5, 8`

## 10. Selection Sort Pseudocode
```text
FOR i = 0 TO length - 2
    minIndex = i

    FOR j = i + 1 TO length - 1
        IF array[j] < array[minIndex] THEN
            minIndex = j
        END IF
    END FOR

    IF minIndex is not i THEN
        SWAP array[i] and array[minIndex]
    END IF
END FOR
```

## 11. Selection Sort in C#
```csharp
int[] numbers = { 5, 3, 8, 4, 2 };

for (int i = 0; i < numbers.Length - 1; i++)
{
    int minIndex = i;

    for (int j = i + 1; j < numbers.Length; j++)
    {
        if (numbers[j] < numbers[minIndex])
        {
            minIndex = j;
        }
    }

    if (minIndex != i)
    {
        int temp = numbers[i];
        numbers[i] = numbers[minIndex];
        numbers[minIndex] = temp;
    }
}

for (int i = 0; i < numbers.Length; i++)
{
    Console.Write(numbers[i] + " ");
}
```

Expected output:
```text
2 3 4 5 8
```

## 12. Selection Sort Complexity
- Best case: O(n²)
- Average case: O(n²)
- Worst case: O(n²)
- Auxiliary space: O(1)

Selection Sort continues scanning the unsorted section to find its minimum, even if the array is already sorted.

# Part IV — Compare the Algorithms

| Feature | Bubble Sort | Selection Sort |
|---|---|---|
| Main operation | Compare adjacent elements | Find minimum in unsorted section |
| Swapping | May swap many times in a pass | Usually at most one swap per pass |
| Worst-case time | O(n²) | O(n²) |
| Auxiliary space | O(1) | O(1) |

Both are introductory algorithms. Their value here is learning how sorting works and how to trace algorithm steps.

# Part V — Practice Set

## Practice 1 — Trace Bubble Sort
Given `7, 4, 9, 2`, sort in ascending order.
a. Show the array after every swap.  
b. Show the result after each complete pass.  
c. Write the final sorted array.

## Practice 2 — Trace Selection Sort
Given `6, 3, 8, 1, 5`, sort in ascending order.
a. Record the minimum found in each pass.  
b. Record the array after each pass.  
c. Write the final result.

## Practice 3 — Descending Order
Given `12, 5, 9, 3, 15`, identify the comparison condition to change in Bubble Sort for descending order. Trace the first pass.

## Practice 4 — Compare Swaps
Given `4, 1, 3, 2`:
a. Trace Bubble Sort.  
b. Trace Selection Sort.  
c. Count swaps for each.  
d. Explain why the swap counts differ.

## Practice 5 — C# Implementation
Write a console program that displays `34, 12, 25, 9, 18`, sorts the array using Bubble Sort, and displays the result. Then modify it to use Selection Sort.

# Key Takeaways
- Bubble Sort compares adjacent values and swaps out-of-order pairs.
- Selection Sort finds the minimum in the unsorted section and places it next.
- Both standard implementations have O(n²) worst-case time.
- Tracing makes the algorithm's data changes visible.
