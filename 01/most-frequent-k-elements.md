# Most Frequent K Elements

## Problem Statement

Create a function, `most_frequent_k_elements`, that takes a non-empty array of integers and return the k most frequent elements. (Note: You may assume k is always valid, 1 ≤ k ≤ number of unique elements.)

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**
```
Input: nums = [1], k = 1
Output: [1]
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

List three or more questions whose answers would clarify the problem statement.

For each question, provide an explanation which includes the effect your decision would have on how you would approach the problem.

##### !end-question

##### !explanation

Here are some example clarifying questions:

1. Can the input array contain negative numbers?
2. What if there is a tie for the most frequent elements? E.g., what if k is 3, but there are two values tied for the 3rd most frequent element?
3. Will the input array always be in sorted order?
4. Must the output list be in a particular order?


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
2. Write unit tests for `most_frequent_k_elements` for the nominal and edge cases you identified in the first step.

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
def test_negative_numbers():
    # Arrange
    arr = [-1,-1,2,3,3,3]
    k = 2 
    # Act
    result = most_frequent_k_elements(arr, k)

    # Assert
    assert result == [3,-1]

def test_unordered_numbers():
    # Arrange
    arr = [3, 1, 2, 3, 1, 3]
    k = 2 
    # Act
    result = most_frequent_k_elements(arr, k)

    # Assert
    assert result == [3, 1]
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

Without writing code, describe how you would implement `most k frequent elements` using hash tables in enough detail that someone else could write the code. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. For example, 1. Handle invalid input, 2. Given valid input, perform the computation/solve the problem/etc.
* Your logical steps could take the form of a numbered list, pseudo code, or anywhere in between. What's important at this stage is to think through and outline the implementation before writing code.

##### !end-question

##### !placeholder

Write the logical steps here.

##### !end-placeholder

##### !hint
1. How could we use a hash/frequency map to keep track of how many times an integer shows up? 
2. Is there a way we could use the frequency map to sort the integers based on their number of occurrences? 
##### !end-hint

#### !explanation
1. Handle edge cases
2. Initialize hash that holds integer occurences
3. Loop through unique integers
    1. Sort them in descending order
4. Return list
#### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->
