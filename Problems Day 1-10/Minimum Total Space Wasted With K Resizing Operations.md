# 1959. Minimum Total Space Wasted With K Resizing Operations

## Problem Statement

You are currently designing a dynamic array. You are given a 0-indexed integer array `nums`, where `nums[i]` is the number of elements that will be in the array at time `i`. In addition, you are given an integer `k`, the maximum number of times you can resize the array (to any size).

The size of the array at time `t`, `size_t`, must be at least `nums[t]` because there needs to be enough space in the array to hold all the elements. The space wasted at time `t` is defined as `size_t - nums[t]`, and the total space wasted is the sum of the space wasted across every time `t` where `0 <= t < nums.length`.

Return the minimum total space wasted if you can resize the array at most `k` times.

**Note:** The array can have any size at the start and does not count towards the number of resizing operations.

## Examples

### Example 1:
**Input:** `nums = [10,20], k = 0`  
**Output:** `10`  
**Explanation:** 
- `size = [20,20]`.
- We can set the initial size to be 20.
- The total wasted space is `(20 - 10) + (20 - 20) = 10`.

### Example 2:
**Input:** `nums = [10,20,30], k = 1`  
**Output:** `10`  
**Explanation:** 
- `size = [20,20,30]`.
- We can set the initial size to be 20 and resize to 30 at time 2.
- The total wasted space is `(20 - 10) + (20 - 20) + (30 - 30) = 10`.

### Example 3:
**Input:** `nums = [10,20,15,30,20], k = 2`  
**Output:** `15`  
**Explanation:** 
- `size = [10,20,20,30,30]`.
- We can set the initial size to 10, resize to 20 at time 1, and resize to 30 at time 3.
- The total wasted space is `(10 - 10) + (20 - 20) + (20 - 15) + (30 - 30) + (30 - 20) = 15`.

## Constraints:
- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 10^6`
- `0 <= k <= nums.length - 1`

## Your Code (approach this question after Dp)

### Problem Breakdown:

Given an array of integers `nums` representing the sizes of elements that need to be stored sequentially and an integer `k` representing the number of resizing operations allowed, the goal is to minimize the total space wasted. The space wasted is defined as the difference between the space allocated and the space actually used.

- When resizing, you can choose to resize the space to fit all elements up to a certain point.
- The goal is to minimize the total wasted space with at most `k` resizing operations.

### Dynamic Programming Approach:

#### Steps:
1. **Define DP State**:
   - Let `dp[i][j]` be the minimum total space wasted for the first `i` elements with `j` resizing operations.
   
2. **Base Case**:
   - `dp[0][j] = 0` for all `j`, because with 0 elements, no space is wasted.
   - `dp[i][0]` is the wasted space when there are no resizing operations allowed.

3. **Transition**:
   - For each element `i`, you can decide to resize at that point. You then compute the wasted space if you use `t` elements and the maximum element in that subarray.
   - The state transition can be represented as:
     \[
     dp[i][j] = \min(dp[i][j], dp[t][j-1] + \text{wasted space from } t+1 \text{ to } i)
     \]
   
4. **Final Answer**:
   - The answer will be `dp[n][k]`, where `n` is the length of the array.

### Implementation:

```cpp
#include <vector>
#include <algorithm>
#include <climits>
using namespace std;

class Solution {
public:
    int minSpaceWastedKResizing(vector<int>& nums, int k) {
        int n = nums.size();
        vector<vector<int>> dp(n + 1, vector<int>(k + 1, INT_MAX));

        // Base case: No elements, no space wasted
        dp[0][0] = 0;

        // Fill the DP table
        for (int i = 1; i <= n; ++i) {
            for (int j = 0; j <= k; ++j) {
                int max_elem = 0;
                int total_sum = 0;
                for (int t = i; t > 0; --t) {
                    max_elem = max(max_elem, nums[t-1]);
                    total_sum += nums[t-1];
                    if (dp[t-1][j] != INT_MAX) {
                        dp[i][j] = min(dp[i][j], dp[t-1][j] + max_elem * (i - t + 1) - total_sum);
                    }
                }
            }
        }

        return dp[n][k];
    }
};
```

### Explanation:

- **Outer Loops**:
  - The first loop iterates through the elements.
  - The second loop iterates through the allowed number of resizing operations.
  
- **Inner Loop**:
  - The innermost loop considers resizing at different positions `t`.
  - It keeps track of the maximum element (`max_elem`) and the total sum of elements from `t` to `i`.

- **Wasted Space**:
  - The space wasted for resizing from `t` to `i` is calculated as `(max_elem * (i - t + 1) - total_sum)`.

### Complexity:

- **Time Complexity**: \(O(n^2 \times k)\) because of the three nested loops.
- **Space Complexity**: \(O(n \times k)\) due to the DP table.

This solution efficiently computes the minimum total space wasted with at most `k` resizing operations using dynamic programming.
