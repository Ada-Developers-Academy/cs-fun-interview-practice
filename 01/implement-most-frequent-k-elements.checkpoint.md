# Most Frequent K Elements

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: c371a9d2-49b1-417b-abc4-3765e5cade18
* title: Most Frequent K Elements
* points: 3
### !question

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

### !end-question
### !placeholder

```python
def most_frequent_k_elements(arr,k):
    """
    A function that returns the k most frequent elements in a given array.
  
    Parameters:
    arr (array): a non-empty array of integers
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
    def test_most_frequent_k_elements_nominal(self):
        # Arrange
        arr = [1,1,1,2,2,3]
        k = 2

        # Act
        result = most_frequent_k_elements(arr, k)

        # Assert
        self.assertEqual(set(result), set([1,2]))

    def test_most_frequent_k_elements_single_arr(self):
        # Arrange
        arr = [1]
        k = 1 


        # Act
        result = most_frequent_k_elements(arr, k)

        # Act
        self.assertEqual(set(result), set([1]))

    def test_most_frequent_k_elements_negative_number_case(self):
        # Arrange
        arr = [-1,-1,-1,-2,-5,-5,3,3,3,3,4]
        k = 3

        # Act
        result = most_frequent_k_elements(arr, k)

        # Assert
        self.assertEqual(set(result), set([3,-1,-5]))



```
### !end-tests
### !explanation

An example of a working implementation:

```python
# Time Complexity: O(N log(N)) where N is the size of the array
# Space Complexity: O(N) where N is the size of the array
def most_frequent_k_elements(arr, k):
    if len(arr) == 1: return [arr[0]]
    
    frequency_map = {}
    uniques = []
    # looping through array and creating hash where key value pairs are unique integers and number of occurrences
    for num in arr:
        if num in frequency_map:
            frequency_map[num] += 1
            
        else:
            frequency_map[num] = 1
            uniques.append(num)
            
    # Sorted has a time complexity of O(N log(N)) takes an iterable, function to decide the order, and reverse to decide descending/ascending
    result = sorted(uniques, key=lambda num: frequency_map[num], reverse=True)

    # use k to return the k most frequent integers
    return result[:k]
```
### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<br>
<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
    def test_most_frequent_k_elements_nominal():
        # Arrange
        arr = [1,1,1,2,2,3]
        k = 2

        # Act
        result = most_frequent_k_elements(arr, k)

        # Assert
        assert set(result) == set([1,2])

    def test_most_frequent_k_elements_single_arr():
        # Arrange
        arr = [1]
        k = 1 


        # Act
        result = most_frequent_k_elements(arr, k)

        # Act
        assert result == [1]

    def test_most_frequent_k_elements_negative_number_case():
        # Arrange
        arr = [-1,-1,-1,-2,-5,-5,3,3,3,3,4]
        k = 3

        # Act
        result = most_frequent_k_elements(arr, k)

        # Assert
        assert set(result) == set([3,-1,-5])
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