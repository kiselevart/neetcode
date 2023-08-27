Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

**Input:** s = "()"
**Output:** true

**Example 2:**

**Input:** s = "()[]{}"
**Output:** true

**Example 3:**

**Input:** s = "(]"
**Output:** false

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of parentheses only `'()[]{}'`.

**thoughts**
* since this is in the stack part, this is obviously a stack question!
* to validate the string you need to make sure that:
	* there is the same number of corresponding brackets
	* that the brackets are facing the right way
	* that the open bracket is closed by the same type closed bracket
* kind of embarrassing, but im not making any progress on this problem
* think im going to look at the solution for this

**neetcode solution**
* creates empty stack
* creates a hashmap of closed brackets as keys with complementing open brackets as values
* loops through the string
* if the character is in the hashmap (is closing bracket)
* and if the most recently pushed open bracket to the stack is the same as the open bracket matching the current bracket (obviously has to be so as the open bracket before the current closing bracket must be complementary)
* then pop the opening bracket, as its valid and no longer needs to be checked
* otherwise return false
* if the character ISNT in the hashmap (is opening bracket)
* push it to the stack (append)
* if at the end of this loop all brackets match the stack must be empty as everything is pushed out
* therefore if not stack at the end return true otherwise false
```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s)%2 != 0:
            return False
            
        stack = []
        closeToOpen = { ")":"(", "}":"{", "]":"[" }
  
        for c in s:
            if c in closeToOpen:
                if stack and stack[-1] == closeToOpen[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)
                
        return True if not stack else False
```
**solution thoughts**
* thought that manually mapping the brackets to each other was too silly/only works for this specific problem as character set is low, which completely stumped me, but its seems to be the way you have to approach this problem
* added a check for odd lengths of s, since those are automatically invalid
* had no idea that array[-1] returns the most recently added element, very cool feature