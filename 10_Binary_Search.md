## Week 10: Binary Search

## Learning Outcomes

At the end of this lesson, students should be able to:

1. Explain how Binary Search works and identify when it can be used.
2. Trace Binary Search using the `low`, `high`, and `mid` positions.
3. Write pseudocode for Binary Search.
4. Implement Binary Search in C#.
5. Compare Binary Search with Sequential Search in terms of requirements and efficiency.

---

## 1. Review: Sequential Search

Sequential Search checks elements one at a time, starting from the first element, until the target is found or there are no more elements to check.

Example:

```text
Values: [18, 7, 25, 12, 30]
Target: 12
```

The search checks `18`, then `7`, then `25`, and finally `12`. The target is found at index `3`.

Sequential Search does not require the array to be sorted.

### Think About This

If an array contains 1,000 values arranged in increasing order, do we always need to start at the first value and check each element one by one?

Binary Search provides another approach, but it requires sorted data.

---

## 2. What Is Binary Search?

**Binary Search** finds a target in a sorted collection by repeatedly checking the middle element and eliminating half of the remaining search range.

Instead of checking every element in order, it asks:

- Is the middle value the target?
- Is the target smaller than the middle value?
- Is the target larger than the middle value?

Because the values are sorted, the algorithm can determine which half may contain the target.

### Important Requirement

**The data must be sorted before Binary Search is used.**

For an array sorted in ascending order:

- If `target == values[mid]`, the target is found.
- If `target < values[mid]`, continue in the left half.
- If `target > values[mid]`, continue in the right half.

If the array is not sorted, these decisions may eliminate the half that contains the target, producing an incorrect result.

---

## 3. Understanding `low`, `high`, and `mid`

Binary Search keeps track of the part of the array that may still contain the target.

- `low`: index of the first position in the current search range.
- `high`: index of the last position in the current search range.
- `mid`: index of the middle position in the current search range.

Calculate the middle index using:

```text
mid = low + (high - low) / 2
```

For integer indexes, division produces an integer result.

Initially:

```text
low = 0
high = array length - 1
```

After checking the middle value:

- Search left: `high = mid - 1`
- Search right: `low = mid + 1`

The `- 1` and `+ 1` ensure the middle element that was already checked is not checked again.

If `low > high`, the search range is empty and the target is not in the array.

---

## 4. Worked Example: Find 23

Given the sorted array:

```text
Index:   0   1   2   3   4   5   6
Values:  3   8  12  17  23  31  42
Target: 23
```

### Trace

| Step | `low` | `high` | `mid` | `values[mid]` | Decision |
|---|---:|---:|---:|---:|---|
| 1 | 0 | 6 | 3 | 17 | 23 is greater than 17; search right |
| 2 | 4 | 6 | 5 | 31 | 23 is less than 31; search left |
| 3 | 4 | 4 | 4 | 23 | Target found |

The target is found at index `4`.

Notice that the algorithm did not need to check every value.

---

## 5. Worked Example: Target Not Found

Given the same array:

```text
Index:   0   1   2   3   4   5   6
Values:  3   8  12  17  23  31  42
Target: 20
```

| Step | `low` | `high` | `mid` | `values[mid]` | Decision |
|---|---:|---:|---:|---:|---|
| 1 | 0 | 6 | 3 | 17 | 20 is greater than 17; search right |
| 2 | 4 | 6 | 5 | 31 | 20 is less than 31; search left |
| 3 | 4 | 4 | 4 | 23 | 20 is less than 23; search left |

After Step 3, update `high = mid - 1`, so `high = 3`.

Now `low = 4` and `high = 3`. Since `low > high`, the target is not found.

The algorithm returns `-1` to indicate that the target is absent.

---

## 6. Binary Search Algorithm

### Pseudocode

```text
Algorithm BinarySearch(values, target)
    low = 0
    high = length(values) - 1

    while low <= high
        mid = low + (high - low) / 2

        if values[mid] == target
            return mid
        else if target < values[mid]
            high = mid - 1
        else
            low = mid + 1

    return -1
```

### How the Algorithm Works

1. Start with the entire array as the search range.
2. Calculate the middle index.
3. Compare the middle value with the target.
4. Return the middle index if the target is found.
5. Otherwise, eliminate the half that cannot contain the target.
6. Repeat while a valid search range remains.
7. Return `-1` if the target is not found.

---

## 7. C# Implementation

The following program searches for a value in an array sorted in ascending order.

```csharp
using System;

class Program
{
    static int BinarySearch(int[] values, int target)
    {
        int low = 0;
        int high = values.Length - 1;

        while (low <= high)
        {
            int mid = low + (high - low) / 2;

            if (values[mid] == target)
            {
                return mid;
            }
            else if (target < values[mid])
            {
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }

        return -1;
    }

    static void Main()
    {
        int[] values = { 3, 8, 12, 17, 23, 31, 42 };

        Console.Write("Enter the value to search for: ");
        int target = Convert.ToInt32(Console.ReadLine());

        int result = BinarySearch(values, target);

        if (result != -1)
        {
            Console.WriteLine("Value found at index: " + result);
        }
        else
        {
            Console.WriteLine("Value not found.");
        }
    }
}
```

### Sample Run 1

```text
Enter the value to search for: 23
Value found at index: 4
```

### Sample Run 2

```text
Enter the value to search for: 20
Value not found.
```

### Code Reminders

- Array indexes begin at `0`.
- `values.Length - 1` is the last valid index.
- `while (low <= high)` means there is still at least one index to examine.
- The method returns an index, not the value itself.
- This program assumes that `values` is sorted in ascending order.

---

## 8. Binary Search vs. Sequential Search

| Feature | Sequential Search | Binary Search |
|---|---|---|
| How it searches | Checks elements one by one | Checks the middle of the current range |
| Must data be sorted? | No | Yes, for this implementation |
| Best-case time | `O(1)` | `O(1)` |
| Worst-case time | `O(n)` | `O(log n)` |
| General approach | Move to the next element | Eliminate half of the remaining range |

### Understanding `O(log n)`

Binary Search reduces the search range by about half after each comparison.

For example, with 16 sorted elements, the range can shrink approximately as follows:

```text
16 → 8 → 4 → 2 → 1
```

This is why Binary Search has logarithmic time complexity, written as **`O(log n)`**.

Sequential Search may need to examine every element in the worst case, so its time complexity is **`O(n)`**.

The time needed to sort data is not included in the Binary Search complexity above. If data must be sorted first, that preparation work should also be considered when choosing an approach.

---

## 9. Guided Practice

Use the sorted array below for each question:

```text
Index:   0   1   2   3   4   5   6   7   8
Values:  4   9  13  18  24  29  35  41  50
```

### Task A: Trace Binary Search

Find the target `29`.

Complete the trace table.

| Step | `low` | `high` | `mid` | `values[mid]` | Decision / update |
|---|---|---|---|---|---|
| 1 |  |  |  |  |  |
| 2 |  |  |  |  |  |
| 3 |  |  |  |  |  |

State the index where the target is found.

### Task B: Target Not Found

Use the same array to search for `30`.

1. Record each `low`, `high`, and `mid`.
2. Record the value checked at each step.
3. Show when the search ends.
4. State the result returned by the algorithm.

### Task C: Identify the Problem

A student writes Binary Search for this array:

```text
{ 18, 4, 29, 9, 41, 13 }
```

The student searches for `29` and reports that the target is not found.

1. What requirement did the student overlook?
2. Why can Binary Search give an incorrect result with this array?
3. What should be done before using Binary Search?

---

## 10. Individual Exercise: Search for a Student Number

A class maintains student numbers in ascending order:

```text
{ 20261003, 20261008, 20261012, 20261019,
  20261025, 20261031, 20261044, 20261050 }
```

Write a C# program that:

1. Stores the student numbers in an array.
2. Asks the user to enter a student number.
3. Uses a separate `BinarySearch` method to search for the number.
4. Displays the index if the number is found.
5. Displays `Student number not found.` if it is absent.
6. Uses `-1` as the not-found return value.

Test your program with:

- A student number at the beginning of the array.
- A student number at the end of the array.
- A student number in the middle.
- A student number that is not in the array.

### Explain Your Solution

After testing, answer:

1. Why is Binary Search suitable for this array?
2. What would need to change if the student numbers were not sorted?
3. What is the worst-case time complexity of the search method?
4. How is the search range updated when the target is smaller than the middle value?

---

## 11. Exit Check

Answer briefly without running the program.

1. What is the main requirement for Binary Search?
2. If `values[mid]` is greater than the target, which variable is updated, and how?
3. What does `low > high` tell us?
4. What value does the sample method return when the target is not found?
5. Which has better worst-case time complexity for a sorted array: Sequential Search or Binary Search? Explain briefly.

---

## Key Points

- Binary Search works on sorted data.
- `low`, `high`, and `mid` define and locate the current search range.
- Each unsuccessful comparison eliminates approximately half of the remaining range.
- Return the index when the target is found; return `-1` when it is absent.
- Binary Search has worst-case time complexity `O(log n)`, while Sequential Search has worst-case time complexity `O(n)`.
