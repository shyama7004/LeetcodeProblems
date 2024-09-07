# Maximum Occurring Character

Given a string `str` of lowercase alphabets, the task is to find the maximum occurring character in the string `str`. If more than one character occurs the maximum number of times, then print the lexicographically smaller character.

## Example 1:

**Input**:
```
str = testsample
```

**Output**:
```
e
```

**Explanation**: `e` is the character that occurs the most frequently.

## Example 2:

**Input**:
```
str = output
```

**Output**:
```
t
```

**Explanation**: `t` and `u` have the same frequency, but `t` is lexicographically smaller.

## Your Task:

The task is to complete the function `getMaxOccuringChar()` which returns the character that occurs the most frequently.

### Expected Time Complexity:
- O(N)

### Expected Auxiliary Space:
- O(Number of distinct characters)

**Note**: N = |s|

## Constraints:
- 1 ≤ |s| ≤ 100

### Problem Intuition

You are asked to find the character that appears the most in a given string, and return that character. The code essentially does this by counting the occurrences of each character in the string and determining which one appears the most frequently.

### Logic Breakdown and Explanation:

#### Step 1: Initialize a frequency array
```cpp
int arr[26] = {0};
```
- This array represents the frequency of each lowercase letter. Since there are 26 letters in the English alphabet, we create an array of size 26 and initialize all elements to zero. The index `0` represents 'a', `1` represents 'b', and so on up to `25` for 'z'.

#### Step 2: Count the frequency of each character
```cpp
for (int i = 0; i < s.size(); i++) {
    char ch = s[i] - 'a';
    arr[ch]++;
}
```
- The code loops through each character of the string.
- `char ch = s[i] - 'a';`:
  - This converts the character `s[i]` (a lowercase letter) to an integer corresponding to its position in the alphabet. For example, `'a' - 'a' = 0`, `'b' - 'a' = 1`, etc.
- The `arr[ch]++` increases the count of the character `s[i]` in the frequency array `arr`.

#### Step 3: Find the character with the maximum frequency
```cpp
int maxi = -1;
int ans = 0;

for (int i = 0; i < s.size(); i++) {
    if (maxi < arr[i]) {
        maxi = arr[i];
        ans = i;
    }
}
```
- The variables `maxi` and `ans` are used to store the maximum frequency and the index (character) corresponding to that frequency, respectively.
- The loop iterates over the frequency array `arr`. For each index `i`, it checks if the frequency at that index (`arr[i]`) is greater than the current maximum (`maxi`). If so, it updates `maxi` with `arr[i]` and updates `ans` to the index `i`.

#### Step 4: Return the character
```cpp
return 'a' + ans;
```
- The index `ans` represents the position of the most frequent character. To get the actual character, we add `'a'` to `ans`. Since `'a'` is the base character (ASCII value 97), adding `ans` gives us the correct character.

#### Step 5: Main Function
```cpp
int main() {
    string s;
    cout << "Enter your string here: " << endl;
    cin >> s;
    char c = getmaxOccChar(s);
    cout << "The char that has occurred the max time: " << c << endl;

    return 0;
}
```
- This function asks the user for a string input, calls `getmaxOccChar` to get the most frequent character, and prints the result.

### Improvements Needed:
The second loop in the function is incorrect since it is iterating over the string's length (`s.size()`) instead of the array of size 26, and this could cause incorrect results. Here's the fix:
```cpp
for (int i = 0; i < 26; i++) {
    if (maxi < arr[i]) {
        maxi = arr[i];
        ans = i;
    }
}
```

### Conclusion:
This code efficiently finds the most frequent character in a string. However, it's restricted to lowercase English letters. The array keeps track of the frequency of each letter, and the logic compares these frequencies to find the one that appears the most.
