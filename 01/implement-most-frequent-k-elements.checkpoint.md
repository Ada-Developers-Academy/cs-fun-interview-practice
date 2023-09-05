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
def most_frequent_k_elements(num_rows):
    """
    A function that returns the first num_rows of Pascal's triangle.
  
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
    def test_most_k_frequent_elements_nominal(self):
        # Arrange
        arr = [1,1,1,2,2,3]
        k = 2

        # Act
        result = most_frequents_k_elements(arr, k)

        # Assert
        self.assertEqual(result, [1,2])

    def test_pascals_big_number(self):
        # Arrange
        arr = [1]
        k = 1 


        # Act
        result = most_frequent_k_elements(arr, k)

        # Act
        self.assertEqual(result, [1])

    def test_pascals_negative_number_case(self):
        # Arrange
        arr = [-1,-1,-1,-2,-5,-5,3,3,3,3,4]
        k = 3

        # Act
        result = most_frequent_k_elements(arr, k)

        # Assert
        self.assertEqual(result, [3,-1,-5])

    def test_pascals_unordered_numbers_case(self):
        # Arrange
        arr = [1,2,1,5,1,5,]
        k = 2

        # Act
        result = most_frequent_k_elements(arr, k)

        # Assert
        self.assertEqual(result, [1,5])



```
### !end-tests
### !explanation

An example of a working implementation:

```python
# Time complexity: O(N + (K - 1)^2) where N is length of the array and K is the number of unique integers.
# Space complexity: O(N + K) where N is length of the array and K is the number of unique integers.
def top_k_frequent_elements(arr, k):
    # returns arr if the length of the given array 1
    if len(arr) == 1: return arr
    
    hash_table = {}
    result = []

    #looping through array and creating hash where key value pairs are unique integers and number of occurences
    for num in arr:
        if hash_table.get(num, False):
            hash_table[num] += 1
            
        else:
            hash_table[num] = 1
            # building a list of unique integers seen
            result.append(num)
            
    i = 0
    # loops through unique integers ordering them by descedent based on their paired values from the hash table
    while i < len(result) - 1:
        for j in range(len(result) - 1):
            if hash_table[result[j]] < hash_table[result[j+1]]:
                result[j], result[j+1] = result[j+1], result[j]
        i += 1

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
    def test_most_k_frequent_elements_nominal(self):
        # Arrange
        arr = [1,1,1,2,2,3]
        k = 2

        # Act
        result = most_frequents_k_elements(arr, k)

        # Assert
        self.assertEqual(result, [1,2])

    def test_pascals_big_number(self):
        # Arrange
        arr = [1]
        k = 1 


        # Act
        result = most_frequent_k_elements(arr, k)

        # Act
        self.assertEqual(result, [1])

    def test_pascals_negative_number_case(self):
        # Arrange
        arr = [-1,-1,-1,-2,-5,-5,3,3,3,3,4]
        k = 3

        # Act
        result = most_frequent_k_elements(arr, k)

        # Assert
        self.assertEqual(result, [3,-1,-5])

    def test_pascals_unordered_numbers_case(self):
        # Arrange
        arr = [1,2,1,5,1,5,]
        k = 2

        # Act
        result = most_frequent_k_elements(arr, k)

        # Assert
        self.assertEqual(result, [1,5])
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