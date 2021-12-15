---
description: >-
  Given a string containing digits from 2-9 inclusive, return all possible
  letter combinations that the number could represent. Return the answer in any
  order.A mapping of digit to letters (just like
---

# Letter Combinations of a Phone Number

```
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []
        self.mapping = {'2': ['a', 'b', 'c'],
                 '3': ['d', 'e', 'f'],
                 '4': ['g', 'h', 'i'],
                 '5': ['j', 'k', 'l'],
                 '6': ['m', 'n', 'o'],
                 '7': ['p', 'q', 'r', 's'],
                 '8': ['t', 'u', 'v'],
                 '9': ['w', 'x', 'y', 'z']}
        result = []
        self.helper(result, [], 0, digits)
        return result
    def helper(self, result, subset, index, digits):
        if index == len(digits):
            result.append(''.join(subset))
        else:
            for i in self.mapping[digits[index]]:
                self.helper(result, subset + [i], index + 1, digits)
```
