
## Problem Statement

Given an array `arr` of integers, where `arr[i]` represents the number of pages in the i-th book. There are `m` number of students, and the task is to allocate all the books to the students. The allocation should satisfy the following conditions:

1. Each student gets at least one book.
2. Each book should be allocated to a student.
3. The allocation of books to each student should be in a contiguous manner.

Your goal is to allocate the books to `m` students such that the maximum number of pages assigned to a student is minimized.

### Example

Let's consider `n = 4` (number of books) and `m = 2` (number of students).

`arr = [10, 20, 30, 40]`.

<div align="center"><img src ="https://github.com/shyama7004/LeetcodeProblems/blob/main/Day%2011-20/Images/1.jpeg" width ="300"></div>


All possible ways to allocate the 4 books to 2 students are:

1. **Allocation:** `[10] | [20, 30, 40]`  
   **Sum of pages:**  
   - Student 1: 10 pages  
   - Student 2: 20 + 30 + 40 = 90 pages  
   **Maximum pages assigned:** `max(10, 90) = 90`

2. **Allocation:** `[10, 20] | [30, 40]`  
   **Sum of pages:**  
   - Student 1: 10 + 20 = 30 pages  
   - Student 2: 30 + 40 = 70 pages  
   **Maximum pages assigned:** `max(30, 70) = 70`

3. **Allocation:** `[10, 20, 30] | [40]`  
   **Sum of pages:**  
   - Student 1: 10 + 20 + 30 = 60 pages  
   - Student 2: 40 pages  
   **Maximum pages assigned:** `max(60, 40) = 60`

Among these, the minimum possible maximum number of pages assigned to a student is `min(90, 70, 60) = 60`.

### Note:
1. Do not print anything; just return the maximum number of pages assigned to a student is minimized.
2. If it is not possible to assign the `n` books to `m` students, then return `-1`.

### Input Format:

- The first line of input contains an integer `T` denoting the number of test cases.
- For each test case:
  - The first line contains two space-separated integers `n` and `m`—`n` represents the number of books, and `m` represents the number of students.
  - The second line contains `n` space-separated integers representing the array `arr`, where `arr[i]` denotes the number of pages in the i-th book.

### Output Format:

For each test case, return the minimum number of pages.

### Constraints:


- 1 ≤ T ≤ 50
- 2 ≤ M ≤ N ≤ 1000
- 1 ≤ arr[i] ≤ 10<sup>9</sup>
- The sum of all `arr[i]` does not exceed 10<sup>9</sup>.
- Time limit: 1 second

This format avoids using LaTeX and uses simple HTML tags like `<sup>` for superscripts, which are supported in GitHub Markdown.

### Sample Cases:

**Sample Case 1:**

- **Input:**
  ```
  1
  4 2
  10 20 30 40
  ```
- **Output:** `60`

- **Explanation:** As shown in the example above, the optimal way to allocate the books is such that the maximum number of pages assigned to any student is 60.

**Sample Case 2:**

- **Input:**
  ```
  1
  5 3
  12 34 67 90 56
  ```
- **Output:** `113`

- **Explanation:** The books can be allocated as `[12, 34] | [67] | [90, 56]`, minimizing the maximum pages to 113.

**Sample Case 3:**

- **Input:**
  ```
  1
  3 2
  15 17 20
  ```
- **Output:** `32`

- **Explanation:** The books can be allocated as `[15] | [17, 20]` with the minimum maximum pages being 32.


## Logic

<div align="center"><img src="https://github.com/shyama7004/LeetcodeProblems/blob/main/Day%2011-20/Images/2.jpg" width="300"></div>

### Approach

To solve the problem of distributing books among students such that the maximum number of pages assigned to any student is minimized, let's break it down:

1. **Case Analysis**:
   - **Case 1**: Student 1 gets the first book (`10` pages), and Student 2 gets the remaining books (`20, 30, 40` pages). The maximum pages assigned to a student in this case is `90`.
   - **Case 2**: Student 1 gets the first two books (`10, 20` pages), and Student 2 gets the last two books (`30, 40` pages). The maximum pages assigned to a student in this case is `70`.
   - **Case 3**: Student 1 gets the first three books (`10, 20, 30` pages), and Student 2 gets the last book (`40` pages). The maximum pages assigned to a student in this case is `60`.

   The objective is to find the minimum of these maximum values, which in this scenario is `60`.

### Reducing the Search Space

<div align="center"><img src="https://github.com/shyama7004/LeetcodeProblems/blob/main/Day%2011-20/Images/3.jpg" width="300"></div>

To efficiently find this minimum, we use a binary search approach:

1. **Initial Setup**:
   - Set `min = 0` (the minimum possible number of pages).
   - Set `max = sum of all elements in the array` (the maximum possible number of pages if all books were assigned to one student).

2. **Binary Search**:
   - Calculate `mid = (min + max) / 2`.
   
   - **Case 1**: If `mid = 50`, then:
     - Assign books such that Student 1 gets books with `10, 20` pages, and Student 2 gets books with `30` pages. However, Student 3 is required to get the last book with `40` pages, making the total number of students `3`.
     - Since the number of students exceeds `2`, this is an invalid case.
     - All values less than `50` will also be invalid, so update the search range by setting `min = mid + 1`.

   - **Case 2**: With the updated range, `mid = (51 + 100) / 2 = 75`:
     - Assign books such that Student 1 gets books with `10, 20, 30` pages, and Student 2 gets the last book with `40` pages.
     - This is a valid case, but we need to find the minimum `mid`, so update the search range by setting `max = mid - 1`.

   <div align="center"><img src="https://github.com/shyama7004/LeetcodeProblems/blob/main/Day%2011-20/Images/4.jpg" width="300"></div>

   - **Continue Searching**:
     - Recalculate `mid = (51 + 74) / 2 = 62`. This is also a valid case, so update the range.
     - Continue this process until the range converges to the minimum valid `mid`.

   - **Final Case**:
     - After several iterations, you'll find `mid = 60`, which is the minimum value where the number of students required is exactly `2`.

   <div align="center"><img src="https://github.com/shyama7004/LeetcodeProblems/blob/main/Day%2011-20/Images/5.jpg" width="300"></div>

   - If `mid = 60` results in a valid distribution, then it's the optimal solution. Any attempt to reduce `mid` further would result in invalid distributions (requiring more than `2` students).

### Code

```cpp
#include <vector>
using namespace std;

// Helper function to check if it is possible to allocate books such that the maximum pages
// assigned to any student is less than or equal to 'mid'.
bool isPossible(vector<int>& arr, int n, int m, int mid) {
    int studentCount = 1; // Start with one student
    int pageSum = 0; // To keep track of pages assigned to the current student

    for (int i = 0; i < n; i++) {
        // If adding the current book's pages to the current student's sum doesn't exceed 'mid'
        if (pageSum + arr[i] <= mid) {
            pageSum += arr[i];
        } else {
            // If it exceeds, allocate books to the next student
            studentCount++;
            // Check if the number of students exceeds the allowed number 'm'
            // or if a single book has more pages than 'mid', making it impossible to allocate
            if (studentCount > m || arr[i] > mid) {
                return false;
            }
            // Assign current book's pages to the new student
            pageSum = arr[i];
        }
    }
    return true;
}

// Main function to allocate books such that the maximum number of pages assigned to any student is minimized
int allocateBooks(vector<int>& arr, int n, int m) {
    // 's' is the minimum number of pages possible, initially 0
    int s = 0;
    // 'sum' is the total number of pages in all books, which is the maximum number of pages possible
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }
    int e = sum; // 'e' is the maximum number of pages possible
    int ans = -1; // Variable to store the final answer
    int mid = s + (e - s) / 2; // Calculate the middle point

    // Perform binary search
    while (s <= e) {
        if (isPossible(arr, n, m, mid)) {
            // If it is possible to allocate books with 'mid' as the maximum pages
            ans = mid;
            e = mid - 1; // Try to find a smaller maximum
        } else {
            s = mid + 1; // If not possible, increase the minimum limit
        }
        mid = s + (e - s) / 2; // Recalculate the middle point
    }

    return ans; // Return the minimum of the maximum pages found
}
```

### Explanation:

1. **Helper Function: `isPossible()`**
   - **Purpose**: This function checks whether it's possible to allocate the books to students such that no student gets more than `mid` pages.
   - **Logic**:
     - We start with one student and try to allocate books sequentially.
     - If adding a book's pages to the current student's total doesn’t exceed `mid`, we add it to their total.
     - If it exceeds, we allocate the current book to the next student and continue.
     - If at any point the number of students exceeds `m`, or a single book's pages exceed `mid`, it's impossible to allocate under the current `mid`, so the function returns `false`.

2. **Main Function: `allocateBooks()`**
   - **Purpose**: This function finds the optimal solution where the maximum pages assigned to any student is minimized.
   - **Logic**:
     - We initialize the search space with `s = 0` and `e = sum of all pages` (the smallest and largest possible values).
     - We calculate the mid-point (`mid`) of this range.
     - We then use binary search:
       - If it’s possible to allocate books with `mid` pages as the maximum (`isPossible()` returns `true`), we store `mid` as a potential answer and try to minimize further by decreasing the upper bound (`e = mid - 1`).
       - If it’s not possible, we increase the lower bound (`s = mid + 1`).
     - The process continues until the search space is exhausted, and `ans` will contain the minimum possible value of the maximum pages.

### How the Logic is Implemented:
- The logic behind minimizing the maximum number of pages is implemented using binary search. The binary search helps in reducing the number of possible solutions and efficiently finds the optimal one.
- The `isPossible` function ensures that for each candidate solution (`mid`), we verify whether it’s feasible to allocate the books under the given constraints.
- The `allocateBooks` function drives the search for the minimum possible maximum by adjusting the search space based on the feasibility check. 

This implementation is efficient and adheres to the constraints of the problem, ensuring that it works within the given limits.
