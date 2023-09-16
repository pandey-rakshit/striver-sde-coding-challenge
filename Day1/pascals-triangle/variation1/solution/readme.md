## Pascal Triangle - variation 1

### [Home](../../../README.md)

### [Question](../readme.md)

### [Variation - Home](../../readme.md)

## Naive - Solutions

we are given the row number r and the column number c,
and we need to find out the element at position (r,c)

**One of the Naive approaches** is to generate the entire pascal triangle and then find the element at position `(r,c)`. we will discuss in variation 3 how to generate pascal's triangle.

We have an easier formula for finding the element i.e. <sup>`r-1`</sup>`C`<sub>`c-1`</sub>.

Assume that `r-1 = n` and `c-1 = r`

Formula:

```

nCr = n! / (r! * (n-r)!)

```

We can separately calculate `n!`, `r!`, `(n-r)!` and using their values we can calculate `nCr`.
This is an extremely naive way to calculate. The time complexity will be `O(n) + O(r) + O(n-r)`.

## Optimal - Solution

The main idea is to reduce our time complexity or the time taken to calculate these factorial values.

can we manipulate the formula, lets see..

let us suppose, we are given value of n and r in <sup>n</sup>C<sub>r</sub>

assuming `n = 9 and r = 4`

```

n = 9
r = 4

<!-- according to formula -->

nCr = n! / (r! * (n-r)!)


9C4 = 9! / (4! * (9-4)!)

9C4 = (9 * 8 * 7 * 6 * 5!) / (4! * 5!)

5! is common on both nominator and denominator

9C4 = 9 * 8 * 7 * 6 * 5 / 4 * 3 * 2 * 1

we have shorten the formula and this calculation can be done using single formula with the time complexity of O(r).

```

### Approach

1. First, we will `consider r-1 as n and c -1 as r.`
2. After that, we will simple calculate the value of the combination using a loop.
3. The loop will run from `0 to r`. And each iteration, we will `multiply (n-i) with the result` and `divide the result by (i+1)`
4. Finally, the calculated value is the answer so `return the value`.

### Solution in python

```py

class Solution:
    def nCr(self, n, r):
      res = 1
      for i in range(r):
        res = res * (n - i)
        res = res // (i + 1)
      return res

```

> **Note**
>
> TimeComplexity O(c) where c = given column number
>
> Reason - we are running loop for r times, where r = c - 1
>
> Space complexity = O(1) as we are using one extra variable
