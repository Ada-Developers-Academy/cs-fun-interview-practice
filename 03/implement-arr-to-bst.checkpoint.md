# Implement Array-to-BST

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 2aba725d-bef8-4175-b73b-286c91373494
* title: Array-to-BST
* points: 3
### !question

Given a sorted array of integers, `arr`, write a function to create a balanced Binary Search Tree from the contents of the array. Return the root of the Binary Search Tree.

Example:

`arr = [5, 10, 15, 20, 25, 30, 35, 40, 45]`

should result in a tree with the following root/height:

![Balanced Binary Search Tree](../images/balanced_bst.png)

Please note one is not required to implement a self-balancing Binary Search Tree in order to solve this exercise. 

It is recommended to break the problem down recursively by first setting the root of the Binary Search Tree to the middle element of the array.

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
        self.assertTrue(is_bst(result))
        self.assertTrue(is_balanced_tree(result))

    def test_will_return_balanced_bst_for_even_lengthed_list(self):
        # Arrange
        arr = [1, 3, 9, 27, 81, 243]

        # Act
        result = arr_to_bst(arr)

        # Assert
        self.assertTrue(is_bst(result))
        self.assertTrue(is_balanced_tree(result))

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
        self.assertTrue(is_bst(result))
        self.assertTrue(is_balanced_tree(result))

    def test_will_return_none_for_empty_list(self):
        # Arrange
        arr = []

        # Act
        result = arr_to_bst(arr)

        # Assert
        self.assertEqual(result, None)
        

    # Below are functions used to test if the given tree is a balanced Binary Search Tree.

    # Returns True if the BST provided is a valid BST.
    def is_bst(root):
        if root is None:
            return True

        left = root.left
        if left is not None and root.val <= left.val:
            return False

        right = root.right
        if right is not None and root.val >= right.val:
            return False

        return is_bst(left) and is_bst(right)

    # Returns the height of a tree
    def height(root):
        if root is None:
            return 0
        
        left_height = height(root.left)
        right_height = height(root.right)

        if left_height > right_height:
            return left_height + 1
        else:
            return right_height + 1


    # Returns True if a tree is balanced
    def is_balanced_tree(root):
        if root is None:
            return True

        left_height = height(root.left)
        right_height = height(root.right)

        if abs(left_height - right_height) > 1:
            return False

        left_check = is_balanced_tree(root.left)
        right_check = is_balanced_tree(root.right)

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

### !end-challenge
<!-- prettier-ignore-end -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: d0c65caa-97b1-4ffb-8038-33303a412a8f
* title: Time Complexity of Solution
* points: 1

##### !question

What is the time complexity of your solution? Remember to define your valuables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: efb51781-bbe5-4a86-9645-6ae1ce49f9f6
* title: Space Complexity of Solution
* points: 1 

##### !question

What is the space complexity of your solution? Remember to define your valuables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->