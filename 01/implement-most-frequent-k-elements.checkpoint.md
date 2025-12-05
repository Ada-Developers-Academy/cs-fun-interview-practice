# Most Frequent K Elements

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: c371a9d2-49b1-417b-abc4-3765e5cade18
* title: Most Frequent K Elements
* points: 3
### !question

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

### !end-question
### !placeholder

```python
def most_frequent_k_elements(numbers, k):
    """
    A function that returns the k most frequent elements in a given array.
  
    Parameters:
    numbers (array): a non-empty array of integers
    k (int): number of most frequent integers to return 
  
    Returns:
    array[int]: 1D array that that returns the k most frequent elements
    """
    pass
```

### !end-placeholder
### !tests

```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_most_frequent_k_elements_sorted_input_succeeds(self):
        # Arrange
        numbers = [1, 1, 1, 2, 2, 3]
        k = 2

        # Act
        result = most_frequent_k_elements(numbers, k)

        # Assert
        self.assertEqual(set(result), set([1, 2]))


    def test_most_frequent_k_elements_single_element_input_succeeds(self):
        # Arrange
        numbers = [1]
        k = 1 


        # Act
        result = most_frequent_k_elements(numbers, k)

        # Act
        self.assertEqual(set(result), set([1]))


    def test_most_frequent_k_elements_negatives_in_input_succeeds(self):
        # Arrange
        numbers = [-1, -1, -1, -2, -5, -5, 3, 3, 3, 3, 4]
        k = 3

        # Act
        result = most_frequent_k_elements(numbers, k)

        # Assert
        self.assertEqual(set(result), set([3, -1, -5]))
```
### !end-tests
### !explanation

An example of a working implementation:

```python
# Time Complexity: O(N log(N)) where N is the size of the array
# Space Complexity: O(N) where N is the size of the array
def most_frequent_k_elements(numbers, k):
    # Edge case: 
    # If there is only 1 element in `numbers, there is no need to iterate
    # we can return the single element in a new list as the result
    if len(numbers) == 1: 
        return [numbers[0]]
    
    frequency_map = {}
    # loop through input array and create a hashmap 
    # where key value pairs are unique integers and their number of occurrences
    for number in numbers:
        if number in frequency_map:
            frequency_map[number] += 1
        else:
            frequency_map[number] = 1
    
    unique_numbers = list(frequency_map.keys())
    # Sorted has a time complexity of O(N log(N)) 
    # It takes an iterable, a function to decide the order, 
    # and `reverse` to decide descending/ascending
    sorted_numbers = sorted(
                unique_numbers, 
                key=lambda num: frequency_map[num], 
                reverse=True
            )

    # Create a list slice of length k to return the k most frequent integers
    return sorted_numbers[:k]
```
### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<br>
<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
    def test_most_frequent_k_elements_sorted_input_succeeds():
        # Arrange
        numbers = [1, 1, 1, 2, 2, 3]
        k = 2

        # Act
        result = most_frequent_k_elements(numbers, k)

        # Assert
        assert set(result) == set([1,2])


    def test_most_frequent_k_elements_single_element_input_succeeds():
        # Arrange
        numbers = [1]
        k = 1 


        # Act
        result = most_frequent_k_elements(numbers, k)

        # Act
        assert result == [1]


    def test_most_frequent_k_elements_negatives_in_input_succeeds():
        # Arrange
        numbers = [-1, -1, -1, -2, -5, -5, 3, 3, 3, 3, 4]
        k = 3

        # Act
        result = most_frequent_k_elements(numbers, k)

        # Assert
        assert set(result) == set([3,-1,-5])
```
</details>

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 2cf7eca9-1f15-47a3-a217-08dfdebbb71f
* title: Time Complexity of Solution
* points: 1
##### !question

What is the time complexity of your solution? 
- Please define your variables and explain what parts of the code contributes to the complexity stated.

##### !end-question
##### !placeholder

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: c48781b8-caf9-460a-af73-bf6e0b54585c
* title: Space Complexity of Solution
* points: 1 
##### !question

What is the space complexity of your solution?
- Please define your variables and explain what parts of the code contributes to the complexity stated.

##### !end-question
##### !placeholder

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
