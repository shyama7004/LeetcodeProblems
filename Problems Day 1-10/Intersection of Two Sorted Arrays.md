# Intersection of Two Sorted Arrays
(Important question as it gives an idea about two pointer which is frequently asked in interviews.)

## Problem Statement

You are given two arrays `A` and `B` of size `N` and `M` respectively. Both these arrays are sorted in non-decreasing order. You have to find the intersection of these two arrays.

Intersection of two arrays is an array that consists of all the common elements occurring in both arrays.

### Notes:
1. The length of each array is greater than zero.
2. Both arrays are sorted in non-decreasing order.
3. The output should be in the order of elements that occur in the original arrays.
4. If there is no intersection present, return an empty array.

## Constraints:
- `1 <= T <= 100`
- `1 <= N, M <= 10^4`
- `0 <= A[i] <= 10^5`
- `0 <= B[i] <= 10^5`

**Time Limit:** 1 sec

## Sample Input 1:
```
2
6 4
1 2 2 2 3 4
2 2 3 3
3 2
1 2 3
3 4  
```

## Sample Output 1:
```
2 2 3
3   
```

### Explanation for Sample Input 1:
- For the first test case, the common elements are `2 2 3` in both arrays, so we print them.
- For the second test case, only `3` is common, so we print `3`.

## Sample Input 2:
```
2
3 3 
1 4 5
3 4 5
1 1
3
6
```

## Sample Output 2:
```
4 5
-1
```
## My nala code

There are a couple of issues with the code you provided. Let's break them down:

### Code Analysis:

```cpp
#include <bits/stdc++.h> 
vector<int> findArrayIntersection(vector<int> &arr1, int n, vector<int> &arr2, int m)
{
    vector<int> ans;

    for(int i = 0; i < n; i++)
    {
        int element = arr1[i];

        for(int j = 0; j < m; j++)
        {
            if(element = arr2[j]) // Issue #1: Assignment instead of comparison
            {
                ans.push_back(element);
                arr2[j] = -2; // Issue #2: Incorrect assignment
                break;
            }
        }
    }

    return ans; // Issue #3: Missing return statement
}
```

### Key Issues:

1. **Assignment Instead of Comparison**:
   - **Problem**: The condition `if(element = arr2[j])` is an assignment, not a comparison. This means that `element` will be assigned the value of `arr2[j]`, and the condition will always be `true` unless `arr2[j]` is `0` (since `0` is considered `false` in a boolean context).
   - **Solution**: Replace `=` with `==` to perform a comparison:
     ```cpp
     if (element == arr2[j])
     ```

2. **Incorrect Assignment for Marking Elements**:
   - **Problem**: The line `arr2[j] = -2;` is intended to mark the element as "used" or "processed," but it may conflict with actual array values (since `-2` could be a valid number in some contexts). Moreover, if `-2` is already an element in `arr2`, this could cause incorrect results.
   - **Optimization**: Instead of marking with `-2`, consider sorting the arrays first and using a two-pointer technique to find intersections. This will reduce the time complexity from `O(n * m)` to `O(n + m)`.

3. **Missing Return Statement**:
   - **Problem**: The function lacks a `return` statement, so it won't return the `ans` vector, leading to undefined behavior.
   - **Solution**: Add a return statement at the end of the function:
     ```cpp
     return ans;
     ```

### Optimized Approach Using Two-Pointer Technique:

Instead of using the nested loop approach (which has a time complexity of `O(n * m)`), we can optimize this using a two-pointer technique:

```cpp
#include <bits/stdc++.h> 
vector<int> findArrayIntersection(vector<int> &arr1, int n, vector<int> &arr2, int m)
{
    vector<int> ans;

    // Sort both arrays
    sort(arr1.begin(), arr1.end());
    sort(arr2.begin(), arr2.end());

    int i = 0, j = 0;

    while (i < n && j < m)
    {
        if (arr1[i] == arr2[j])
        {
            ans.push_back(arr1[i]);
            i++;
            j++;
        }
        else if (arr1[i] < arr2[j])
        {
            i++;
        }
        else
        {
            j++;
        }
    }

    return ans;
}
```

### Explanation of the Optimized Code:

1. **Sorting**: We sort both arrays to make it easier to find intersections.
2. **Two-Pointer Technique**: 
   - We use two pointers, `i` for `arr1` and `j` for `arr2`.
   - If the elements at both pointers are equal, it means we have found an intersection, so we add it to the result and increment both pointers.
   - If the element in `arr1` is smaller, we increment `i` to move to the next element.
   - If the element in `arr2` is smaller, we increment `j`.
3. **Efficiency**: This approach runs in `O(n log n + m log m)` due to the sorting step, but after sorting, the intersection is found in `O(n + m)` time.

This optimized solution is much more efficient than the original nested loop approach, especially when dealing with large arrays.

## Top voted solution

```cpp
#include <bits/stdc++.h> 
vector<int> findArrayIntersection(vector<int> &a, int n, vector<int> &b, int m)
{
    int i = 0, j = 0;
    vector<int> v;
    while (i < n && j < m)
    {
        if (a[i] == b[j])
        {
            // If the element is the same in both arrays, add it to the result
            v.push_back(a[i]);
            i++;
            j++;
        }
        else if (a[i] < b[j])
        {
            // If a[i] is smaller, move the pointer i to the next element
            i++;
        }
        else
        {
            // If b[j] is smaller, move the pointer j to the next element
            j++;
        }
    } 
    return v;
}
```

### Intuition:

The problem is about finding common elements between two sorted arrays. Since the arrays are sorted, a two-pointer technique can be efficiently used to traverse both arrays simultaneously and find matching elements.

### Approach:

1. **Two-Pointer Technique**:
    - **Initialization**: Start with two pointers, `i` and `j`, set to the beginning of the two arrays `a` and `b`, respectively.
    - **Comparison**: 
        - Compare `a[i]` and `b[j]`.
        - If they are equal, it means this element is common to both arrays, so add it to the result vector `v`, and increment both `i` and `j`.
        - If `a[i]` is smaller, increment `i` to move to the next element in `a`.
        - If `b[j]` is smaller, increment `j` to move to the next element in `b`.
    - **Continue** until one of the pointers reaches the end of its array.
2. **Return**: After exiting the loop, return the vector `v`, which contains all the common elements.

### Space Complexity:

- **Space Complexity**: `O(min(n, m))`
    - The only additional space used is for the result vector `v`, which will contain at most the smaller of the two array sizes (`n` or `m`). 
    - No extra space is required beyond that for data structures like maps or sets.

### Time Complexity:

- **Time Complexity**: `O(n + m)`
    - The algorithm involves a single traversal of both arrays, where each element in both arrays is visited exactly once. Therefore, the total time complexity is linear in terms of the sizes of the two arrays.

### Summary:

- **Intuition**: Leverage the sorted nature of the arrays to efficiently find common elements using a two-pointer technique.
- **Approach**: Use two pointers to traverse both arrays, compare elements, and collect common ones.
- **Complexity**: 
  - **Time**: `O(n + m)`
  - **Space**: `O(min(n, m))`

This approach is both time-efficient and space-efficient for finding the intersection of two sorted arrays.
