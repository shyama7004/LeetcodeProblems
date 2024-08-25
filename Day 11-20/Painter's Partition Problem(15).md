# Painter's Partition Problem

## Problem Statement

Given an array/list of length `n`, where the array/list represents the boards, and each element of the given array/list represents the length of each board. Some `k` numbers of painters are available to paint these boards. Consider that each unit of a board takes 1 unit of time to paint.

You are supposed to return the area of the minimum time to get this job done of painting all the `n` boards under a constraint that any painter will only paint the continuous sections of boards.

### Example

**Input:** `arr = [2, 1, 5, 6, 2, 3]`, `k = 2`

**Output:** `11`

**Explanation:**
- The first painter can paint boards 1 to 3 in 8 units of time, and the second painter can paint boards 4-6 in 11 units of time. 
- Thus, both painters will paint all the boards in `max(8, 11) = 11` units of time. 
- It can be shown that all the boards can't be painted in less than 11 units of time.

### Detailed Explanation (Input/Output Format, Notes, Images)

**Sample Input 1:**
```
4 2
10 20 30 40
```

**Sample Output 1:**
```
60
```

**Explanation for Sample Input 1:**
- In this test case, we can divide the first 3 boards for one painter and the last board for the second painter.

**Sample Input 2:**
```
2 2
48 90
```

**Sample Output 2:**
```
90
```

### Expected Time Complexity

Try to do this in `O(n*log(n))`.

### Constraints

- `1 <= n <= 10^5`
- `1 <= k <= n`
- `1 <= arr[i] <= 10^9`

**Time Limit:** 1 sec.

## Logic

- **Similar to Book Allocation Problem**: Both problems require distributing tasks to minimize the maximum workload.
- Click here to see the [Book Allocation Problem](https://github.com/shyama7004/LeetcodeProblems/blob/main/Day%2011-20/Book%20Allocation(15).md)
  
- **Why the Same Logic Applies**:
  - The problem involves minimizing or maximizing workloads, indicating that a **binary search on the answer** is suitable.

- **Key Steps**:
  - **Define Search Space**:
    - **Lower Bound (`start`)**: Maximum board length (no painter can paint less than this).
    - **Upper Bound (`end`)**: Sum of all board lengths (one painter paints all boards).
  - **Binary Search**:
    - Search for the smallest feasible maximum workload (`mid`) using binary search.
  - **Feasibility Check**:
    - Implement a function (`isPossible`) to verify if painting all boards is possible with the current `mid` and given number of painters.

- **Conclusion**: This method efficiently finds the minimum possible maximum workload using binary search.

## Code

```cpp
bool isPossible(vector<int>& boards, int k, int mid) {
    int painterCount = 1;
    int boardSum = 0;

    for (int i = 0; i < boards.size(); i++) {
        if (boardSum + boards[i] <= mid) {
            boardSum += boards[i];
        } else {
            painterCount++;
            if (painterCount > k || boards[i] > mid) {
                return false;
            }
            boardSum = boards[i];
        }
    }
    return true; 
}

int findLargestMinDistance(vector<int>& boards, int k) {
    int start = *max_element(boards.begin(), boards.end());  // Start with the largest board
    int sum = accumulate(boards.begin(), boards.end(), 0);  // Sum of all boards
    int end = sum;
    int mid, ans = -1;

    while (start <= end) {
        mid = start + (end - start) / 2;

        if (isPossible(boards, k, mid)) {  // Check if it's possible with mid as the maximum distance
            ans = mid;
            end = mid - 1; 
        } else {
            start = mid + 1;
        }
    } 
    return ans;
}

```
