# 1047. Remove All Adjacent Duplicates In String

## Problem Statement

You are given a string `s` consisting of lowercase English letters. A duplicate removal consists of choosing two adjacent and equal letters and removing them.

We repeatedly make duplicate removals on `s` until we no longer can.

Return the final string after all such duplicate removals have been made. It can be proven that the answer is unique.

## Example 1:

**Input**:  
```
s = "abbaca"
```

**Output**:  
```
"ca"
```

**Explanation**:  
For example, in `"abbaca"` we could remove `"bb"` since the letters are adjacent and equal, and this is the only possible move. The result of this move is that the string is `"aaca"`, of which only `"aa"` is possible to remove, so the final string is `"ca"`.

## Example 2:

**Input**:  
```
s = "azxxzy"
```

**Output**:  
```
"ay"
```

## Constraints:

- 1 ≤ `s.length` ≤ 10⁵
- `s` consists of lowercase English letters.

## Solution

The line `store.pop_back()` only removes the last element from the `store` vector. It does not remove multiple elements at once. To understand how duplicates are removed using this line, let's consider the logic and sequence of operations in the `removeDuplicates` function.

### Function Logic

```cpp
#include <string>
#include <vector>

class Solution {
public:
    std::string removeDuplicates(std::string s) {
        std::vector<char> store;
        
        for (int i = 0; i < s.length(); i++) {
            if (!store.empty() && store.back() == s[i]) {
                store.pop_back();
            } else {
                store.push_back(s[i]);
            }
        }
        
        return std::string(store.begin(), store.end());
    }
};
```

### Explanation

1. **Initialization of `store`:** An empty vector `store` is created to keep track of characters.
2. **Loop through the string:** The function iterates through each character in the input string `s` using a for loop.
3. **Check the last character in `store`:**
   - `if (!store.empty() && store.back() == s[i])`: This condition checks if the `store` is not empty and the last character in the `store` is equal to the current character `s[i]`.
   - If the condition is true, `store.pop_back()` is called to remove the last character from `store`.
   - If the condition is false, the current character `s[i]` is added to `store` using `store.push_back(s[i])`.

### How Duplicates Are Removed

The function removes adjacent duplicates by checking the current character against the last character in the `store`:

- When a duplicate is found (`store.back() == s[i]`), it indicates that the last character in `store` is the same as the current character `s[i]`.
- The function then removes the last character from `store` using `store.pop_back()`. This effectively removes the duplicate character from the `store`.
- If there are consecutive duplicate characters in the input string, the function will remove each pair of duplicates one by one.

### Example Walkthrough

Consider the input string `s = "abbaca"`:

1. Initial state: `store = []`
2. Iterate over `s`:
   - `s[0] = 'a'`: `store = ['a']` (added 'a')
   - `s[1] = 'b'`: `store = ['a', 'b']` (added 'b')
   - `s[2] = 'b'`: Here, `store.back() == 'b'` and `s[2] == 'b'`, so the condition is true. We remove 'b' from `store` using `store.pop_back()`, resulting in `store = ['a']`.
   - `s[3] = 'a'`: Here, `store.back() == 'a'` and `s[3] == 'a'`, so the condition is true again. We remove 'a' from `store` using `store.pop_back()`, resulting in `store = []`.
   - `s[4] = 'c'`: `store = ['c']` (added 'c')
   - `s[5] = 'a'`: `store = ['c', 'a']` (added 'a')

The final `store` vector contains `['c', 'a']`, and the function returns "ca".

### Summary

The line `store.pop_back()` removes only the last element from `store`. The overall function logic ensures that adjacent duplicates are removed by checking each character against the last character in `store` and removing the last character when a duplicate is found. This process effectively removes both elements of a duplicate pair one at a time.
