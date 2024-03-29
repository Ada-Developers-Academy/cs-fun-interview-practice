# Implement Array-to-BST

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: b2640327-8294-4e0c-a982-a4edd3aa095f
* title: Array-to-BST
* points: 3
### !question

Given a sorted array of unique integers, `arr`, write a function to create a balanced Binary Search Tree from the contents of the array. Return the root of the Binary Search Tree.

Example:

`arr = [5, 10, 15, 20, 25, 30, 35, 40, 45]`

should result in a tree with the following root/height:

![Balanced Binary Search Tree](../images/balanced_bst.png)

Please note the following:
* There will not be any duplicate elements in the array
* One is not required to implement a self-balancing Binary Search Tree in order to solve this exercise. For an extra challenge, consider why it is unnecessary!

### !end-question
### !placeholder

```python
class TreeNode:
    def __init__(self, value, left = None, right = None):
        self.val = value
        self.left = left
        self.right = right


def arr_to_bst(arr):
    """
    A function to create a balanced Binary Search Tree from the contents of an array.
  
    Parameters:
    arr (list[int]): A list of sorted integers
  
    Returns:
    TreeNode: The root of the Binary Search Tree created from the given array, arr.
    """
    pass
```

### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_will_return_balanced_bst_for_odd_lengthed_list(self):
        # Arrange
        arr = [5, 10, 15, 20, 25, 30, 35, 40, 45]

        # Act
        result = arr_to_bst(arr)

        # Assert
        self.assertEqual(result.val, 25)
        self.assertTrue(self.is_bst(result))
        self.assertTrue(self.is_balanced_tree(result))

    def test_will_return_balanced_bst_for_even_lengthed_list(self):
        # Arrange
        arr = [1, 3, 9, 27, 81, 243]

        # Act
        result = arr_to_bst(arr)

        # Assert
        self.assertTrue(self.is_bst(result))
        self.assertTrue(self.is_balanced_tree(result))

    def test_will_return_balanced_bst_for_long_list(self):
        # Arrange
        arr = []
        num = 0
        while num < 100:
            arr.append(num)
            num += 1

        # Act
        result = arr_to_bst(arr)

        # Assert
        self.assertTrue(self.is_bst(result))
        self.assertTrue(self.is_balanced_tree(result))

    def test_will_return_none_for_empty_list(self):
        # Arrange
        arr = []

        # Act
        result = arr_to_bst(arr)

        # Assert
        self.assertEqual(result, None)
        

    # Below are functions used to test if the given tree is a balanced Binary Search Tree.

    # Returns True if the BST provided is a valid BST.
    def is_bst(self, root):
        if root is None:
            return True

        left = root.left
        if left is not None and root.val <= left.val:
            return False

        right = root.right
        if right is not None and root.val >= right.val:
            return False

        return self.is_bst(left) and self.is_bst(right)

    # Returns the height of a tree
    def height(self, root):
        if root is None:
            return 0
        
        left_height = self.height(root.left)
        right_height = self.height(root.right)

        if left_height > right_height:
            return left_height + 1
        else:
            return right_height + 1


    # Returns True if a tree is balanced
    def is_balanced_tree(self, root):
        if root is None:
            return True

        left_height = self.height(root.left)
        right_height = self.height(root.right)

        if abs(left_height - right_height) > 1:
            return False

        left_check = self.is_balanced_tree(root.left)
        right_check = self.is_balanced_tree(root.right)

        return left_check and right_check
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def arr_to_bst(arr):
    if not arr:
        return None

    mid = (len(arr)) // 2

    root = TreeNode(arr[mid])
    root.left = arr_to_bst(arr[:mid])
    root.right = arr_to_bst(arr[mid + 1:])
    return root
```
### !end-explanation

### !hint
It is recommended to break the problem down recursively by first setting the root of the Binary Search Tree to the middle element of the array.
### !end-hint

### !end-challenge
<!-- prettier-ignore-end -->

<br>
<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
def test_will_return_balanced_bst_for_odd_lengthed_list(self):
    # Arrange
    arr = [5, 10, 15, 20, 25, 30, 35, 40, 45]

    # Act
    result = arr_to_bst(arr)

    # Assert
    self.assertEqual(result.val, 25)
    self.assertTrue(self.is_bst(result))
    self.assertTrue(self.is_balanced_tree(result))

def test_will_return_balanced_bst_for_even_lengthed_list(self):
    # Arrange
    arr = [1, 3, 9, 27, 81, 243]

    # Act
    result = arr_to_bst(arr)

    # Assert
    self.assertTrue(self.is_bst(result))
    self.assertTrue(self.is_balanced_tree(result))

def test_will_return_balanced_bst_for_long_list(self):
    # Arrange
    arr = []
    num = 0
    while num < 100:
        arr.append(num)
        num += 1

    # Act
    result = arr_to_bst(arr)

    # Assert
    self.assertTrue(self.is_bst(result))
    self.assertTrue(self.is_balanced_tree(result))

def test_will_return_none_for_empty_list(self):
    # Arrange
    arr = []

    # Act
    result = arr_to_bst(arr)

    # Assert
    self.assertEqual(result, None)
```

</details>

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: 4b02044b-128b-4df6-be11-2756c347b882
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
* id: 964cb04f-3bbd-4947-82ba-7662789960f0
* title: Space Complexity of Solution
* points: 1 

##### !question

What is the space complexity of your solution? Please define and explain your variables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->