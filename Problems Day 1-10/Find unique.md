# Find Unique

## Problem statement

You have been given an integer array/list (ARR) of size `N`, where `N` is equal to `[2M + 1]`.

Now, in the given array/list, `M` numbers are present twice, and one number is present only once.

You need to find and return that number which is unique in the array/list.

**Note:**  
The unique element is always present in the array/list according to the given condition.

## Detailed explanation
- **Input/output format**
- **Notes**
- **Images**

## Constraints

- `1 <= t <= 10^2`
- `0 <= N <= 10^3`
- **Time Limit**: 1 sec

## Sample Input 1:
```
1
7
2 3 1 6 3 6 2
```

## Sample Output 1:
```
1
```

**Explanation**: The array is `[2, 3, 1, 6, 3, 6, 2]`. Here, the numbers `2`, `3`, and `6` are present twice, and the number `1` is present only once. So, the unique number in this array is `1`.

## Sample Input 2:
```
2
5
2 4 7 2 7
9
1 3 1 3 6 6 7 10 7
```

## Sample Output 2:
```
4
10
```

## Code
```cpp
int findUnique(int *arr, int size)
{
    int ans = 0;
    
    for(int i = 0;i<size;i++)
    {
        ans = ans^arr[i];
    }
    return ans;
}
```

**Explanation**:  
In the first test case, the array is `[2, 4, 7, 2, 7]`. Here, the numbers `2` and `7` are present twice, and the number `4` is present only once. So, the unique number in this array is `4`.

In the second test case, the array is `[1, 3, 1, 3, 6, 6, 7, 10, 7]`. Here, the numbers `1`, `3`, `6`, and `7` are present twice, and the number `10` is present only once. So, the unique number in this array is `10`.

### Code Explanation and Intuition:

The code `findUnique` is designed to find the unique element in an array where every other element appears twice. This approach relies on the properties of the XOR (`^`) bitwise operator.

### Key Concepts:
1. **XOR Operator (`^`)**:
   - XOR of two bits is `1` if the bits are different, and `0` if they are the same.
   - XOR is both commutative and associative, meaning the order in which you apply XOR doesn't matter.

2. **Properties of XOR**:
   - `a ^ a = 0`: Any number XORed with itself results in `0`.
   - `a ^ 0 = a`: Any number XORed with `0` remains unchanged.
   - This means if you XOR all the numbers in an array, pairs of the same number will cancel each other out (because `n ^ n = 0`), and you’ll be left with the unique number.

### Step-by-Step Approach:
1. **Initialize `ans` to `0`**:
   - Start with `ans = 0` because XORing with `0` leaves the number unchanged.

2. **Iterate through the array**:
   - For each element in the array, XOR it with `ans`. If an element appears twice in the array, XORing it twice will cancel it out, effectively removing it from consideration.

3. **Return the Result**:
   - After looping through the entire array, `ans` will hold the value of the unique element that doesn’t have a pair.

### Example Walkthrough:
Consider an array `[2, 3, 1, 6, 3, 2, 1]`:
- Initial `ans = 0`
- XOR each element:
  - `0 ^ 2 = 2`
  - `2 ^ 3 = 1`
  - `1 ^ 1 = 0`  (pair cancels out)
  - `0 ^ 6 = 6`
  - `6 ^ 3 = 5`
  - `5 ^ 2 = 7`
  - `7 ^ 1 = 6` (all pairs cancel out, leaving `6`)

Final result: `ans = 6`, which is the unique number.

### Intuition:
The XOR operation efficiently cancels out all elements that appear twice, leaving only the element that appears once. This approach is optimal because it processes each element only once (O(n) time complexity) and uses constant space (O(1) space complexity).
