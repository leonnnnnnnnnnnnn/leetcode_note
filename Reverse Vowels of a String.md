# Reverse Vowels of a String - LC 345

## Description

Write a function that takes a string as input and reverse only the vowels of a string.

**Example 1:**

```
Input: "hello"
Output: "holle"
```

**Example 2:**

```
Input: "leetcode"
Output: "leotcede"
```

**Note:**
The vowels does not include the letter "y".

## Solution 1: Two pointers

```cpp
string reverseVowels(string s) {
        int i = 0, j = s.size() - 1;
        
        string vowels("aeiouAEIOU");
        
        while(i < j) {            
            while(i < j && vowels.find(s[i]) == string::npos)
                  i++;
            while(i < j && vowels.find(s[j]) == string::npos)
                  j--;
                  
            if(i == j)
                  break;
            
            swap(s[i++], s[j--]);
        }
        
        return s;
    }
```

