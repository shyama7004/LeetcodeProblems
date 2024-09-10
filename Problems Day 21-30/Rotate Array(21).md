# 189. Rotate Array

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

In the given code, the line `temp[(i + k) % nums.size()] = nums[i];` is responsible for rotating the elements of the `nums` vector by `k` positions to the right. Here's a detailed explanation of this line:

1. **Index Calculation**: `(i + k) % nums.size()`
   - `i` is the current index of the element in the original `nums` vector.
   - `k` is the number of positions to rotate the vector to the right.
   - `nums.size()` gives the total number of elements in the `nums` vector.
   - Adding `i` and `k` gives the new index where the current element (`nums[i]`) should be placed in the `temp` vector.
   - The modulo operation `% nums.size()` ensures that the new index wraps around if it goes beyond the bounds of the vector size. This is crucial for handling cases where the new index would exceed the vector length, ensuring it "wraps around" to the beginning of the vector.

2. **Assignment**: `temp[(i + k) % nums.size()] = nums[i];`
   - This assigns the element `nums[i]` to the new index `(i + k) % nums.size()` in the `temp` vector.
   - By doing this for every element in the original `nums` vector, the `temp` vector ends up being a rotated version of `nums`.

### Example

Consider the vector `nums = [1, 2, 3, 4, 5]` and `k = 2`.

1. For `i = 0`, `(i + k) % nums.size()` is `(0 + 2) % 5` which is `2`. So, `temp[2] = nums[0]` -> `temp[2] = 1`.
2. For `i = 1`, `(i + k) % nums.size()` is `(1 + 2) % 5` which is `3`. So, `temp[3] = nums[1]` -> `temp[3] = 2`.
3. For `i = 2`, `(i + k) % nums.size()` is `(2 + 2) % 5` which is `4`. So, `temp[4] = nums[2]` -> `temp[4] = 3`.
4. For `i = 3`, `(i + k) % nums.size()` is `(3 + 2) % 5` which is `0`. So, `temp[0] = nums[3]` -> `temp[0] = 4`.
5. For `i = 4`, `(i + k) % nums.size()` is `(4 + 2) % 5` which is `1`. So, `temp[1] = nums[4]` -> `temp[1] = 5`.

After this process, `temp` will be `[4, 5, 1, 2, 3]`, which is the original `nums` vector rotated to the right by 2 positions.

Finally, the line `nums = temp;` assigns the rotated vector back to `nums`, completing the rotation operation.

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

`Note` : In-place means that you should update the original string rather than creating a new one.

Depending on the language/framework that you're using this could be impossible. (For example, strings are immutable in .NET and Java, so it would be impossible to perform an in-place update of a string without resorting to some evil hacks.)



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

The provided code rotates a vector `nums` to the right by `k` positions. The rotation is performed in three steps using the `reverse` function from the C++ Standard Library. Here's an explanation of each part:

1. **Handling Large `k` Values**:
   ```cpp
   k = k % nums.size();
   ```
   - This line ensures that `k` is within the bounds of the vector's length. 
   - If `k` is larger than the size of `nums`, rotating the array by `k` positions has the same effect as rotating it by `k % nums.size()` positions.
   - For example, rotating an array of size 5 by 7 positions is equivalent to rotating it by 2 positions (since `7 % 5 == 2`).

2. **Reverse the First Part of the Array**:
   ```cpp
   reverse(nums.begin(), nums.begin() + (nums.size() - k));
   ```
   - This line reverses the first part of the array, up to the point where the rotation will split it.
   - `nums.begin() + (nums.size() - k)` gives an iterator to the point where the rotation split occurs.
   - Reversing this part of the array prepares it for the final rotation.

3. **Reverse the Second Part of the Array**:
   ```cpp
   reverse(nums.begin() + (nums.size() - k), nums.end());
   ```
   - This line reverses the second part of the array, starting from the split point to the end.
   - This prepares the second part of the array for the final rotation.

4. **Reverse the Entire Array**:
   ```cpp
   reverse(nums.begin(), nums.end());
   ```
   - Finally, this line reverses the entire array.
   - By reversing the entire array after reversing the two parts separately, the elements are effectively rotated to the right by `k` positions.

### Example Walkthrough

Consider the vector `nums = [1, 2, 3, 4, 5]` and `k = 2`.

1. **Handle Large `k` Values**:
   - `k = k % nums.size()`, which results in `k = 2 % 5 = 2`.

2. **Reverse the First Part**:
   - Before reversal: `[1, 2, 3]`
   - After reversal: `[3, 2, 1]`
   - Array state: `[3, 2, 1, 4, 5]`

3. **Reverse the Second Part**:
   - Before reversal: `[4, 5]`
   - After reversal: `[5, 4]`
   - Array state: `[3, 2, 1, 5, 4]`

4. **Reverse the Entire Array**:
   - Before reversal: `[3, 2, 1, 5, 4]`
   - After reversal: `[4, 5, 1, 2, 3]`
   - Final array state: `[4, 5, 1, 2, 3]`

This final array is the original array rotated to the right by 2 positions.

In summary, these steps reverse the necessary parts of the array to achieve the rotation in an efficient manner, avoiding the need for additional space beyond a few temporary variables for the iterators.

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
