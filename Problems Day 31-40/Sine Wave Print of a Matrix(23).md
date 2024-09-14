# Sine Wave Print of a Matrix

## Problem Statement

For a given two-dimensional integer array/list `ARR` of size (N x M), print the `ARR` in a sine wave order, i.e., print the first column top to bottom, next column bottom to top, and so on.

### Example:

The sine wave order for the matrix:

```
1 2
3 4
```

will be: 
```
[1, 3, 4, 2]
```

---

## Input/Output Format

- **Input:**
  - The first line contains an integer `T`, the number of test cases.
  - For each test case:
    - The first line contains two integers, `N` and `M` (dimensions of the matrix).
    - The next `N` lines contain `M` integers representing the matrix `ARR`.

- **Output:**
  - For each test case, print the matrix in sine wave order.

---

## Constraints:

- `1 <= T <= 10`
- `1 <= N <= 100`
- `1 <= M <= 100`
- `0 <= ARR[i][j] <= 100`

### Time Limit:
- `1 sec`

---

## Sample Input 1:

```
2
3 4
1 2 3 4
5 6 7 8
9 10 11 12
4 4
1 2 4 5
3 6 8 10
11 12 13 15
16 14 9 7
```

### Sample Output 1:

```
1 5 9 10 6 2 3 7 11 12 8 4
1 3 11 16 14 12 6 2 4 8 13 9 7 15 10 5
```

### Explanation For Sample Input 1:

Here, the elements are printed in a wave pattern:
- First, the 0th column is printed from top to bottom.
- Then, the 1st column is printed from bottom to top, and so on.

Basically, the even columns are printed from top to bottom, and the odd columns are printed in the opposite direction.

---

## Sample Input 2:

```
2
1 1
3
1 2
6 5
```

### Sample Output 2:

```
3
6 5
```

## Question Explanation and Logic

<div align ="center"><img src ="https://github.com/shyama7004/LeetcodeProblems/blob/main/Problems%20Day%2031-40/Images/123.png"></div>



```py

#include <bits/stdc++.h> 
vector<int> wavePrint(vector<vector<int>> arr, int nRows, int mCols)
{
    //Write your code here
    vector<int> ans;
    for (int j=0; j<mCols; j++) {
        if (j%2==0) {
            for (int i=0; i<nRows; i++) {
                ans.push_back(arr[i][j]);
            }   
        }
        else {
            for (int i=nRows-1; i>=0; i--) {
                ans.push_back(arr[i][j]);
            } 
        }
    }
    return ans;
}
```
This code implements a wave-like traversal of a 2D matrix and returns the elements in a specific order. Here's the explanation of the logic, intuition, and approach:

### Intuition
The aim is to traverse the matrix in a wave-like pattern, column by column. For even-indexed columns, the traversal is top to bottom, while for odd-indexed columns, the traversal is bottom to top. This pattern resembles waves and ensures all elements are visited.

### Approach
1. **Initialize Result Vector**: Create an empty vector `ans` to store the traversal result.
2. **Iterate Over Columns**: Use a loop to iterate over each column (denoted by `j`).
3. **Column Check**:
    - For even-indexed columns (`j % 2 == 0`), traverse from the top to the bottom of the current column, adding elements to `ans`.
    - For odd-indexed columns, traverse from the bottom to the top of the current column, adding elements to `ans`.
4. **Return Result**: After iterating through all columns, return the `ans` vector containing the wave traversal of the matrix.

### Code Walkthrough
- **Initialization**: `vector<int> ans;` creates an empty vector to store the wave traversal result.
- **Outer Loop**: `for (int j=0; j<mCols; j++)` iterates through each column.
    - **Even Column Check**: `if (j % 2 == 0)` checks if the column index is even.
        - **Top to Bottom Traversal**: `for (int i=0; i<nRows; i++)` iterates through each row from top to bottom, adding elements to `ans`.
    - **Odd Column Check**: `else` handles the odd-indexed columns.
        - **Bottom to Top Traversal**: `for (int i=nRows-1; i>=0; i--)` iterates through each row from bottom to top, adding elements to `ans`.
- **Return Statement**: `return ans;` returns the result vector containing the wave traversal.

This approach ensures all elements in the matrix are traversed in the desired wave pattern.
