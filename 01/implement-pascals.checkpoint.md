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

Below is a representation of what the triangle looks like when the input is 5 (the first 5 rows of Pascal's Triangle) with the indices in the resulting 2d array marked.

![pascals triangle with indices marked](../images/pascals-triangle-full-with-indices.png)

If the function receives a number that is less than 0, a `ValueError` is thrown.

Please solve this problem using a dynamic programming approach. A dynamic programming approach requires re-using previously calculated rows to calculate additional rows.

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
    """
    A function that returns the first num_rows of Pascal's triangle.
  
    Parameters:
    num_rows (int): The number of rows to return
  
    Returns:
    list[list[int]]: 2D array where the outer list stores the entire triangle 
    and each index of the list stores the numbers in row `index + 1` 
    of Pascal's triangle.
    """
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
        numRows = 1

        # Act
        result = pascals_triangle(numRows)

        # Assert
        self.assertEqual(result, [[1]])

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
# Time complexity: O(N^2) where N is the number of rows. The outer loop will run N times, and the inner loop will run at most num_rows times.
# Space complexity: O(N^2) where N is the number of rows. The size of the array will be N + N - 1 + N - 2 + .... + 1, which calculates
# to N * (N + 1) / 2, which reduces down to O(N^2).
def pascals_triangle(num_rows):
    # handle edge case
    if num_rows < 0:
        raise ValueError("No input less than 0.")
        
    # initialize 2d array to hold triangle
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

<br>
<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
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
    numRows = 1

    # Act
    result = pascals_triangle(numRows)

    # Assert
    self.assertEqual(result, [[1]])

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
</details>

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: 2cf7eca9-1f15-47a3-a217-08dfdebbb71f
* title: Time Complexity of Solution
* points: 1

##### !question

What is the time complexity of your solution? Please define and explain your variables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: c48781b8-caf9-460a-af73-bf6e0b54585c
* title: Space Complexity of Solution
* points: 1 

##### !question

What is the space complexity of your solution? Please define and explain your variables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->