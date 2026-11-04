# remove-all-adjacent-duplicates-in-string
feat: add Python solution for LeetCode 1047 (Remove All Adjacent Duplicates In String)  - Implement stack-based approach for linear time complexity - Add comprehensive README with algorithm explanation and performance analysis - Include local test cases for verification
# LeetCode 1047: Remove All Adjacent Duplicates In String

## Problem Description
Given a string `s` consisting of lowercase English letters, a **duplicate removal** consists of choosing two adjacent and equal letters and removing them.

We repeatedly make duplicate removals on `s` until we no longer can.

Return the final string after all such duplicate removals have been made. It can be proven that the answer is unique.

### Example 1:
* **Input:** `s = "abbaca"`
* **Output:** `"ca"`
* **Explanation:** In `"abbaca"`, the only adjacent pair is `"bb"`. We remove it to get `"aaca"`. In `"aaca"`, the adjacent pair is `"aa"`, which we remove to get `"ca"`. This is the final result.

### Example 2:
* **Input:** `s = "azxxzy"`
* **Output:** `"ay"`

### Constraints:
* `1 <= s.length <= 10^5`
* `s` consists of lowercase English letters.

---

## Algorithm Explanation
The problem requires us to eliminate adjacent duplicate characters iteratively. A **Stack** data structure is ideal for this pattern because the most recently added character is the first one that needs to be checked against a incoming match (Last-In, First-Out behavior).

### Step-by-Step Approach:
1. Initialize an empty list `stack` to keep track of the characters.
2. Iterate through each character `char` in the input string `s`.
3. For each character, check if the stack is not empty and if the top element of the stack (`stack[-1]`) is equal to the current character.
   * If they match, it means we have found an adjacent duplicate. **Pop** the element from the stack to remove it.
   * If they do not match (or the stack is empty), **push** (append) the current character onto the stack.
4. After processing the entire string, join the characters remaining in the stack into a single string and return it.

---

## Python 3 Source Code

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        stack = []
        
        for char in s:
            # If the stack has elements and the top element matches the current char
            if stack and stack[-1] == char:
                stack.pop()  # Remove the duplicate
            else:
                stack.append(char)  # Add the unique or non-matching char
                
        return "".join(stack)

# --- Local Testing Block ---
if __name__ == "__main__":
    solution = Solution()
    
    # Test case 1
    test1 = "abbaca"
    print(f"Input: {test1} -> Output: {solution.removeDuplicates(test1)} (Expected: 'ca')")
    
    # Test case 2
    test2 = "azxxzy"
    print(f"Input: {test2} -> Output: {solution.removeDuplicates(test2)} (Expected: 'ay')")
```

---

## Complexity Analysis

| Complexity | Scale | Reason |
| :--- | :--- | :--- |
| **Time Complexity** | **O(N)** | We iterate through the string of length `N` exactly once. Each character is pushed and popped from the stack at most once, which takes `O(1)` time per operation. |
| **Space Complexity** | **O(N)** | In the worst-case scenario (e.g., no duplicates present like `"abcdef"`), the stack will store all `N` characters of the string. |
