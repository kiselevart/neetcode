Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3
**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1
**Output:** ["()"]

**Constraints:**

- `1 <= n <= 8`

**thoughts**
* well formed parentheses just mean they complete each other, regardless of what the others do
* so parenthesis 1 should be open and the last parenthesis should be closed for example
* how to even create these parenthesis pairs
* this is like math probability permutation stuff
* to create the permutations can take the number of spaces, which is the number of pairs * 2
* calculate all possible ways the open brackets can fit, and then just fit the closed brackets into the empty spaces