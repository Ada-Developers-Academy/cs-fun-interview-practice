# Implement Pascal's Triangle

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: c371a9d2-49b1-417b-abc4-3765e5cade18
* title: IPQ
* points: 3
### !question

Create a function, `pascals_triangle`, that returns the first `num_rows` of Pascal's Triangle. 

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

![pascals triangle visualization](../images/pascal-triangle-animated.gif)

The function will return a 2D array where the outer list stores the entire triangle and each index of the list stores the numbers in row `index + 1` of Pascal's triangle. For example, index 0 will store the first row, index 1 will store the second row, and so on. 

The first row will always contain [1], the second row will always contain [1, 1]. Each row afterwards will have 1 as the first and last element and the middle elements will be calculated using the two numbers directly above it.

If the function receives a number that is less than 0, a `ValueError` is thrown.

(This problem is sourced from [LeetCode](https://leetcode.com/problems/pascals-triangle/description/))

**Example 1:**

```
Input: num_rows = 3
Output: [[1], [1, 1], [1, 2, 1]]
Explanation: The 0th index (first row) in the outer list contains one number: [1]. 
The 1st index (second row) contains two numbers: [1, 1]. 
The 2nd index (third row) can be calculated by setting the first and last indexes to 1 
and calculating the middle index using the two elements above it (1 + 1) 
so the third row is [1, 2, 1].
```

**Example 2:**
```
Input: num_rows = 0
Output: []
Explanation: If there are 0 rows, the outer list will be empty.
```

**Example 3:**
```
Input: num_rows = 6
Output: [
    [1], 
    [1, 1], 
    [1, 2, 1], 
    [1, 3, 3, 1], 
    [1, 4, 6, 4, 1], 
    [1, 5, 10, 10, 5, 1]
]
Explanation: The first index (first row) in the outer list contains one number: [1].
The second index (second row) contains two numbers: [1, 1]. 
Each row afterwards can be calculated by setting the first and last index to 1 
and calculating the middle elements using the two elements above it.
```

### !end-question
### !placeholder

```python
def pascals_triangle(num_rows):
    pass
```
### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_pascals_nominal(self):
        # Arrange
        numRows = 3

        # Act
        result = pascals_triangle(numRows)

        # Assert
        self.assertEqual(result, [[1], [1, 1], [1, 2, 1]])

    def test_pascals_big_number(self):
        # Arrange
        numRows = 10

        # Act
        result = pascals_triangle(numRows)

        # Act
        self.assertEqual(result, [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1], [1, 5, 10, 10, 5, 1], [1, 6, 15, 20, 15, 6, 1], [1, 7, 21, 35, 35, 21, 7, 1], [1, 8, 28, 56, 70, 56, 28, 8, 1], [1, 9, 36, 84, 126, 126, 84, 36, 9, 1]])

    def test_pascals_base_case(self):
        # Arrange
        numRows = 2

        # Act
        result = pascals_triangle(numRows)

        # Assert
        self.assertEqual(result, [[1], [1, 1]])

    def test_pascals_out_of_range(self):
        # Arrange
        numRows = -1

        # Assert
        with self.assertRaises(ValueError):
            pascals_triangle(numRows)
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def pascals_triangle(num_rows):
    if num_rows < 0:
        raise ValueError("No input less than 0.")
        
    triangle = []

    for row_num in range(num_rows):
        # The first and last row elements are always 1.
        row = [None for _ in range(row_num + 1)]
        row[0], row[-1] = 1, 1

        # Each triangle element is equal to the sum of the elements
        # above-and-to-the-left and above-and-to-the-right.
        for j in range(1, len(row) - 1):
            row[j] = triangle[row_num - 1][j - 1] + triangle[row_num - 1][j]

        triangle.append(row)

    return triangle
```
### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->