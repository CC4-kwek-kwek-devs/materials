## Week 12 — Sorting Algorithms II: Insertion Sort and Comparison

## Learning Objectives

Students should be able to:

1. Explain how Insertion Sort works.
2. Trace it pass by pass.
3. Implement it in C#.
4. Compare Insertion Sort with Bubble Sort and Selection Sort.
5. Identify basic best-, average-, and worst-case behavior.
6. Justify a simple sorting-algorithm choice for a given scenario.

# Part I — Review

Sorting arranges data in a specified order.

```text
Unsorted: 9, 4, 7, 2, 6
Ascending: 2, 4, 6, 7, 9
```

- **Bubble Sort:** compares adjacent elements and swaps them when out of order.
- **Selection Sort:** finds the smallest value in the unsorted section and places it next.

# Part II — Insertion Sort

## 1. What Is Insertion Sort?

Insertion Sort builds a sorted section one element at a time. It takes the next value and inserts it into its correct position among the values already sorted.

Think of arranging playing cards in your hand: pick up the next card, move larger cards to make room, and insert the card in order.

## 2. Main Steps

For ascending order:

1. Treat the first element as the initial sorted section.
2. Select the next element as the `key`.
3. Compare the key with elements to its left.
4. Shift elements larger than the key one position right.
5. Insert the key into the open position.
6. Repeat until all elements are processed.

## 3. Worked Example

Given `7, 4, 5, 2`.

- **Initial:** `7, 4, 5, 2` — treat `7` as sorted.
- **Pass 1, key = 4:** shift 7 right and insert 4 → `4, 7, 5, 2`
- **Pass 2, key = 5:** shift 7 right and insert 5 after 4 → `4, 5, 7, 2`
- **Pass 3, key = 2:** shift 7, 5, and 4 right; insert 2 at the beginning → `2, 4, 5, 7`

| Pass | Key | Action | Array after insertion |
| --- | --- | --- | --- |
| Initial | —   | First element is sorted section | 7, 4, 5, 2 |
| 1   | 4   | Shift 7; insert 4 | 4, 7, 5, 2 |
| 2   | 5   | Shift 7; insert 5 | 4, 5, 7, 2 |
| 3   | 2   | Shift 7, 5, 4; insert 2 | 2, 4, 5, 7 |

## 4. Insertion Sort Pseudocode

```text
FOR i = 1 TO length - 1
    key = array[i]
    j = i - 1

    WHILE j >= 0 AND array[j] > key
        array[j + 1] = array[j]
        j = j - 1
    END WHILE

    array[j + 1] = key
END FOR
```

## 5. Insertion Sort in C#

```csharp
int[] numbers = { 7, 4, 5, 2 };

for (int i = 1; i < numbers.Length; i++)
{
    int key = numbers[i];
    int j = i - 1;

    while (j >= 0 && numbers[j] > key)
    {
        numbers[j + 1] = numbers[j];
        j--;
    }

    numbers[j + 1] = key;
}

Console.WriteLine("Sorted array:");
for (int i = 0; i < numbers.Length; i++)
{
    Console.Write(numbers[i] + " ");
}
```

Expected output:

```text
Sorted array:
2 4 5 7
```

## 6. Why Store a Key?

```csharp
int key = numbers[i];
```

The key stores the value being inserted. Larger values may be shifted over its original position, so the key must be preserved. After shifting, it is placed at `numbers[j + 1]`.

# Part III — Analyze Insertion Sort

## 7. Best Case

Already sorted input: `1, 2, 3, 4, 5`.

Each key needs little work and no shifts are needed. Best-case time is **O(n)**.

## 8. Worst Case

Reverse order: `5, 4, 3, 2, 1`.

Each new key may need to pass all elements in the sorted section. Worst-case time is **O(n²)**.

## 9. Average Case

For typical unsorted input, elements may need to be shifted. Average-case time is **O(n²)**.

Auxiliary space for the standard in-place implementation is **O(1)**.

# Part IV — Compare Three Sorting Algorithms

## 10. How They Work

**Bubble Sort**

- Compares adjacent values.
- Swaps them if out of order.
- Repeats passes.

**Selection Sort**

- Finds the minimum in the unsorted section.
- Places it at the beginning of that section.
- Repeats for the remaining values.

**Insertion Sort**

- Takes the next value as a key.
- Shifts larger values to the right.
- Inserts the key into the sorted section.

## 11. Complexity Comparison

| Algorithm | Best Case | Average Case | Worst Case | Auxiliary Space |
| --- | --- | --- | --- | --- |
| Bubble Sort, basic version | O(n²) | O(n²) | O(n²) | O(1) |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) |

**Note:** An optimized Bubble Sort that stops after a pass with no swaps has O(n) best-case time. The table describes the basic Bubble Sort from Week 11.

## 12. Operational Comparison

| Question | Bubble Sort | Selection Sort | Insertion Sort |
| --- | --- | --- | --- |
| Main focus | Adjacent pairs | Minimum of unsorted section | Correct position for key |
| Main movement | Swaps | Usually one swap per pass | Shifts |
| Already-sorted data | Basic version still does nested-loop passes | Still scans unsorted section | Performs relatively little work |
| Worst case | O(n²) | O(n²) | O(n²) |

## 13. Which Should We Choose?

- Bubble Sort is useful for demonstrating adjacent comparisons and swaps.
- Selection Sort is useful for demonstrating minimum selection.
- Insertion Sort can be a good simple choice for small or nearly sorted data because it may need fewer shifts.

These are introductory algorithms. Real applications often use more advanced or library-provided sorting methods.

# Part V — Practice Set

## Practice 1 — Trace Insertion Sort

Given `8, 3, 6, 2, 5`, sort in ascending order.
a. Record the key for each pass.  
b. Show which values shift right.  
c. Show the array after each insertion.  
d. Give the final result.

## Practice 2 — Already Sorted Data

Given `2, 4, 6, 8, 10`:
a. Trace Insertion Sort.  
b. How many elements are shifted?  
c. Why is this a favorable input?

## Practice 3 — Reverse-Ordered Data

Given `9, 7, 5, 3, 1`:
a. Trace the first two passes.  
b. Explain why more shifting is required.  
c. Identify the worst-case complexity.

## Practice 4 — Compare Algorithms

Given `6, 2, 5, 1`:
a. Sort a copy using Bubble Sort.  
b. Sort a copy using Selection Sort.  
c. Sort a copy using Insertion Sort.  
d. Record the array after each pass.  
e. Explain how their movements differ.

## Practice 5 — C# Implementation

Write a console application that:

1. Stores `40, 15, 30, 10, 25` in an array.
2. Displays the original array.
3. Sorts it using Insertion Sort.
4. Displays the sorted array.

Test it with an already-sorted array, a reverse-ordered array, and an array with duplicate values.

## Practice 6 — Choose and Explain

Choose one algorithm and explain your reasoning.

**A.** You want to demonstrate adjacent comparisons and swaps.  
**B.** You want to demonstrate selecting the smallest remaining value.  
**C.** You need a simple sorting method for a small, nearly sorted array.

# Part VI — Short Assessment

1. What is the purpose of sorting?
2. How does Bubble Sort work?
3. How does Selection Sort work?
4. How does Insertion Sort work?
5. Which algorithm has O(n) best-case time in its standard implementation?
6. Why does Selection Sort still scan the unsorted section when data is already sorted?
7. Why can Insertion Sort work well on nearly sorted data?
8. What is the worst-case time complexity of all three algorithms?
9. Why is tracing useful?
10. Explain the difference between a comparison, a swap, and a shift.

# Key Takeaways

- Bubble Sort repeatedly compares adjacent values.
- Selection Sort repeatedly selects the minimum in the unsorted section.
- Insertion Sort inserts each next value into its correct position in the sorted section.
- All three standard algorithms have O(n²) worst-case time.
- Insertion Sort has O(n) best-case time on already-sorted input.
- Tracing makes data changes visible and helps identify errors.
