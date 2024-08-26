# Selection Sort

## Problem Statement

Selection sort is a sorting algorithm that works by repeatedly finding the minimum element from the unsorted part of the array and putting it at the beginning of the unsorted region of the array.

You are given an unsorted array consisting of `N` non-negative integers. Your task is to sort the array in non-decreasing order using the Selection Sort algorithm.

### Example

Selection Sort implementation for the given array `{29, 72, 98, 13, 87, 66, 52, 51, 36}` 

```plaintext
Initial array: {29, 72, 98, 13, 87, 66, 52, 51, 36}

Step 1: Find the minimum element in the unsorted part {29, 72, 98, 13, 87, 66, 52, 51, 36}, which is 13, and swap it with the first element. 
New array: {13, 72, 98, 29, 87, 66, 52, 51, 36}

Step 2: The next minimum element is 29. Swap it with the second element. 
New array: {13, 29, 98, 72, 87, 66, 52, 51, 36}

Step 3: Continue finding the minimum element and swapping until the entire array is sorted.
Final sorted array: {13, 29, 36, 51, 52, 66, 72, 87, 98}
```

### Constraints

- `1 <= T <= 100`
- `1 <= N <= 100`
- `1 <= Arr[i] <= 1000`

Where:
- `T` represents the number of test cases.
- `N` represents the size of the array.
- `Arr[i]` represents the elements of the array.

**Time Limit:** 1 second

### Sample Input 1

```plaintext
1
5
6 2 8 4 10
```

### Sample Output 1

```plaintext
2 4 6 8 10
```

**Explanation:**

- In the first step, the minimum element is 2. It is swapped with the starting element of the unsorted region.
- In the second step, 4 is the minimum element. It is swapped with the next starting element.
- Similarly, in the third step, the minimum element is 6, which is swapped accordingly.
- In the final step, all elements are arranged in non-decreasing order, and the array is sorted.

### Sample Input 2

```plaintext
2
2
1 2
4
4 3 2 1
```

### Sample Output 2

```plaintext
1 2
1 2 3 4
```

---

## Code
```cpp
#include <bits/stdc++.h> 
void selectionSort(vector<int>& arr, int n)
{   
    for(int i = 0; i < n-1; i++ )
    {
        int minIndex = i;
        for(int j = i + 1;j < n ;j++)
        {
            if(arr[j] < arr[minIndex])
            minIndex = j;
        }
        swap(arr[minIndex],arr[i]);
    }
```
}
