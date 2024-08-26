# Bubble Sort

## Problem Statement

Bubble Sort is a simple sorting algorithm that works by repeatedly swapping adjacent elements if they are in the wrong order. The goal is to sort an array of `N` non-negative integers in non-decreasing order using the Bubble Sort algorithm.

### Example

Consider the following array: `{6, 2, 8, 4, 10}`. After applying Bubble Sort, the array becomes `{2, 4, 6, 8, 10}`.

### Input/Output Format

- **Input:**
  - The first line contains an integer `T`, the number of test cases.
  - For each test case:
    - An integer `N`, the size of the array.
    - A line with `N` space-separated integers, representing the elements of the array.

- **Output:**
  - For each test case, print the sorted array in a single line.

### Constraints
- `1 <= T <= 100`
- `1 <= N <= 100`
- `1 <= Arr[i] <= 1000`
### Time Limit: 1 second

---

## Example

### Sample Input 1

```
1
5
6 2 8 4 10
```

### Sample Output 1

```
2 4 6 8 10
```

### Sample Input 2

```
2
2
1 2
4
4 3 2 1
```

### Sample Output 2

```
1 2
1 2 3 4
```

---

## Bubble Sort Algorithm

### Basic Implementation

```cpp
#include <bits/stdc++.h> 
void bubbleSort(vector<int>& arr, int n) {   
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < n - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                std::swap(arr[j], arr[j + 1]);
            }
        }
    }
}
```

### How It Works

Bubble Sort works by repeatedly stepping through the list, comparing each pair of adjacent items, and swapping them if they are in the wrong order. The process repeats until no swaps are needed, which means the list is sorted.

#### Outer Loop (`for(int i = 1; i < n; i++)`)

- **Purpose:** Controls the number of passes over the array.
- **Range:** `i` runs from `1` to `n-1`.
- **Effect:** After each pass, the largest unsorted element moves to its correct position.

#### Inner Loop (`for(int j = 0; j < n - 1; j++)`)

- **Purpose:** Compares and swaps adjacent elements if necessary.
- **Range:** `j` runs from `0` to `n-2`.
- **Effect:** In each pass, the largest element "bubbles up" to its correct position at the end.

---

## Optimization of Bubble Sort

### Optimized Code

```cpp
#include <bits/stdc++.h> 
void bubbleSort(vector<int>& arr, int n) {   
    for (int i = 1; i < n; i++) {
        bool swapped = false;
        for (int j = 0; j < n - i; j++) {
            if (arr[j] > arr[j + 1]) {
                std::swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        if (!swapped)
            break;  // If no elements were swapped, array is already sorted
    }
}
```

### Explanation of Optimizations

- **Early Exit:** The `swapped` flag is used to check if any elements were swapped during a pass. If no swaps occur, the array is already sorted, and the algorithm exits early, saving unnecessary comparisons.
  
- **Reduced Comparisons:** By modifying the inner loop to `j < n - i`, the number of comparisons is reduced in each subsequent pass since the last `i` elements are already sorted.

---

## Detailed Breakdown

### Example Walkthrough

For the array `[6, 2, 8, 4, 10]`:

- **First Pass (i=1):**
  - Compare 6 and 2 → Swap → Array becomes `[2, 6, 8, 4, 10]`
  - Compare 6 and 8 → No swap
  - Compare 8 and 4 → Swap → Array becomes `[2, 6, 4, 8, 10]`
  - Compare 8 and 10 → No swap

- **Second Pass (i=2):**
  - Compare 2 and 6 → No swap
  - Compare 6 and 4 → Swap → Array becomes `[2, 4, 6, 8, 10]`
  - Compare 6 and 8 → No swap
  - Compare 8 and 10 → No swap

The array is now sorted: `[2, 4, 6, 8, 10]`.

### Time Complexity

- **Worst-Case Time Complexity:** \(O(n^2)\), where `n` is the number of elements.
- **Best-Case Time Complexity (Optimized):** \(O(n)\) when the array is already sorted.

### Space Complexity

- **Space Complexity:** \(O(1)\) as Bubble Sort is an in-place sorting algorithm.

---

<details>
<summary>Homework</summary>

### Question - 1 : Can you use `for(int i = 0; i < n - 1; i++)` in the outer loop, and  will it work correctly ?

Yes, you can use `for(int i = 0; i < n - 1; i++)` in the outer loop, and it will work correctly. Here’s the logic behind this approach:

### Updated Code

```cpp
#include <bits/stdc++.h> 
void bubbleSort(vector<int>& arr, int n)
{   
    for(int i = 0; i < n - 1; i++)
    {
        for(int j = 0; j < n - i - 1; j++)
        {
            if(arr[j] > arr[j + 1])
            {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}
```

### Explanation

- **Outer Loop (`for(int i = 0; i < n - 1; i++)`)**:
  - **Purpose:** The loop runs `n-1` times to ensure that the array is fully sorted.
  - **Range:** `i` runs from `0` to `n-2`. This means the loop iterates `n-1` times, which is the number of passes required to sort the array.
  - **Effect:** With each pass, the largest unsorted element is moved to its correct position at the end of the unsorted portion of the array. 

- **Inner Loop (`for(int j = 0; j < n - i - 1; j++)`)**:
  - **Purpose:** This loop compares and swaps adjacent elements if they are out of order.
  - **Range:** `j` runs from `0` to `n-i-2`. The range decreases by one with each pass of the outer loop (`i` increases) because the last `i` elements are already sorted and in their correct positions.
  - **Effect:** This optimization reduces the number of comparisons in each pass since the end of the array is already sorted.

### Logic Behind Using `i = 0` Instead of `i = 1`

Starting `i` from `0` and running it up to `n-2` still results in `n-1` passes over the array, which is sufficient to sort the array completely. 

- **Comparison and Swapping:** The inner loop compares elements in pairs, and since the last `i` elements are sorted after each pass, we reduce the number of comparisons accordingly (`n-i-1`).
  
- **Final Pass:** By the time the outer loop completes all its passes, the array will be fully sorted, as the inner loop handles the necessary swapping.

### Example Walkthrough

For an array `[6, 2, 8, 4, 10]`:

- **First Pass (`i = 0`):**
  - `j` runs from `0` to `3` (4 comparisons).
  - After the pass, the array might become `[2, 6, 4, 8, 10]`.

- **Second Pass (`i = 1`):**
  - `j` runs from `0` to `2` (3 comparisons).
  - The array becomes `[2, 4, 6, 8, 10]`.

- **Subsequent Passes:** They ensure the array is sorted, with fewer comparisons each time.

This approach is slightly more efficient than the original code, as it avoids unnecessary comparisons in already sorted portions of the array.

### Question - 2: Is this bubble sort stable or unstable ?

This Bubble Sort implementation is **stable** because it only swaps adjacent elements when they are out of order. If two elements are equal, they won't be swapped, preserving their original relative order in the array. Thus, it maintains the relative positioning of elements with equal values, which is the defining characteristic of a stable sorting algorithm.

### Question - 3: What is In - place sort ?

An **in-place sort** refers to a sorting algorithm that sorts the elements of a collection (like an array or list) without requiring additional storage space proportional to the size of the collection. Here are the key points:

- **No Extra Space:** Uses a constant amount of extra memory, typically \(O(1)\), meaning it doesn't require additional arrays or data structures for sorting.
- **Original Array:** The sorting is done by modifying the original array or list directly.
- **Efficiency:** In-place sorting algorithms are space-efficient, especially for large datasets, as they minimize memory usage.
- **Examples:** Common in-place sorting algorithms include Bubble Sort, Insertion Sort, and Selection Sort.
- **Contrast:** Non in-place sorts, like Merge Sort, require extra memory for temporary storage of elements during the sorting process.
</details>

For `geeks for geeks` quiz [click here](https://www.geeksforgeeks.org/quizzes/top-mcqs-on-bubblesort-algorithm-with-answers/)
