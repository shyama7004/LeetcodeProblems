# First and Last Position of an Element In Sorted Array

## Problem Statement

You have been given a sorted array/list `arr` consisting of `n` elements. You are also given an integer `k`.

Your task is to find the first and last occurrence of `k` in `arr`.

### Note:
1. If `k` is not present in the array, then the first and the last occurrence will be `-1`.
2. `arr` may contain duplicate elements.

## Example

**Input:**  
`arr` = [0, 1, 1, 5], `k` = 1

**Output:**  
1 2

**Explanation:**
If `arr` = [0, 1, 1, 5] and `k` = 1, then the first and last occurrence of 1 will be 1 (0-indexed) and 2.

## Detailed Explanation (Input/Output Format, Notes, Images)

### Sample Input 1:
```
8 2
0 0 1 1 2 2 2 2
```

### Sample Output 1:
```
4 7
```

**Explanation:**
For this testcase, the first occurrence of 2 is at index 4, and the last occurrence is at index 7.

### Sample Input 2:
```
4 2
1 3 3 5
```

### Sample Output 2:
```
-1 -1
```

## Expected Time Complexity:
Try to do this in `O(log(n))`.

## Constraints:
- `1 <= n <= 10^5`
- `0 <= k <= 10^9`
- `0 <= arr[i] <= 10^9`

**Time Limit:** 1 second

## Code
```cpp
#include<iostream>
#include<vector>
#include<cmath>
#include<algorithm>

using namespace std;

int firstOccurence(vector<int>& arr, int size, int key)
{
    int s = 0;
    int e = size - 1;

    int mid = s + (e - s)/2;
    int ans = -1;
    while(s <= e)
    {
        if(arr[mid] == key)
        {
            ans = mid;
            e = mid - 1;
        }

        else if(key > arr[mid])
        {
            s = mid + 1;
        }
        
        else if(key < arr[mid])
        {
            e = mid - 1;
        }
        mid = s + (e - s)/2;
    }
    return ans;
}

int lastOccurence(vector<int>& arr, int size, int key)
{
    int s = 0;
    int e = size - 1;

    int mid  = s + (e - s)/2;
    int ans = -1;

    while(s <= e)
    {
        if(arr[mid] == key)
        {
            ans = mid;
            s = mid + 1;
        }

        else if(key > arr[mid])
        {
            s = mid + 1;
        }
        
        else if(key < arr[mid])
        {
            e = mid - 1;
        }
        mid = s + (e - s)/2;
    }
    return ans;
    
}

pair<int, int> firstandlastOccurence()
{
    vector<int> arr = {0 ,0, 1, 1, 2, 2, 2, 2};
    int k = 2;
    int size = 8;

    pair<int, int> p;

    p.first = firstOccurence(arr, size, k);
    p.second = lastOccurence(arr, size, k);

    return p;
}

int main() 
{
    pair<int, int> result = firstandlastOccurence();
    cout << "The first index is " << result.first << " and the last index is " << result.second << endl;
    return 0;
}

```
### Code Explanation

1. **`firstOccurrence`**: 
   - This function finds the first occurrence of `key` in the sorted array `arr`.
   - It uses binary search to locate the key. Once found, it continues searching in the left part to ensure it's the first occurrence.
   - The variable `ans` stores the index of the first occurrence.

2. **`lastOccurrence`**:
   - This function finds the last occurrence of `key` in the sorted array `arr`.
   - It also uses binary search, but after finding the key, it continues searching in the right part to ensure it's the last occurrence.
   - The variable `ans` stores the index of the last occurrence.

3. **`firstAndLastPosition`**:
   - This function returns a pair of integers representing the first and last occurrences of the key `k` in the array.
   - It calls `firstOccurrence` and `lastOccurrence` to get the required indices.

### Logic and Intuition

- **Binary Search**: The core of the logic is based on binary search, which splits the array into halves and reduces the search space logarithmically. This makes the solution efficient with a time complexity of \(O(\log n)\).

- **First Occurrence**: 
  - If the middle element matches the key, move the `end` pointer to `mid - 1` to continue searching in the left part. This ensures you find the first occurrence.

- **Last Occurrence**:
  - Similarly, if the middle element matches the key, move the `start` pointer to `mid + 1` to continue searching in the right part, ensuring you find the last occurrence.

- **Pair of Indices**: The result is a pair of indices representing the first and last positions of the key in the array. If the key is not found, both values will be `-1`.
