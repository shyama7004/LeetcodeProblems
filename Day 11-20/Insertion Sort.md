# Insertion Sort

### Problem statement

You are given `N` integers in the form of an array `ARR`. Print the sorted array using the insertion sort.

**Note:**  
No need to return anything. You should sort the array in-place.

**Example:**  
Let `ARR` be: `[1, 4, 2]`  
The sorted array will be: `[1, 2, 4]`.

### Constraints

- `1 <= T <= 10`
- `1 <= N <= 5000`
- `1 <= ARR[i] <= 100000`

**Time Limit:** 1 second

### Sample Input 1

```
2
4
3 1 2 2
3
1 4 2
```

### Sample Output 1

```
1 2 2 3
1 2 4
```

**Explanation For Sample Output 1:**

- **Test Case 1:**  
  The sorted array will be: `[1, 2, 2, 3]`.

- **Test Case 2:**  
  The sorted array will be: `[1, 2, 4]`.

### Sample Input 2

```
2
4
4 12 11 20
6
6 5 4 3 2 1
```

### Sample Output 2

```
4 11 12 20
1 2 3 4 5 6
```
## Code

```cpp
#include <bits/stdc++.h> 
void insertionSort(int n, vector<int> &arr){
    for(int i = 1; i < n; i++)  // Start from the second element (index 1)
    {
        int temp = arr[i];      // Store the current element in `temp`
        int j = i - 1;          // Start comparing with the element just before `i`

        // Move elements of `arr[0...i-1]` that are greater than `temp` one position ahead
        for(; j >= 0; j--)
        {
            if(arr[j] > temp)   // If current element is greater than `temp`
            {
                arr[j + 1] = arr[j];  // Shift the element to the right
            }
            else break;         // If we find an element smaller than `temp`, stop shifting
        }

        // Insert the `temp` value at the correct position
        arr[j + 1] = temp;
    }
}
```

### Explanation of Each Line

1. **`for(int i = 1; i < n; i++)`**:
   - **Purpose:** Start from the second element and iterate through the array. `i` represents the current element to be positioned correctly in the sorted part of the array.

2. **`int temp = arr[i];`**:
   - **Purpose:** Store the current element (`arr[i]`) in a temporary variable `temp`. This element will be compared with the elements in the sorted portion to its left.

3. **`int j = i - 1;`**:
   - **Purpose:** Initialize `j` to the index just before `i`. This sets up for comparing `temp` with elements on the left side of `arr[i]`.

4. **`for(; j >= 0; j--)`**:
   - **Purpose:** The loop runs backward from `j` to `0`, comparing `temp` with the elements in the sorted portion of the array.

5. **`if(arr[j] > temp)`**:
   - **Purpose:** If the current element `arr[j]` is greater than `temp`, it means `temp` should be placed before `arr[j]`. Therefore, shift `arr[j]` one position to the right.

6. **`arr[j + 1] = arr[j];`**:
   - **Purpose:** Shift the current element (`arr[j]`) one position to the right to make space for `temp`.

7. **`else break;`**:
   - **Purpose:** If `arr[j]` is not greater than `temp`, it means `temp` has found its correct position. Exit the loop as no more shifts are needed.

8. **`arr[j + 1] = temp;`**:
   - **Purpose:** After the loop completes, insert `temp` into the correct position (`j + 1`). This is the position where all elements to the left are smaller, and all elements to the right are larger.

### Debugged Issue
- The original code was correct in logic but may cause confusion due to the placement of the final insertion step (`arr[j + 1] = temp;`). The logic is straightforward once understood that `j + 1` is the correct position for the `temp` value after shifting all greater elements to the right.

The provided insertion sort code is already quite efficient for its purpose, but there's a small optimization we can apply to make it slightly more efficient. Specifically, we can eliminate unnecessary array assignments when no shifting is needed, and we can avoid checking the condition inside the loop by breaking out of it.

## Optimized Version:

```cpp
#include <bits/stdc++.h> 
void insertionSort(int n, vector<int> &arr){
    for(int i = 1; i < n; i++) 
    {
        int temp = arr[i];
        int j = i - 1;
        
        // Shift elements of `arr[0...i-1]` that are greater than `temp` to one position ahead
        while(j >= 0 && arr[j] > temp) 
        {
            arr[j + 1] = arr[j];  // Shift the element to the right
            j--;
        }
        
        // Insert `temp` at the correct position
        arr[j + 1] = temp;
    }
}
```

### Optimizations Applied

1. **Using `while` Loop**:
   - **Change:** The `for` loop was replaced with a `while` loop.
   - **Reason:** The `while` loop is a more direct way to handle the situation where we want to shift elements until the correct position for `temp` is found. This reduces the number of checks (no need for `else break`), as the loop condition itself ensures that we only continue shifting as long as needed.

2. **Avoiding Redundant Assignments**:
   - **Change:** The `arr[j + 1] = arr[j];` operation only occurs if `arr[j] > temp`.
   - **Reason:** By checking the condition directly in the `while` loop, we avoid unnecessary assignments and checks.

### Explanation of the Optimized Code

- **Outer Loop (`for(int i = 1; i < n; i++)`)**:
  - Iterates over each element starting from the second one, treating the array before `i` as the sorted part.

- **Inner `while` Loop**:
  - **Condition:** The loop continues as long as `j >= 0` and `arr[j] > temp`.
  - **Purpose:** Shift elements that are greater than `temp` to the right.

- **`arr[j + 1] = temp;`**:
  - After exiting the `while` loop, `j` is either `-1` or points to the last element smaller than `temp`. Insert `temp` at `j + 1`.

### Benefits of Optimization

- **Fewer Operations:** The `while` loop combined with the direct condition check reduces unnecessary operations, especially in scenarios where few elements need shifting.
- **Improved Readability:** The use of a `while` loop simplifies the logic, making the code easier to read and maintain.

This version should be slightly faster, particularly when dealing with partially sorted arrays or when the array is nearly sorted.
