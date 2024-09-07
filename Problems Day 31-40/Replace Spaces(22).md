# Replace Spaces

## Problem Statement

You have been given a string `STR` of words. You need to replace all the spaces between words with `@40`.

## Detailed Explanation

- **Input**: A string containing words separated by spaces.
- **Output**: The same string with spaces replaced by `@40`.

### Constraints:
- 1 ≤ T ≤ 50
- 0 ≤ |STR| ≤ 100

Where `|STR|` is the length of the string including spaces.

**Time limit**: 1 second

## Sample Input 1:
```
2
Coding Ninjas Is A Coding Platform
Hello World
```

## Sample Output 1:
```
Coding@40Ninjas@40Is@40A@40Coding@40Platform
Hello@40World
```

### Explanation for Sample Output 1:
- In test case 1, after replacing the spaces with `@40`, the string becomes:  
  `Coding@40Ninjas@40Is@40A@40Coding@40Platform`
- In test case 2, after replacing the spaces with `@40`, the string becomes:  
  `Hello@40World`

## Sample Input 2:
```
3
Hello
I love coding
Coding Ninjas India
```

## Sample Output 2:
```
Hello
I@40love@40coding
Coding@40Ninjas@40India
```

### Explanation for Sample Output 2:
- In test case 1, no spaces are present, so the string remains:  
  `Hello`
- In test case 2, after replacing the spaces with `@40`, the string becomes:  
  `I@40love@40coding`
- In test case 3, after replacing the spaces with `@40`, the string becomes:  
  `Coding@40Ninjas@40India`

### Problem Understanding:
The goal of this code is to replace all spaces (`' '`) in a given string with the sequence `"@40"`. This type of problem could be useful when encoding URLs (where spaces are replaced by `%20`), or in cases where we need to avoid spaces and represent them in some specific format.

### Intuition:
When we encounter a space character in the string, instead of leaving it as is, we replace it with the sequence `@40`. This way, we preserve the content of the string but replace spaces with a more descriptive sequence.

### Logic and Approach:

1. **Input String**: We are given a string, and the goal is to iterate through every character in that string.
   
2. **Temporary String for Result**: A temporary string (`temp`) is created to store the result. This temporary string will contain the modified version of the input string, where spaces are replaced by `@40`.

3. **Iteration**: We iterate through each character of the input string:
    - If the character is a space (`' '`), append the characters `'@'`, `'4'`, and `'0'` to the temporary string. This is how we represent the space in the encoded format.
    - If the character is not a space, we simply append the current character to the temporary string.

4. **Return Result**: Once the loop is done, the temporary string contains the original string but with spaces replaced by `@40`. We return this temporary string as the result.

### Steps Breakdown:
1. **Initialize `temp`**: We start with an empty string (`temp = ""`), which will store the modified version of the input string.

2. **Loop Through Each Character**:
    - Use a `for` loop to iterate over each character in the input string:
      - If a space (`' '`) is encountered, we append the sequence `'@'`, `'4'`, and `'0'` to the `temp` string.
      - Otherwise, we append the current character directly to `temp`.
      
3. **Return the Result**: Once the loop finishes, return the `temp` string, which now contains the updated version of the input string.

### Example Walkthrough:

Let’s take the string `str = "Hello World"`.

- Start with `temp = ""`.
- First iteration (character `'H'`): Append `'H'` to `temp`, so `temp = "H"`.
- Second iteration (character `'e'`): Append `'e'` to `temp`, so `temp = "He"`.
- Continue for `'l'`, `'l'`, and `'o'`, until `temp = "Hello"`.
- Now, we encounter a space `' '`:
  - Instead of appending a space, we append `'@'`, `'4'`, and `'0'`, making `temp = "Hello@40"`.
- Continue for the rest of the string (`'W'`, `'o'`, `'r'`, `'l'`, `'d'`), resulting in `temp = "Hello@40World"`.

The final result is `Hello@40World`.

```cpp
#include <bits/stdc++.h> 
string replaceSpaces(string &str){
	string temp = "";// "" is correct, " " is incorrect.

	for(int i = 0; i < str.size(); i++)
	{
		if(str[i] == ' ')
		{
			temp.push_back('@');
			temp.push_back('4');//as temp is a string
			temp.push_back('0');
		}

		else
		{
			temp.push_back(str[i]);
		}
	} 
	return temp;//aaaah how did i forget this ::)
}
```

### Time Complexity:
- **O(n)**: We are iterating through each character of the input string exactly once. The string operations (appending characters) take constant time on average, so the overall time complexity is linear with respect to the length of the string, `n`.

### Space Complexity:
- **O(n)**: We are using a temporary string (`temp`) to store the result, which grows in size proportional to the input string. Therefore, the space complexity is also linear, `O(n)`.

### Summary:
- **Logic**: Iterate through the input string, replacing spaces with `@40` and appending the rest of the characters as they are.
- **Approach**: Use a temporary string to store the updated result and return it after processing the input string.
- **Efficiency**: This solution is optimal in terms of time and space, with both being O(n).

This simple algorithm is both efficient and easy to implement, making it a great solution for encoding spaces in a string.
