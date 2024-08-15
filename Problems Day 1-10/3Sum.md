# 3Sum

## Problem Statement

You are given an array/list `ARR` consisting of `N` integers. Your task is to find all the distinct triplets present in the array that add up to a given number `K`.

An array is said to have a triplet `{ARR[i], ARR[j], ARR[k]}` with sum = `K` if there exist three indices `i`, `j`, and `k` such that `i != j`, `j != k`, `i != k`, and `ARR[i] + ARR[j] + ARR[k] = K`.

### Notes:
1. You can return the list of values in any order. For example, if a valid triplet is `{1, 2, -3}`, then `{2, -3, 1}`, `{-3, 2, 1}`, etc., are also valid triplets. Also, the ordering of different triplets can be random, i.e., if there are more than one valid triplets, you can return them in any order.
2. The elements in the array need not be distinct.
3. If no such triplet is present in the array, then return an empty list, and the output printed for such a test case will be `-1`.

## Constraints:
- `1 <= T <= 50`
- `1 <= N <= 10^3`
- `-10^6 <= ARR[i] <= 10^6`
- `-10^9 <= K <= 10^9`

**Time Limit:** 1 sec

## Sample Input 1:
```
1
5
10 5 5 5 2
12
```

## Sample Output 1:
```
5 5 2
```

### Explanation for Sample Input 1:
- `5 5 2` is the only triplet that adds up to `12`. Note that the order of the output doesn’t matter, so `5 2 5` or `2 5 5` is also an acceptable answer.

## Sample Input 2:
```
3
6
1 2 3 1 2 3
6
4
1 2 3 4 
11
6
1 1 2 2 1 1
4
```

## Sample Output 2:
```
1 2 3
-1
1 1 2
```

### Explanation for Sample Input 2:
- In the first input, `(1, 2, 3)` is the only unique triplet that adds up to six.
- In the second input, since there are no such triplets, we print `-1`.
- For the third input, the only distinct triplet is `(1, 1, 2)`, so just print `1 1 2`.

## Solution 

### Problem Overview

The task is to find all distinct triplets in an array that sum up to a given number \( K \). We can solve this problem using a brute-force approach with three nested loops, which will allow us to consider all possible triplets in the array.

### Approach and Intuition

1. **Triple Nested Loops**:
   - The outermost loop will pick the first element of the triplet.
   - The middle loop will pick the second element.
   - The innermost loop will pick the third element.
   - For each combination of three elements, we check if their sum equals \( K \).
   - If the sum matches \( K \), we store the triplet in a result list.

2. **Avoid Duplicates**:
   - To ensure that we only store distinct triplets, we can use a set to keep track of the triplets we have already seen.

3. **Sort the Triplets**:
   - Although the order of elements in each triplet doesn’t matter, to avoid storing duplicates in different orders (like {2, 5, 5} and {5, 2, 5}), we can sort the triplet before adding it to the set.

### Time and Space Complexity

- **Time Complexity**: \( O(n^3) \) due to the three nested loops, where \( n \) is the size of the array.
- **Space Complexity**: \( O(k) \), where \( k \) is the number of distinct triplets found.

### Implementation in C++

Here's the solution using three loops:

```cpp
#include <iostream>
#include <vector>
#include <set>
#include <algorithm>

using namespace std;

vector<vector<int>> threeSum(vector<int> &arr, int K) {
    int n = arr.size();
    set<vector<int>> uniqueTriplets;

    // Triple nested loop to check all triplets
    for (int i = 0; i < n - 2; i++) {
        for (int j = i + 1; j < n - 1; j++) {
            for (int k = j + 1; k < n; k++) {
                if (arr[i] + arr[j] + arr[k] == K) {
                    vector<int> triplet = {arr[i], arr[j], arr[k]};
                    sort(triplet.begin(), triplet.end()); // Sort to avoid duplicates
                    uniqueTriplets.insert(triplet); // Insert into set to ensure uniqueness
                }
            }
        }
    }

    // Convert set to vector of vectors
    vector<vector<int>> result(uniqueTriplets.begin(), uniqueTriplets.end());
    return result;
}

int main() {
    int T;
    cin >> T;
    while (T--) {
        int N, K;
        cin >> N;
        vector<int> arr(N);
        for (int i = 0; i < N; i++) {
            cin >> arr[i];
        }
        cin >> K;

        vector<vector<int>> triplets = threeSum(arr, K);

        if (triplets.empty()) {
            cout << "-1" << endl;
        } else {
            for (const auto &triplet : triplets) {
                for (int num : triplet) {
                    cout << num << " ";
                }
                cout << endl;
            }
        }
    }
    return 0;
}
```

### Explanation:

1. **Triple Loop**:
   - The loops iterate through every possible combination of three different indices `i`, `j`, and `k` such that `i < j < k`.
   - The sum of `arr[i] + arr[j] + arr[k]` is checked against \( K \).

2. **Unique Triplets Using Set**:
   - A set is used to automatically handle duplicate triplets. By inserting a sorted triplet into the set, we ensure that the order of elements doesn't affect uniqueness.

3. **Returning Results**:
   - If no triplet is found, the function returns `-1`.
   - Otherwise, the unique triplets are printed.

### Example Execution:

For the input:
```
1
5
10 5 5 5 2
12
```

The output would be:
```
5 5 2
```

This approach guarantees that all possible triplets are checked, and duplicates are avoided, which ensures correctness. However, it is not optimized for large inputs, as the time complexity is \( O(n^3) \).
```
