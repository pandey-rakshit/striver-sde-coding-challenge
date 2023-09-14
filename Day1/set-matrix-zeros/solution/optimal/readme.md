## [Solutions Approach](../readme.md)

### [Home](../../../../README.md)

### [Question](../../readme.md)

### Solutions - Optimal Solution

So in the better-than-naive solution we reduced the time complexity to `n`<sup>`2`</sup>
but, the space complexity is also added to `O(n) + O(m)`

We can try to optimize this solution as well

We cannot reduce more time complexity as its equal to matrix traversal. However, we can try to reduce are space complexity.

> QNA:
>
> Can we merge or coincide these two separate arrays within our given matrix?

lets try and Replace the outer array with the first row/column of the matrix for manipulation.

> **Note:**
>
> Things to remember,
> we will be using first row and first column for marking rows and column although it will create a issue as our ( 0,0 ) index will be common for both first row and first column How to solve this ??

### How to solve the index problem ?

lets take the fist column and suppose it represent the row array
and first row except the first column represent the column array.

now we can see 1 column is less in the column array so lets take a variable col0 to represent the missing column.

![index problem](https://i.ibb.co/gtg2ZRW/index-problem.webp)

```


col0 = 1                          col0 = 1
 --             --                --             --
 |   1   0   1   |  col           |   1   0   1   | col
 |   0   0   0   |     <==        |   0   0   1   |
 |   1   0   1   |                |   1   1   1   |
 -- row         --                -- row         --
        step 4                            step 3

                                              ^
                                              |
                                              |

  col0 = 1                        col0 = 1
  --             --              --              --
  |   1   1   1   | col          |   1    0   1   | col
  |   1   0   1   |     ==>      |   1    0   1   |
  |   1   1   1   |              |   1    1   1   |
  -- row         --              --  row         --
        step 1                            step2

```

step 1: Initialize col0 to 1 and traverse the matrix and search for 0

step 2 and 3: As soon as you find 0 mark it using first column and first row.

Note - add a condition for (0,0) special case - row / column representation

- index `[0][0]` - responsible for changes in the first row
- `col0` - responsible for changes in the first column

check if represented `[i][0]` in first col is zero or not
if yes i.e., j = 0 so set col0 = 0 as col0 will represent future changes in that col. instead of `[0][0]` which is representing rows.

step 4 : Now traverse through the matrix for setting rows and column to 0 in specific order -

- 1 - Part of matrix that is not used for marking - first iteration of matrix from `[1->m][1->n]` for setting rows and column value to 0
- 2 - now first we set value of row first that is represented by `[0][0]` why ? - because if we set column value first then there may be chance of changing `[0][0]` which well then lead to change in 1st row and hence can change the answer value.
- 3 - after changing 1st row. change the 1st column.

#### How it helps us to improve time and space complexity ?

- initially, In the better-than-naive approach,
  overall time complexity was O(n \* m) - matrix traversal
  and space complexity was O(n) + O(m) - because of array that we created

- now we removed or coincide the arrays in the matrix itself the extra O(n)+O(m) space was removed and we use one separate variable to store single variable i.e O(1) i.e. constant.

Hence the optimal solution

lets check the solution using python

### Solutions using Python

```py

class Solution(object):
    def setZeroes(self, matrix):
      m = len(matrix)
      n = len(matrix[0])

      # step 1: Initialize col0 to 1
      col0 = 1

      # traverse the matrix and search for 0
      for i in range(m):
        for j in range(n):

          if matrix[i][j] == 0:
            # [i][0] representing to row's = 0
            matrix[i][0] = 0

            # Note - add a condition for (0,0) special case - row / column representation

            # index [0][0] - responsible for changes in the first row
            # col0 - responsible for changes in the first column

            # check if [i][0] in first col is zero or not
            # if yes i.e., j = 0 so set col0 = 0 as col0 is representing future changes in that col. instead of [0][0] which is representing rows.

            if j != 0:
              matrix[0][j] = 0
            else:
              col0 = 0


      # step 4 : Now traverse through the matrix for setting rows and column to 0 in specific order -
      # 1 - Part of matrix that is not used for marking - first iteration of matrix from `[1->m][1->n]` for setting rows and column value to 0
      for i in range(1, m):
        for j in range(1, n):
          if matrix[i][0] == 0 or matrix[0][j] == 0:
            matrix[i][j] = 0

      # 2 - now first we set value of row first that is represented by `[0][0]`
      # why ? - because if we set column value first then there may be chance of changing `[0][0]`
      # which well then lead to change in 1st row and hence can change the answer value.
      if matrix[0][0] == 0:
        for j in range(n):
            matrix[0][j] = 0

      # 3 - after changing 1st row. change the 1st column.
      if col0 == 0:
        for i in range(m):
            matrix[i][0] = 0

      return matrix


```
