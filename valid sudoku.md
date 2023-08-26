Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

**Example 1:**

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

**Input:** board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
**Output:** true

**Example 2:**

**Input:** board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
**Output:** false
**Explanation:** Same as Example 1, except with the **5** in the top left corner being modified to **8**. Since there are two 8's in the top left 3x3 sub-box, it is invalid.

**Constraints:**

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`.

**thoughts**
* board is a 2D array, returning bool
* need some sort of validation algorithm here
* brute force would check if only one instance in row, column or box otherwise return false

algo for checking column validity
```python
        col = [[0]*9 for x in range(9)]
        for i in range(0,8):
            for j in range(0,8):
                if board[j][i] in col[i]:
                    return False
                col.append(board[j][i])
```

**iterating through 3x3 grid**
the pattern for each 3x3 is:
```python
[0,0 0,1 0,2] [0,3 0,4 0,5]
[1,0 1,1 1,2] [1,3 1,4 1,5]
[2,0 2,1 2,2] [2,3 2,4 2,5]
```
those are the first two grids
now I need to find a way to iterate through each grid 1 by 1

the innermost loop should go through the grid like so:
```python
for i in range(row, row+3):
	for j in range(col, col+3):
		#access board[i][j]
```
now what lets me iterate through the grid with this

suppose row and col indexes are 0,0 at the start
then the col index gets 3 added
now it will go through starting from 0,3
then go through 0,6

now we have to add 3 to the row index
what lets me do this

```python
for row in range(0,9,3):
	for col in range(0,9,3):
		print(row,col)
```
this might work, have to test
the third number in the range function is the step

that works.
now i just have to set up an empty 1D array named grid before the i and j loops
this array will check if a value has already come up within the grid, otherwise will append it to the array

**debugging**
[[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."]]
saving this empty test case here
[["5","5",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."]]
row testcase
[["5",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],["5",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],["",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".",".","."]]
grid testcase

after around an hour and a half of debugging i present this abomination:
```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        for row in range(0,9,3): #handles 3x3 grid check
            for col in range(0,9,3):
                grid = [] 
                for i in range(row, row+3):
                    for j in range(col, col+3):
                        if board[i][j] in grid and board[i][j] != '.':
                            return False
                        grid.append(board[i][j])
                        
        for i in board: #handles row checking
            row = []
            for j in i:
                if j in row and j != '.':
                    print(j)
                    return False
                row.append(j)

        for i in range(9): #handles column checking
            col = []
            for j in range(9):
                if board[j][i] in col and board[j][i] != '.':
                    return False
                col.append(board[j][i])

        return True #valid return
```

**explanation**
* goes through the board with a 3x3 grid, returns False if any duplicates found
* goes through the board row by row, returns False if any duplicates found
* goes through the board column by column, returns False if any duplicates in found
* if all checks are passed, returns True

**code review**
* this is essentially just brute force.
* i am assuming there is a much better and simple solution, possibly to do with hash maps or some sort of math algorithm that counts up the values
* this array method is simply the first idea that i thought of and i kept on with it until it worked
* this solution is in the median both for runtime and space complexity
* can also put the 3x3 check at the bottom instead for slightly faster runtime as the faster loop gets checked first

**neetcode solution**
* using integer division to find the index of the 3x3 grid, very clever
* uses hashsets for each subdivision (rows, cols, grids)
* for each value in the board checks if its empty
* checks if is already in any of the hashsets
* if not it adds it in
* for rows the key is the row
* for cols the key is the column
* for grids the key is the integer division of both row and column, basically the coordinate of which grid we are in on the sudoku board

**code**
```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        cols = collections.defaultdict(set)
        rows = collections.defaultdict(set)
        grids = collections.defaultdict(set)
        
        for r in range(9):
            for c in range(9):
                if board[r][c] == '.':
                    continue
                if (board[r][c] in rows[r] or
                    board[r][c] in cols[c] or
                    board[r][c] in grids[(r//3, c//3)]):
                    return False
                cols[c].add(board[r][c])
                rows[r].add(board[r][c])
                grids[(r//3, c//3)].add(board[r][c])
                
        return True
```
