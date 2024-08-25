# Aggressive Cows

## Problem Statement
You are given an array `arr` consisting of `n` integers, which denote the position of stalls.

You are also given an integer `k`, which denotes the number of aggressive cows.

Your task is to assign stalls to `k` cows such that the minimum distance between any two of them is the maximum possible.

Print the maximum possible minimum distance.

### Example
**Input:**  
`n` = 3, `k` = 2, `arr` = {1, 2, 3}

**Output:**  
2

**Explanation:**  
The maximum possible minimum distance will be 2 when 2 cows are placed at positions {1, 3}. The distance between cows is 2.

## Detailed Explanation (Input/Output Format, Notes, Images)

### Sample Input 1:
```
6 4
0 3 4 7 10 9
```

### Sample Output 1:
```
3
```

**Explanation:**  
The maximum possible minimum distance between any two cows will be 3 when 4 cows are placed at positions {0, 3, 7, 10}. The distances between cows are 3, 4, and 3 respectively.

### Sample Input 2:
```
5 2
4 2 1 3 6
```

### Sample Output 2:
```
5
```

## Expected Time Complexity:
- Can you solve this in `O(n * log(n))` time complexity?

## Constraints:
- `2 <= n <= 10^5`
- `2 <= k <= n`
- `0 <= arr[i] <= 10^9`

**Time Limit:** 1 second


## Logic

<div align="center"><img src="https://github.com/shyama7004/LeetcodeProblems/blob/main/Day%2011-20/Images/6.jpg" width="400"></div>

- **Cow Placement**:
  - Cow 1 = C1 & Cow 2 = C2
  - We place each cow in different positions and calculate the absolute difference between their positions. The goal is to maximize this minimum difference.

- **Why Binary Search?**:
  - First, attempt a solution. If it’s invalid (i.e., the cows cannot be placed with the current minimum distance), this invalid solution helps us eliminate a portion of the search space.
  - This process of narrowing down the search space indicates that binary search is applicable.

- **Applying Binary Search**:
  - **Search Space**:
    - `min = 0` (minimum possible distance between cows)
    - `max = sum of elements` (though in this context, `max` should actually be the distance between the furthest stalls)
  - Calculate `mid = (start + end) / 2` and check if it's a valid solution.

- **Iterate**:
  - Adjust the search space based on whether the current `mid` is a valid distance for placing all cows. Continue this process until the maximum possible minimum distance is found.

## Code
```cpp
#include<algorithm>

bool isPossibleSolution(vector<int> &stalls, int k, int mid) {
    int cowCount = 1;
    int lastPos = stalls[0];

    for (int i=0; i<stalls.size(); i++) {
		if (stalls[i]-lastPos >= mid) {
            cowCount++;
            if (cowCount == k) {
                return true;
            }
            lastPos = stalls[i];
		}
	}
	return false;
}

int aggressiveCows(vector<int> &stalls, int k)
{
    //    Write your code here.
    sort(stalls.begin(), stalls.end());
    int s = 0;
    int e = *max_element(stalls.begin(), stalls.end());
    int ans = -1;
    int mid = s + (e-s)/2;

    while (s<=e) {
        if (isPossibleSolution(stalls, k, mid)) {
            ans = mid;
            s = mid + 1;
        }
        else {
            e = mid - 1;
        }

        mid = s + (e-s)/2;
    }
    return ans;
}
```
## Explanation

### Code Overview
This code solves the "Aggressive Cows" problem using a binary search approach to find the maximum possible minimum distance between any two cows.

### Step-by-Step Explanation

1. **isPossibleSolution Function**:
   - **Purpose**: This function checks whether it is possible to place all `k` cows in the stalls such that the minimum distance between any two cows is at least `mid`.
   - **Logic**:
     - Start by placing the first cow in the first stall (`lastPos = stalls[0]`).
     - Iterate through the stalls to place the remaining cows. 
     - If the difference between the current stall and the `lastPos` is greater than or equal to `mid`, place a cow there and update `lastPos`.
     - If you can place all `k` cows this way, return `true`. Otherwise, return `false`.

2. **aggressiveCows Function**:
   - **Purpose**: This function uses binary search to find the maximum possible minimum distance between the cows.
   - **Logic**:
     - **Sorting the Stalls**: First, sort the `stalls` array to make it easier to calculate distances between them.
     - **Define Search Space**:
       - Start with `s = 0` (the smallest possible minimum distance).
       - Set `e = max(stalls) - min(stalls)` (the largest possible distance between any two stalls).
       - Initialize `ans = -1` to store the best solution found.
     - **Binary Search**:
       - Calculate `mid = s + (e - s) / 2`.
       - Use the `isPossibleSolution` function to check if it's possible to place all cows with at least `mid` distance.
       - If it's possible (`isPossibleSolution` returns `true`), update `ans` to `mid` and try for a larger distance by setting `s = mid + 1`.
       - If it's not possible, reduce the search space by setting `e = mid - 1`.
       - Repeat until `s > e`.
     - **Return the Answer**: The value stored in `ans` is the maximum possible minimum distance between the cows.

### Key Points
- **Sorting**: Sorting the stalls allows for an easier and efficient calculation of distances between them.
- **Binary Search**: The binary search effectively reduces the range of possible answers by testing the middle value (`mid`) and adjusting the search space based on the feasibility of that value.
- **Efficiency**: The approach ensures that the solution is found in `O(n * log(n))` time, where `n` is the number of stalls. This is efficient enough given the constraints.

### Example Walkthrough
For a quick example, if you have stalls at positions `[1, 2, 4, 8, 9]` and `k = 3` cows:
- **Initial Conditions**: The stalls are sorted as `[1, 2, 4, 8, 9]`.
- **Search Space**: Start with `s = 0` and `e = 8` (distance between `1` and `9`).
- **Binary Search**:
  - First `mid = 4`. Check if it's possible to place cows with at least `4` distance.
    - Possible positions: `1, 8, (no space for third cow)`. Not feasible, reduce `e`.
  - Next `mid = 2`. Check feasibility.
    - Possible positions: `1, 4, 8`. Feasible, try larger distance (`s = mid + 1`).
  - Continue until the optimal distance is found.

