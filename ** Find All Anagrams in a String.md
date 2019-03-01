# Find All Anagrams in a String

## Description

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s**and **p** will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```



**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

## Solution 1: Sliding Window

```cpp
bool same(int* freq_s, int* freq_p) {
    for(int i = 0; i < 26; i++)
        if(freq_s[i] != freq_p[i])
            return false;
    return true;
}

vector<int> findAnagrams(string s, string p) {
    vector<int> res;
    
    if(s.size() < p.size())
        return res;
    
    assert(p.size() > 0);
    
    int freq_s[26] = {0}; // char frequency of s
    int freq_p[26] = {0}; // char frequency of p
    
    for(char c: p)
        freq_p[c - 'a']++;
    
    int l = 0, r = -1;
    
    while(l < s.size()) {
        if(r + 1 < s.size() && r - l + 1 < p.size())
            freq_s[s[++r] - 'a']++;
        else
            freq_s[s[l++] - 'a']--;
        
        if(r - l + 1 == p.size() && same(freq_s, freq_p))
            res.push_back(l);
    }
    
    return res;
}
```

$T(n)=O(n)$



Altenate implementations of *findAnagrams()*:

```cpp
vector<int> findAnagrams(string s, string p) {
    vector<int> res;
    
    if(s.size() < p.size())
        return res;
    
    assert(p.size() > 0);
    
    int freq_s[26] = {0}; // char frequency of s
    int freq_p[26] = {0}; // char frequency of p
    
    for(char c: p)
        freq_p[c - 'a']++;
    
    int l = 0;
    
    for(int r = 0; r < s.size(); r++) {
        freq_s[s[r] - 'a']++;
        
        if(r - l + 1 > p.size())
            freq_s[s[l++] - 'a']--;
        
        if(same(freq_s, freq_p))
            res.push_back(l);
    }
    return res;
}
```



```cpp
vector<int> findAnagrams(string s, string p) {
    vector<int> res;
    
    if(s.size() < p.size())
        return res;
    
    assert(p.size() > 0);
    
    int freq_s[26] = {0}; // char frequency of s
    int freq_p[26] = {0}; // char frequency of p
    
    for(char c: p)
        freq_p[c - 'a']++;
    
    int l = 0, r = -1;
    
    while(r + 1 < s.size()) {
        freq_s[s[++r] - 'a']++;
        
        if(r - l + 1 > p.size())
            freq_s[s[l++] - 'a']--;
        
        if(same(freq_s, freq_p))
            res.push_back(l);
    }
    return res;
}
```

