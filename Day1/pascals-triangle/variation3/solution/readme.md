# Pascals Triangle - Solutions

### [Home](../../../README.md)

### [Question](../readme.md)

### [Variation - Home](../../readme.md)

## Problem Understanding

Before actually solving the problem we must understand the problem what the problem is all about

<p>In <strong>Pascal&#39;s triangle</strong>, each number is the sum of the two numbers directly above it as shown:</p>
<img alt="" src="https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif" style="height:240px; width:260px" />
<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> numRows = 5
<strong>Output:</strong> [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
</pre>

## Approaches

### Naive Approach

The naive approach is basically a combination of variation 1 and variation 2.

Here, for every row from 1 to n, we will try to generate all the row elements by simply using the naive approach of variation 2. So, we will use the same code as variation 2(naive approach), inside a loop (i.e, row runs from 1 to n)

#### Approach

- step 1 - First, we will run a `loop(say row) from 1 to n.`

- step 2 - We will use a `loop (say col) to iterate over each column i.e. from 1 to row + 1.` And inside the nested loops, we will do the following steps

  - First, we will consider `row - 1 as n and col - 1 as r.`

  - After that, we will simply calculate the value of the combination using a loop.

  - The `loop will run from 0 to r`. And in each iteration, `we will multiply(n - i) with the result and divide the result by (i+1)`

  - finally, we will add the element to a temporary list.

- step 3 - After calculating all the elements for all columns of a row, we will add the temporary list to our final answer list.

- step 4 - finally, we will return the answer list.

### Solution in python

```py

class Solution:

    # variation 1
    def nCr(self, n, r):
        res = 1

        # calculating nCr:
        for i in range(r):
            res = res * (n - i)
            res = res // (i + 1)

        return res


    def generate(self, numRows: int) -> List[List[int]]:
        ans = []
        for row in range(1, numRows+1):
            tempLst = []
            for col in range(1, row+1):
                ele = self.nCr(row - 1, col - 1)
                tempLst.append(ele)
            ans.append(tempLst)
        return ans

```

> **Note:**
>
> Time complexity: O(n \* n \* r) ~ O(n<sup>3</sup>), where n = no. of rows and r = column index.
>
> Reason - The row loop will run for approximately n times. And generate a row using the naive approach of variation 2 takes O(n \* r) time complexity

### Optimal Approach

Now, in the optimal approach of variation 2, we have learned how to generate a row in O(n) time complexity.

So, in order to optimize the overall time complexity, we will be using that approach for every row. Thus the total time complexity will reduce.

#### Approach

- step 1 - First we will run a `loop say row from 1 to n.`

- step 2 - inside the loop we will `call a generateRow() function` and add the returned list to our final answer.

  Inside the function we will do the following

  - First, we will `store the 1st element i.e., 1 manually.`

  - After that, we will use a `loop (say col) that runs from 1 to n-1`. It will store the rest of the elements.

  - Inside the loop, we will use the specified formula to print the element. we will `multiply the previous answer by (row - col)` and `divide it by col itself.`

  - Thus, the entire row will be stored and returned.

### Solution in python

```py

class Solution:

    def generateRow(self, n):
        row = [1]
        for i in range(1, n):
            res = row[i - 1] * (n - i)
            res = res // i
            row.append(res)
        return row




    def generate(self, numRows: int) -> List[List[int]]:
        ans = []
        for row in range(1, numRows+1):
            ans.append(self.generateRow(row))
        return ans


```

> **Notes:**
>
> Time Complexity: `O(n`<sup>`2`</sup>`)`, where `n = number of rows(given)`.
>
> Reason: We are generating a row for each single row. ` The number of rows is n`. And generating an entire row takes `O(n)` time complexity.
