# Pascal's Triangle

## Problem Statment

Create a function, `pascals_triangle`, that returns the first `num_rows` of Pascal's Triangle. 

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

![pascals triangle visualization](../images/pascal-triangle-animated.gif)

The function will return a 2D array where the outer list stores the entire triangle and each index of the list stores the numbers in the nth row of Pascal's triangle. Index 0 will store the first row, index 1 will store the second row, and so on. 

The first row will always contain [1], the second row will always contain [1, 1]. Each row afterwards will have 1 as the first and last element and the middle elements will be calculated using the two numbers directly above it.

If the function receives a number that is less than 0, a `ValueError` is thrown.

(This problem is sourced from [LeetCode](https://leetcode.com/problems/pascals-triangle/description/))

**Example 1:**

```
Input: num_rows = 3
Output: [[1], [1, 1], [1, 2, 1]]
Explanation: The first index in the outer list contains one number: [1]. The second row contains two numbers: [1, 1]. The third row can be calculated by setting the first and last indexes to 1 and calculating the middle index using the two elements above it (1 + 1) so the third row is [1, 2, 1].
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
Output: [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1], [1, 5, 10, 10, 5, 1]]
Explanation: The first index in the outer list contains one number: [1]. The second row contains two numbers: [1, 1]. Each row afterwards can be calculated by setting the first and last index to 1 and calculating the middle elements using the two elements above it.
```

## Prompts

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: c5a19c81-1e98-416e-8bd6-4f32bb9975aa
* title: Ask Clarifying Questions
* topics: pse
##### !question

List three or more questions whose answers would clarify the problem statement

##### !end-question

##### !explanation

Here are some example clarifying questions:

1. What happens if the input is a number less than 1?
2. How large can the input size be?

##### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->

### !challenge
* type: code-snippet
* language: python3.6
* id: afcb3fb9-b225-4d48-b255-b0f3508de237
* title: Write Unit Tests
* topics: pse
##### !question

1. Use the comments provided to write at least two example input/outputs:
    * Consider at least one nominal and one edge case.
    * What is the expected output for the given input?
    * You can use the examples provided in the prompt, or other examples.
2. Write unit tests for `pascals_triangle` for the nominal and edge cases you identified in the first step.

*Note: Click the **Run Tests** button to save your tests for instructor feedback. No real tests are actually run again your unit tests.*

##### !end-question
##### !placeholder

```py
# example input 1:
# expected output 1:

# example input 2:
# expected output 2:

def test_nominal_case():
    # ^rename with meaningful test name
    # and complete test implementation below
    pass
    # arrange

    # act

    # assert

def test_edge_case():
    # ^rename with meaningful test name
    # and complete test implementation below
    pass
    
    # arrange
    
    # act
    
    # assert
```
##### !end-placeholder

##### !tests

```py
import unittest

class TestPython1(unittest.TestCase):
  def test_always_pass(self):
    self.assertEqual(1,1)
```

##### !end-tests
##### !explanation 

Example tests:

```python
def test_pascals_two_rows(self):
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

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 2df04c34-94fb-45f3-869a-09f96fef5e6b
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `pascals_triangle` in enough detail that someone else could write the code. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. For example, 1. Handle invalid input, 2. Given valid input, perform the computation/solve the problem/etc.
* Your logical steps could take the form of a numbered list, pseudo code, or anywhere in between. What's important at this stage is to think through and outline the implementation before writing code.

##### !end-question

##### !placeholder

Write the logical steps here.

##### !end-placeholder

### !end-challenge
<!-- prettier-ignore-end -->
