# Sum Of Two Arrays

## Problem Statement

You are given two numbers 'A' and 'B' in the form of two arrays (`A[]` and `B[]`) of lengths 'N' and 'M' respectively, where each array element represents a digit. You need to find the sum of these two numbers and return this sum in the form of an array.

### Note:

1. The length of each array is greater than zero.
2. The first index of each array is the most significant digit of the number. For example, if the array `A[] = {4, 5, 1}`, then the integer represented by this array is 451, and array `B[] = {3, 4, 5}` so the sum will be 451 + 345 = 796. You need to return `{7, 9, 6}`.
3. Both numbers do not have any leading zeros in them. Subsequently, the sum should not contain any leading zeros.

## Detailed Explanation

### Input/Output Format, Notes, Images

**Constraints:**
- 1 ≤ T ≤ 10²
- 1 ≤ N, M ≤ 10⁴
- 0 ≤ A[i], B[i] ≤ 9

**Time Limit:** 1 sec

### Sample Input 1:

```
2
4 1 
1 2 3 4
6
3 2
1 2 3
9 9    
```

### Sample Output 1:

```
1 2 4 0
2 2 2
```

### Explanation For Sample Input 1:

For the first test case, the integer represented by the first array is 1234, and the second array is 6, so the sum is 1234 + 6 = 1240.

For the second test case, the integer represented by the first array is 123, and the second array is 99, so the sum is 123 + 99 = 222.

### Sample Input 2:

```
2
3 3 
4 5 1
3 4 5
2 2
1 1
1 2
```

### Sample Output 2:

```
7 9 6
2 3
```
## Code
```cpp
#include <bits/stdc++.h> 
using namespace std;

vector<int> reverse(vector<int> v) {
    int s = 0;
    int e = v.size() - 1;

    while(s < e) {
        swap(v[s++], v[e--]);
    }
    return v;
}

vector<int> findArraySum(vector<int>& a, int n, vector<int>& b, int m) {
    int i = n - 1;
    int j = m - 1;

    vector<int> ans;
    int carry = 0;

    while(i >= 0 && j >= 0) {
        int val1 = a[i];
        int val2 = b[j];

        int sum = val1 + val2 + carry;
        carry = sum / 10;
        sum = sum % 10;

        ans.push_back(sum);
        i--;
        j--; 
    }

    // First case: first array is bigger than the second array
    while(i >= 0) {
        int sum = a[i] + carry;

        carry = sum / 10;
        sum = sum % 10;
        
        ans.push_back(sum);
        i--;  // Missing decrement
    }

    // Second case: second array is bigger than the first array
    while(j >= 0) {
        int sum = b[j] + carry;  // Use b[j] instead of a[j]

        carry = sum / 10;
        sum = sum % 10;

        ans.push_back(sum);
        j--;  // Missing decrement
    }

    // If there's any carry left, add it to the result
    if(carry > 0) {
        ans.push_back(carry);
    }

    return reverse(ans);
}

```

### Intuition and Logic

The problem is about adding two non-negative integers where each integer is represented by an array of digits. The goal is to simulate the addition of these two numbers, considering that the digits are stored in arrays. This approach mimics the way you perform addition by hand, starting from the least significant digit (the rightmost digit) and moving towards the most significant digit (the leftmost digit).

### Approach

1. **Start from the Last Digits**: 
   - We begin by adding the digits starting from the end (least significant digits) of both arrays, moving towards the start (most significant digits). This is similar to how addition is done manually.

2. **Consider Carry**:
   - Just like in manual addition, where sometimes the sum of two digits exceeds 9, we need to carry over the extra value to the next digit. We use a `carry` variable to keep track of this.

3. **Handle Different Lengths**:
   - The two arrays might be of different lengths. We need to handle the remaining digits in the longer array once we've exhausted the shorter array.

4. **Reverse the Result**:
   - Since we build our result starting from the least significant digit, the resulting array will be in reverse order. Therefore, we reverse it at the end.

### Explanation of All Cases

1. **When Both Arrays Have Digits Left**:
   - We add the digits from both arrays at positions `i` and `j`, along with any `carry` from the previous addition. The sum is split into two parts:
     - The digit to store in the result (`sum % 10`).
     - The carry to add to the next digit (`carry = sum / 10`).
   - After processing, we decrease both `i` and `j`.

2. **When the First Array Has Remaining Digits**:
   - If one array (let’s say the first array `a`) has remaining digits after the other (second array `b`) is fully processed, we continue adding the remaining digits of `a` to the result along with the carry.
   - We continue this until we run out of digits in `a`.
   - Decrement `i` in each iteration.

3. **When the Second Array Has Remaining Digits**:
   - Similar to the previous case, but this time it’s the second array `b` that has remaining digits. We add these digits to the result along with the carry.
   - Decrement `j` in each iteration.

4. **Handling the Final Carry**:
   - After processing all digits in both arrays, if there’s any carry left, it is added as a new digit to the result.

5. **Reversing the Result**:
   - Since we have added the digits starting from the least significant digit, the result is in reverse order. We reverse the array to get the correct order.

<div align = "center"><img src ="https://github.com/shyama7004/LeetcodeProblems/blob/main/Problems%20Day%2021-30/array.jpg"></div>

### Example Walkthrough

Consider the example with two arrays:
- `a = [9, 9]`
- `b = [1]`

**Step 1**: Start from the last digit of both arrays.
- Add `9` (from `a`) and `1` (from `b`): `9 + 1 = 10`, so `0` goes to the result, and `1` is carried over.

**Step 2**: Continue with the next digits.
- Now, only `9` from `a` is left and needs to be added to the carry: `9 + 1 = 10`, so again, `0` goes to the result, and `1` is carried over.

**Step 3**: No more digits left in both arrays, but we still have a carry of `1`.
- Add `1` to the result.

**Step 4**: The result array is `[0, 0, 1]`, which is in reverse order. After reversing, the final answer is `[1, 0, 0]`.

This approach ensures that the solution handles all possible scenarios correctly, resulting in the correct sum of the two numbers represented by the arrays.
