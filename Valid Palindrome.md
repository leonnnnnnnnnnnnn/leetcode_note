# Valid Palindrome

## Description

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

**Example 1:**

```
Input: "A man, a plan, a canal: Panama"
Output: true
```

**Example 2:**

```
Input: "race a car"
Output: false
```

## Solution 1: Two pointers

```cpp
bool isPalindrome(string s) {
        auto i = s.begin();
        auto j = s.end() - 1;

        while(i < j) {
            while(i < j && !isalnum(*i))
                i++;
            
            while(j > i && !isalnum(*j))
                j--;
            
            if(i == j)
                break;

            if (tolower(*i) != tolower(*j))
                return false;

            i++;
            j--;
        }

        return true;
}
```

