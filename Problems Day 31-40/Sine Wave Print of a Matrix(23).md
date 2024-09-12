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
