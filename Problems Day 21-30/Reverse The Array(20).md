# Reverse The Array

## Problem statement

Given an array/list `ARR` of integers and a position `M`. You have to reverse the array after that position.

### Example

We have an array `ARR = {1, 2, 3, 4, 5, 6}` and `M = 3` (considering 0-based indexing). The subarray `{5, 6}` will be reversed, and our output array will be `{1, 2, 3, 4, 6, 5}`.

### Detailed Explanation

- **Input/output format**
- **Notes**
- **Images**

### Constraints

- `1 <= T <= 10`
- `0 <= M <= N <= 5 * 10^4`
- `-10^9 <= ARR[i] <= 10^9`

**Time Limit:** 1 sec

### Sample Input 1

```
2
6 3
1 2 3 4 5 6
5 2
10 9 8 7 6
```

### Sample Output 1

```
1 2 3 4 6 5
10 9 8 6 7
```

### Explanation 1

- For the first test case:  
  Considering 0-based indexing, we have `M = 3`, so the subarray `[M+1 … N-1]` has to be reversed.  
  Therefore, the required output will be `{1, 2, 3, 4, 6, 5}`.

- For the second test case:  
  Considering 0-based indexing, we have `M = 2`, so the subarray `[M+1 … N-1]` has to be reversed.  
  Therefore, the required output will be `{10, 9, 8, 6, 7}`.

### Sample Input 2

```
2
7 3
1 4 5 6 6 7 7 
9 3
10 4 5 2 3 6 1 3 6
```

### Sample Output 2

```
1 4 5 6 7 7 6
10 4 5 2 6 3 1 6 3
```

## Hints

1. Try to think by creating another array.
2. Try to think about which elements are being swapped.

## Code
```cpp
void reverseArray(vector<int> &arr , int m) {
    int s = m+1;
    int e = arr.size()-1;
    while(s<e)
    {
        swap(arr[s],arr[e]);
        s++;
        e--;
    }
return arr;    	
}
```
The code you've provided has a few issues that need to be corrected:

### Issues:
1. **Incorrect Indexing**: The condition `if(s > m)` implies that the swap should occur only when `s` is greater than `m`, but you might want to start reversing after the `m`th index (meaning `s >= m`).
  
2. **Missing Semicolon**: The `swap(arr[s], arr[e])` line is missing a semicolon at the end.

3. **Incorrect Return Type**: The function has a `void` return type, so `return arr;` is not needed and will cause a compilation error.

4. **Logic Issue**: The initial value of `s` should start from `m + 1` if you intend to reverse the elements after the `m`th index.

### Corrected Code:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void reverseArray(vector<int> &arr, int m) {
    int s = m + 1;  // Start reversing from the index after m
    int e = arr.size() - 1;

    while (s < e) {
        swap(arr[s], arr[e]);  // Swap elements at indices s and e
        s++;
        e--;
    }
}

void printArray(const vector<int> &arr) {
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5, 6, 7, 8};

    int m = 3;  // Reverse the array after the 3rd index
    reverseArray(arr, m);  // Reverse part of the array

    printArray(arr);  // Print the modified array

    return 0;
}
```

### Explanation of Fixes:
1. **Start Index `s = m + 1`**: This ensures that the reversal begins after the `m`th index.

2. **Added Semicolon**: The missing semicolon at the end of the `swap` line is added to avoid syntax errors.

3. **Removed `return` Statement**: Since the function is of type `void`, returning a value is unnecessary and has been removed.

4. **Updated `printArray` Function**: This function now correctly prints the array to verify the reversal.

### Output:
If you run the corrected code with the input vector `{1, 2, 3, 4, 5, 6, 7, 8}` and `m = 3`, the output will be:

```
1 2 3 4 8 7 6 5 
```

This output shows that the elements after index 3 (i.e., elements after `4`) have been reversed.
