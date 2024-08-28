# Search In Rotated Sorted Array

## Problem Statement

You have been given a sorted array/list `arr` consisting of `n` elements. You are also given an integer `k`.

Now the array is rotated at some pivot point unknown to you.

For example, if `arr = [1, 3, 5, 7, 8]`, then after rotating `arr` at index 3, the array will be `arr = [7, 8, 1, 3, 5]`.

Now, your task is to find the index at which `k` is present in `arr`.

### Note:
1. If `k` is not present in `arr`, then print `-1`.
2. There are no duplicate elements present in `arr`.
3. `arr` can be rotated only in the right direction.

### Example:

**Input:**  
`arr = [12, 15, 18, 2, 4]`, `k = 2`

**Output:**  
`3`

**Explanation:**  
If `arr = [12, 15, 18, 2, 4]` and `k = 2`, then the position at which `k` is present in the array is `3` (0-indexed).

## Detailed Explanation (Input/Output Format, Notes, Images)

### Sample Input 1:
```
4 3
8 9 4 5
```

### Sample Output 1:
```
-1
```

**Explanation of Sample Output 1:**  
For the test case, `3` is not present in the array. Hence the output will be `-1`.

### Sample Input 2:
```
4 3
2 3 5 8
```

### Sample Output 2:
```
1
```

## Expected Time Complexity:
Try to do this in `O(log(n))`.

## Constraints:
- `1 <= n <= 10^5`
- `0 <= k <= 10^9`
- `0 <= arr[i] <= 10^9`

**Time Limit:** 1 second
### Logic and Intuition Behind the Solution

The problem involves finding the pivot index in a rotated sorted array. The pivot is the point where the rotation occurs, and it is the smallest element in the array. In other words, it's the point where the array starts from the lowest value after the rotation.

### Step-by-Step Explanation

#### 1. **Understanding the Pivot:**
   - In a rotated sorted array, the pivot is the index where the smallest element resides. For example, in the array `[7, 9, 10, 17, 1]`, the pivot is at index `4` (element `1`), because it's the smallest element and marks the beginning of the rotation.

#### 2. **Binary Search Approach:**
   - We can use a modified binary search to find the pivot index efficiently in `O(log n)` time.

#### 3. **Initial Setup:**
   - We start with two pointers: `s` (start) and `e` (end) pointing to the beginning and the end of the array.
   - We calculate the `mid` index as the middle of `s` and `e`.

#### 4. **Mid Comparison and Adjusting the Search Space:**
   - **Case 1:** If `arr[mid] >= arr[0]`, it means that the middle element is still part of the initial (non-rotated) part of the array. This suggests that the pivot must be to the right of `mid`. Hence, we move `s` to `mid + 1`.
   - **Case 2:** If `arr[mid] < arr[0]`, it means that the middle element is part of the rotated section, so the pivot could be at `mid` or before it. Therefore, we set `e` to `mid`.

   - The loop continues until `s < e`.

#### 5. **Finding the Pivot:**
   - When the loop exits, `s` will point to the smallest element in the array, which is the pivot. This is because `s` will eventually converge to the smallest element as we narrow down the search space.

#### 6. **Return the Pivot Index:**
   - Finally, we return `s` as the pivot index.

### Example Walkthrough
Consider the array: `[7, 9, 10, 17, 1]`

- **First Iteration:**
  - `s = 0`, `e = 4`
  - `mid = 2` (element `10`)
  - `arr[mid] (10) >= arr[0] (7)`, so `s = mid + 1 = 3`

- **Second Iteration:**
  - `s = 3`, `e = 4`
  - `mid = 3` (element `17`)
  - `arr[mid] (17) >= arr[0] (7)`, so `s = mid + 1 = 4`

- **Loop ends:**
  - `s = 4`, `e = 4`
  - The pivot index is `4`, which corresponds to the smallest element `1`.

### Complete Code
```cpp
#include<iostream>
using namespace std;

int getPivot(int arr[], int n) {
    int s = 0;
    int e = n-1;
    int mid = s + (e-s)/2;

    while (s < e) {
        if (arr[mid] >= arr[0]) {
            s = mid + 1;
        } else {
            e = mid;
        }
        mid = s + (e-s)/2;
    }
    return s;
}

int main() {
    int arr[] = {7, 9, 10, 17, 1};
    int n = 5;

    cout << "Pivot Index: " << getPivot(arr, n) << endl;

    return 0;
}
```
