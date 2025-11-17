# Most Frequent K Elements

## Problem Statement

Create a function, `most_frequent_k_elements`, that takes a non-empty array of integers and returns the `k` most frequent elements. 
- You may assume `k` is always valid, where `1 ≤ k ≤ number of unique elements`.

**Example 1:**

```
Input: numbers = [1, 1, 1, 2, 2, 3], k = 2
Output: [1, 2]
```

**Example 2:**
```
Input: numbers = [1], k = 1
Output: [1]
```

## Prompts

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: c5a19c81-1e98-416e-8bd6-4f32bb9975aa
* title: Describe Your Understanding
* topics: pse
##### !question

Before you begin solving this problem, take a moment to think like a professional software engineer. 
- What do we know about the problem? 
- What assumptions can we make based on the information in the problem statement? 
- What further information do the example inputs and outputs give us?
- What questions would you ask a teammate, product manager, or interviewer to better understand the problem before writing any code?

<br>

In the box below, list 5 or more observations about the problem or questions whose answers would clarify the problem statement. For each observation or question, include information on why that observation is important or why you are asking the question.
- For each observation, answer how that observation will affect your approach to the problem.
- For each question, describe what you are hoping to clarify about the problem and provide an answer which includes the effect your decision would have on how you might approach the problem.

<br>

As you come up with observations and questions, assume that error handling for invalid data is managed outside the function. We want to focus on the core behavior of the function we will write. 

##### !end-question
##### !hint

Further questions to ask as you read through the problem statement and examples:
- What is the goal of the function?
- What are the types of the expected inputs and outputs?
- Are there any restrictions on any of the inputs?
  - For example: if any of the inputs are a list, do we know anything about how the list is ordered?
- What do the examples show us about the data types and values that are allowed for our inputs?
- What do the examples tell us about the return value in different scenarios?
- Reflecting on the observations you have made so far, what questions would give you new information?

<br>

Consider the following for inspiration:
- [About PSEs](../about-pses/about-pses.md)
- [Our example PSE with example answers](../about-pses/example-pse.md)
- Previous PSEs

##### !end-hint
##### !explanation

One of many possible responses could look like:

1. We are told that we will be given a non-empty list of input and that `1 ≤ k ≤ number of unique elements`.
    - Since there will always be values in the input list, and `k` will always be valid and less than or equal to the number of unique elements in the list, our function can operate assuming that it will always be able to return a result.

2. The problem statement says that we should return `k` elements, but does not specify a data type. The examples show list syntax (`[]`) for the output.
       - While a tuple or set could work depending on if the result needs to be mutable or if we need to preserve a certain ordering, based on the examples I will return a list. 

3. What if there is a tie for the most frequent elements? E.g., what if k is 3, but there are two values tied for the 3rd most frequent element?
    - Since the problem statement says to return `k` most frequent elements, if there is a tie I will choose the first element found rather than returning all tied elements.

4. Will the input array always be sorted in ascending order?
    - We can write a more general function that processes the input list element by element building a frequency map and that would be fairly efficient for smaller lists. 
    - If we were working with a large input list with many duplicates, that is sorted in ascending order,
      we could find the counts for each value in the list a little differently: 
        1) As we reach an element that is a new value, we could do a binary search on the remainder of the list to find the last index holding that value (the index where the next element is a new number). 
        2) Then we can take the difference of the current index and the last index to get a count for that value update our frequency map, and move to the next number. 

      The notes around the list being large and having repeats is important, if we had a list of only unique elements, this searching approach would not be very useful. 

5. Must the output list be in a particular order?
    - In the examples, it is unclear if the output is sorted by ordering the most frequent values first or by the order that the values were encountered in the input. Since this problem is concerned with the most frequent values, I will assume that the output should be sorted in desending frequency so that the most freqent item is at the start of the result list. 

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

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
