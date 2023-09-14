## [Solutions Approach](../readme.md)

### [Home](../../../../README.md)

### [Question](../../readme.md)

### Solutions - Brute Force

Brute force is all about achieving what is asked follow the question and try to solve it yourself.

check below diagram for clearing the approach

```

 step 4 - make every -1 to 0       step 3 - similarly, change
  and return the matrix          respective row to -1

  --             --           --               --
  |   1   0   1   |           |    1   -1   1   |
  |   0   0   0   |     <==   |   -1    0  -1   |
  |   1   0   1   |           |    1   -1   1   |
  --             --           --               --

                                        ^
                                        |
                                        |

  --             --           --               --
  |   1   1   1   |           |    1   -1   1   |
  |   1   0   1   |     ==>   |    1    0   1   |
  |   1   1   1   |           |    1   -1   1   |
  --             --           --               --

step 1 - start                step 2 - As soon you find 0
traversing the matrix         change respective column to -1

```

#### In step 2 and 3 we are changing it to -1 why not 0 ?

- we cannot change respective row or column to 0 at the same moment when we are traversing the matrix. Suppose when we traverse and we set the entire row to 0 then we cannot have track of the 0's in the initial matrix which will leads to setting zeros for wrong rows and column. hence a wrong solutions.

### Solutions using Python

```py

class Solution(object):

  def changeRow(self, matrix, i, n):
    for j in range(n):
        if matrix[i][j] != 0:
            matrix[i][j] = -1
    return matrix


  def changeCol(self, matrix, j, m):
    for i in range(m):
        if matrix[i][j] != 0:
            matrix[i][j] = -1
    return matrix


  def setZeroes(self, matrix):
    m = len(matrix)
    n = len(matrix[0])

    # step 1 - Traversing the matrix

    for i in range(m):
      for j in range(n):

        # step 2 and 3 - search for 0
        # As soon as you find 0 change respective row and column to 0

        if (matrix[i][j] == 0):
          matrix = self.changeCol(matrix, j, m)
          matrix = self.changeRow(matrix, i, n)

    # step 4 - change all the -1 to 0

    for i in range(m):
      for j in range(n):
        if matrix[i][j] == -1 :
          matrix[i][j] = 0
    return matrix

# Time Complexity = Time taken in traversing * time taken to change row and col to -1 + time taken to reset -1 to 0


# Time Complexity = O(n * m) * (n + m) + O(n * m)
# Time Complexity = somewhere near to O(n^3) if n == m

```
