# 189. Rotate Array

## Topics

- Arrays
- Algorithms

## Problem Statement

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

## Examples

### Example 1

**Input:** `nums = [1,2,3,4,5,6,7]`, `k = 3`

**Output:** `[5,6,7,1,2,3,4]`

**Explanation:**
- Rotate 1 step to the right: `[7,1,2,3,4,5,6]`
- Rotate 2 steps to the right: `[6,7,1,2,3,4,5]`
- Rotate 3 steps to the right: `[5,6,7,1,2,3,4]`

### Example 2

**Input:** `nums = [-1,-100,3,99]`, `k = 2`

**Output:** `[3,99,-1,-100]`

**Explanation:**
- Rotate 1 step to the right: `[99,-1,-100,3]`
- Rotate 2 steps to the right: `[3,99,-1,-100]`

## Constraints

- `1 <= nums.length <= 10^5`
- `-2^31 <= nums[i] <= 2^31 - 1`
- `0 <= k <= 10^5`

# Code
Let's analyze the two different implementations provided for rotating an array `nums` by `k` steps. We'll go through the logic, intuition, and explanation for both approaches.

### Approach 1: Using an Auxiliary Array

#### Code
```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        vector<int> temp(nums.size());
        for(int i = 0; i < nums.size(); i++) {
            temp[(i + k) % nums.size()] = nums[i];
        }
        nums = temp;
    }
};
```

#### Logic and Intuition

1. **Create a temporary array:** A new array `temp` of the same size as `nums` is created to store the rotated elements.
2. **Map each element to its new position:**
    - For each element in the original array `nums`, calculate its new position after rotation.
    - The new position of an element at index `i` is `(i + k) % nums.size()`.
    - This formula ensures that the new position wraps around to the beginning of the array if it exceeds the array length.
3. **Copy the temporary array back to the original array:** After all elements are placed in their new positions in `temp`, copy the contents of `temp` back to `nums`.

#### Explanation

- **Time Complexity:** \( O(N) \) because we iterate through the array once to fill `temp` and then copy `temp` to `nums`.
- **Space Complexity:** \( O(N) \) because we use an additional array `temp` of the same size as `nums`.

This approach is straightforward and easy to understand, but it uses extra space proportional to the size of the input array.

<details>
<summary>VS-Code</summary>

  ```cpp
#include<iostream>
#include<vector>
#include<cmath>
#include<algorithm>



using namespace std;

void rotate(vector<int>& arr, int key)
{
    vector<int> v(arr.size());

    for(int i = 0;i<arr.size();i++)
    {
        v[(i + key)%arr.size()] = arr[i];
    }

    arr = v;
}

int main()
{
    vector<int> nums = {1,2,3,4,5,6,7};
    int k = 3;
   rotate(nums,k);
    for(int i = 0;i < nums.size();i++)
    {
        cout<<nums[i]<<" ";
    }
    cout<<endl;
    return 0;
}
  ```

</details>

### Approach 2: In-Place Rotation Using Reversal

#### Code
```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        k = k % nums.size();  // Handle cases where k is larger than the array size
        reverse(nums.begin(), nums.begin() + (nums.size() - k));
        reverse(nums.begin() + (nums.size() - k), nums.end());
        reverse(nums.begin(), nums.end());
    }
};
```

#### Logic and Intuition

1. **Handle `k` greater than the array size:** Calculate `k % nums.size()` to handle cases where `k` is greater than the size of the array. Rotating an array by its length results in the same array, so we only need to rotate by the remainder.
2. **Reverse the first part of the array:** Reverse the first `n-k` elements. This changes the order of the first part of the array.
    - Example: For `nums = [1, 2, 3, 4, 5, 6, 7]` and `k = 3`, `n-k` is 4. Reverse `[1, 2, 3, 4]` to get `[4, 3, 2, 1]`.
3. **Reverse the second part of the array:** Reverse the last `k` elements. This changes the order of the second part of the array.
    - Reverse `[5, 6, 7]` to get `[7, 6, 5]`.
4. **Reverse the entire array:** Reverse the whole array to get the final rotated result.
    - Reverse `[4, 3, 2, 1, 7, 6, 5]` to get `[5, 6, 7, 1, 2, 3, 4]`.

#### Explanation

- **Time Complexity:** \( O(N) \) because we reverse the array three times, and each reversal operation is \( O(N) \).
- **Space Complexity:** \( O(1) \) because we perform the rotations in-place without using extra space.

This approach is more space-efficient compared to the first one because it rotates the array in-place using the reversal technique.

<details>
<summary>Vs-Code</summary>

```cpp
  #include<iostream>
#include<vector>
#include<cmath>
#include<algorithm>



using namespace std;

void rotate(vector<int>& arr, int k)
{
    k = k % arr.size();
    reverse(arr.begin(),arr.begin() + (arr.size() - k));
    reverse(arr.begin() + (arr.size() - k),arr.end());
    reverse(arr.begin(), arr.end());
}

int main()
{
    vector<int> nums = {1,2,3,4,5,6,7};
    int k = 3;
   rotate(nums,k);
    for(int i = 0;i < nums.size();i++)
    {
        cout<<nums[i]<<" ";
    }
    cout<<endl;
    return 0;
}
```
</details>

### Summary

- **Approach 1 (Auxiliary Array):**
    - **Logic:** Create a temporary array to store the rotated elements and then copy it back to the original array.
    - **Time Complexity:** \( O(N) \)
    - **Space Complexity:** \( O(N) \)
    - **Use Case:** Simple to understand and implement but uses extra space.

- **Approach 2 (In-Place Rotation Using Reversal):**
    - **Logic:** Rotate the array in three steps using the reversal technique.
    - **Time Complexity:** \( O(N) \)
    - **Space Complexity:** \( O(1) \)
    - **Use Case:** More space-efficient and suitable for in-place rotation without extra memory allocation.

Both methods are effective, but the choice between them depends on whether you prioritize simplicity (Approach 1) or space efficiency (Approach 2).

## Follow Up

Try to come up with as many solutions as you can. There are at least three different ways to solve this problem.

Could you do it in-place with `O(1)` extra space?
