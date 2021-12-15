---
description: Given a string s, return the longest palindromic substring in s.
---

# Longest Palindromic Substring

```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        #dp[i, j] = true if s[i] == s[j] and dp[i+1, j-1]
        #dp[i, i] = true
        #dp[i, i + 1] = true if s[i] == s[i + 1]
        max_string = ""
        if not s:
            return ""
        dp = [[False] * len(s) for _ in range(len(s))]
        for i in range(len(s)):
            dp[i][i] = True
            max_string = s[i]
        
        for i in range(len(s) - 1, -1, -1):
            for j in range(i + 1, len(s)):
                if s[i] == s[j]:
                    if j - i == 1 or dp[i + 1][j - 1]:
                        dp[i][j] = True
                        if (j - i + 1) > len(max_string):
                            max_string = s[i:j+1]
        return max_string
```
