## [Solutions Approach](../readme.md)

### [Home](../../../../README.md)

### [Question](../../readme.md)

### Solutions - Better Solution

So in the naive solution we saw the time complexity is reaching approx n<sup>3</sup>

We can try to optimize the solution a little bit
We saw changing rows and col when seeing 0 cost us increase in time complexity

```py

    for i in range(m):
      for j in range(n):
        if (matrix[i][j] == 0):
          matrix = self.changeCol(matrix, j, m)
          matrix = self.changeRow(matrix, i, n)

    #  how can we remove these function or reduce our time complexity


```

can we use something to mark our rows and column to which we need to set 0 at the end of the day

What if we can use separate array's and mark index to identify our rows and col which will be set to 0

Let look carefully to the below diagram

```

    [   1   0   1   ] col              [   1   0   1   ] col
    --             --                  --             --
 1  |   1   0   1   |               1  |   1   1   1   |
 0  |   0   0   0   |     <==       0  |   1   0   1   |
 1  |   1   0   1   |               1  |   1   1   1   |
row --             --             row  --             --
        step 4                            step 3

                                              ^
                                              |
                                              |


    [   1   1   1   ] col             [   1   0   1   ] col
     --             --                --              --
  1  |   1   1   1   |             1  |   1    1   1   |
  1  |   1   0   1   |     ==>     1  |   1    0   1   |
  1  |   1   1   1   |             1  |   1    1   1   |
row  --             --           row  --              --
        step 1                            step2


step 1: initialize two array of size m and n representing row and col, and set each element to 1

step 2 and 3: traverse the array and search for 0 once you find it mark the row and col index using the array we created initially and set to 0 as shown in figure.

 step 4: Traverse the matrix again check if the corresponding row or col is marked using col and row array if Yes change the element to 0 and at last return the matrix
```

#### How it helps us to improve time complexity ?

- initially, In the naive approach,
  we were using two function that were using O(n+m) to set respective rows and col to -1

- now we eliminated that step instead we bring two arrays and we will mark index using those array which will be O(1 + 1) operation

hence overall time complexity will be O(n \* m) - matrix traversal
but we will have space complexity of O(n) + O(m) - because of array that we created

lets check the solution using python

### Solutions using Python

```py

class Solution(object):
    def setZeroes(self, matrix):
      m = len(matrix)
      n = len(matrix[0])

      # step 1: initialize two array of size m and n representing row and col,
      # and set each element to 1
      row = [1] * m
      col = [1] * n

      # step 2 and 3: traverse the array and search for 0
      # once you find it mark the row and col index using
      # the array we created initially and set to 0.

      for i in range(m):
        for j in range(n):
          if (matrix[i][j] == 0):
            row[i] = 0
            col[j] = 0

      # step 4: Traverse the matrix again check
      # if the corresponding row or col is marked using col and row array
      # if Yes change the element to 0 and at last return the matrix

      for i in range(m):
        for j in range(n):
          if (row[i] == 0 or col[j] == 0):
            matrix[i][j] = 0

      return matrix


```
