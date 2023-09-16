## Pascal Triangle - variation 2

### [Home](../../../README.md)

### [Question](../readme.md)

### [Variation - Home](../../readme.md)

## Naive - Solutions

Given the row number n, Print the n-th row of pascal's triangle.

**In this approaches**, for every column from 1 to n,
we will calculate the element `(n,c) where n = given row number.` and `c = column number` that will vary from 1 to n.

### Naive Approach (using variation 1)

We will use a loop to iterate over each column i.e `1 to n`. And for each column, we will do following steps.

- first, we will consider `n-1 as n` and `c-1 as r`
- After that, we will simply calculate the value of the combination using a loop.
- The loop will run from 0 to r. and in each iteration, we will multiply (n-i) with the result and divide the result by (i+1)
- finally print the element

### Solution in Python

```py

class Solution:

  # from variation 1
    def nCr(self, n, r):
        res = 1

        for i in range(r):
            res = res * (n - i)
            res = res // (i + 1)
        return res


    def getRow(self, rowIndex: int) -> List[int]:
        lst = []
        rowIndex += 1
        for c in range(1, rowIndex+1):
            res = self.nCr(rowIndex - 1, c - 1)
            lst.append(res)

        return lst

```

### Code complexity

- Time complexity - `O(n * r)` where n = given row and r = column index vary from `0 to n - 1`

- Reasons - We are calculating the element for each column. now there are total `n` columns, and for each column, the calculation of the element takes `O(r)` time where `r is the column index.`

- Space complexity - 0(1) as we are not using any extra space.

## Optimal - Solution

We will try to build intuition for this approach using the following observation

![pascal triangle optimal solution observation](https://i.ibb.co/L5yBgrz/pascal-triangle-optimal.webp)

Here we can see that,

In each steps the numerator is multiplied by the previous consecutive element, and the denominator is multiplied by the next consecutive element.

```

correct element = prevElement * (rowNumber - colIndex) / colIndex

```

### Approach

- step 1 - First, we print the 1st element, i.e., 1 manually

- step 2 - After that, we will use a loop that runs from `1 to n - 1`. It will print the rest of the elements.

- step 3 - Inside the loop, we will use the above formula to print the element. - we will `multiply the previous answer by (n-1)` and then `divide it by index` itself

- step 4 - similarly entire row will be printed.

### Solution in python

```py

class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        ans = [1]
        rowIndex += 1
        for i in range(1, rowIndex):
            res = ans[i-1] * (rowIndex - i)
            res = res // i
            ans.append(res)

        return ans

```
