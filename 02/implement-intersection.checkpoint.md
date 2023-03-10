# Implement Linked List Intersection

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 2aba725d-bef8-4175-b73b-286c91373494
* title: Linked List Intersection
* points: 3
### !question

Given the heads of two singly linked-lists `head_a` and `head_b`, return the node at which the two lists intersect. If the two linked lists do not intersect, the function should return `None`.

For example, the following two linked lists begin to intersect at the node 8:

![intersecting linked lists example 1](../images/intersection_linked_list_example_1.png)

The following two linked lists do _not_ intersect at all.

![intersecting linked lists example 2](../images/intersection_linked_list_example_2.png)

For this problem, we want to focus on the nodes themselves and not necessarily the *value* inside of the node.

For example, while the following linked lists have tails that share the same values, they are not considered to intersect because the nodes of the linked lists are not the same nodes in memory.

![intersecting linked lists example 3](../images/intersection_linked_list_example_3.png)

There are no cycles anywhere in the linked list structures. Assume any intersection includes the tails of each list.

The linked lists must retain their original structure after the function returns.

### !end-question
### !placeholder

```python
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None

def intersection_node(head_a, head_b):
    """
    Given the heads of two singly linked-lists `head_a` and `head_b`, 
    return the node at which the two lists intersect.
  
    Parameters:
    head_a (Node): head node of list A
    head_b (Node): head node of list B
  
    Returns:
    Node: the node at which list A and list B intersect, 
    or None if they do not intersect.
    """
    pass
```

### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_will_return_intersection_for_lists_of_same_length(self):
        # Arrange
        node_d = Node("D")
        node_e = Node("E")
        node_f = Node("F")

        node_x = Node("X")
        node_y = Node("Y")
        node_z = Node("Z")

        node_one = Node("1")
        node_two = Node("2")
        node_three = Node("3")
        node_one.next = node_two
        node_two.next = node_three

        # List A: ["D", "E", "F", "1", "2", "3"]
        node_d.next = node_e
        node_e.next = node_f
        node_f.next = node_one

        # List B: ["X", "Y", "Z", "1", "2", "3"]
        node_x.next = node_y
        node_y.next = node_z
        node_z.next = node_one

        head_a = node_d
        head_b = node_x

        # Act
        answer = intersection_node(head_a, head_b)

        # Assert
        self.assertEqual(answer, node_one)

    def test_will_return_intersection_with_lists_of_differing_lengths(self):
        # Arrange
        node_d = Node("D")
        node_e = Node("E")
        node_f = Node("F")

        node_x = Node("X")

        node_one = Node("1")
        node_two = Node("2")
        node_three = Node("3")
        node_one.next = node_two
        node_two.next = node_three

        # List A: ["D", "E", "F", "1", "2", "3"]
        node_d.next = node_e
        node_e.next = node_f
        node_f.next = node_one

        # List B: ["X", "1", "2", "3"]
        node_x.next = node_one

        head_a = node_d
        head_b = node_x

        # Act
        answer = intersection_node(head_a, head_b)

        # Assert
        self.assertEqual(answer, node_one)

    def test_will_return_none_with_one_empty_list(self):
        # Arrange
        node_d = Node("D")
        node_e = Node("E")
        node_f = Node("F")

        # List A: ["D", "E", "F"]
        node_d.next = node_e
        node_e.next = node_f

        # List B: [] <-- empty list

        # Act
        answer = intersection_node(node_d, None)

        # Assert
        self.assertEqual(answer, None)

    def test_will_return_none_when_no_intersection(self):
        # Arrange
        node_d = Node("D")
        node_e = Node("E")
        node_f = Node("F")

        node_x = Node("X")
        node_y = Node("Y")
        node_z = Node("Z")

        # List A: ["D", "E", "F"]
        node_d.next = node_e
        node_e.next = node_f

        # List B: ["X", "Y", "Z"]
        node_x.next = node_y
        node_y.next = node_z

        head_a = node_d
        head_b = node_x

        # Act
        answer = intersection_node(head_a, head_b)

        # Assert
        self.assertEqual(answer, None)

    def test_will_return_none_for_two_empty_lists(self):
        # Arrange

        # List A: [] <-- empty list
        # List B: [] <-- empty list

        # Act
        answer = intersection_node(None, None)

        # Assert
        self.assertEqual(answer, None)

    def test_will_return_none_for_tails_with_same_values_but_different_memory_location(self):
        # Arrange
        node_d = Node("D")
        node_e1 = Node("E")
        node_f1 = Node("F")

        node_x = Node("X")
        node_e2 = Node("E")
        node_f2 = Node("F")

        # List A: ["D", "E", "F"]
        node_d.next = node_e1
        node_e1.next = node_f1
        
        # List B:
        node_x.next = node_e2
        node_e2.next = node_f2

        # Act
        answer = intersection_node(node_d, node_x)

        # Assert
        self.assertEqual(answer, None)
```
### !end-tests
### !explanation

An example of a working implementation:

```python
# Time complexity: O(A + B) where A is the size of list A and B is the size of list B. The loop will traverse through the lists at most twice.
# Space complexity: O(1) as the added space needed does not scale with the input data (two additional pointers)
def intersection_node(head_a, head_b):
    # assign l1 and l2 to point to the heads of list A and list B
    l1, l2 = head_a, head_b
    # while l1 and l2 do not reference the same node or None
    while l1 != l2:
        # once we've traversed through an entire list, we will set the pointer for the smaller list to the beginning of the other list
        # on the next iteration of the lists:
        #   if there is NO intersection, both pointers will reach None at the same time.
        #   if there is an intersection, both pointers will reach the intersecting Node at the same time.

        # set l1 to be l1.next if l1 is not None, otherwise set l1 to be the head of list B 
        l1 = l1.next if l1 else head_b
        # likewise, set l2 to be l2.next if l2 is not None, otherwise set l2 to be the head of list A
        l2 = l2.next if l2 else head_a
    return l1
```
### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<br>
<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
def test_will_return_intersection_for_lists_of_same_length(self):
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    node_x = Node("X")
    node_y = Node("Y")
    node_z = Node("Z")

    node_one = Node("1")
    node_two = Node("2")
    node_three = Node("3")
    node_one.next = node_two
    node_two.next = node_three

    # List A: ["D", "E", "F", "1", "2", "3"]
    node_d.next = node_e
    node_e.next = node_f
    node_f.next = node_one

    # List B: ["X", "Y", "Z", "1", "2", "3"]
    node_x.next = node_y
    node_y.next = node_z
    node_z.next = node_one

    head_a = node_d
    head_b = node_x

    # Act
    answer = intersection_node(head_a, head_b)

    # Assert
    self.assertEqual(answer, node_one)

def test_will_return_intersection_with_lists_of_differing_lengths(self):
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    node_x = Node("X")

    node_one = Node("1")
    node_two = Node("2")
    node_three = Node("3")
    node_one.next = node_two
    node_two.next = node_three

    # List A: ["D", "E", "F", "1", "2", "3"]
    node_d.next = node_e
    node_e.next = node_f
    node_f.next = node_one

    # List B: ["X", "1", "2", "3"]
    node_x.next = node_one

    head_a = node_d
    head_b = node_x

    # Act
    answer = intersection_node(head_a, head_b)

    # Assert
    self.assertEqual(answer, node_one)

def test_will_return_none_with_one_empty_list(self):
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    # List A: ["D", "E", "F"]
    node_d.next = node_e
    node_e.next = node_f

    # List B: [] <-- empty list

    # Act
    answer = intersection_node(node_d, None)

    # Assert
    self.assertEqual(answer, None)

def test_will_return_none_when_no_intersection(self):
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    node_x = Node("X")
    node_y = Node("Y")
    node_z = Node("Z")

    # List A: ["D", "E", "F"]
    node_d.next = node_e
    node_e.next = node_f

    # List B: ["X", "Y", "Z"]
    node_x.next = node_y
    node_y.next = node_z

    head_a = node_d
    head_b = node_x

    # Act
    answer = intersection_node(head_a, head_b)

    # Assert
    self.assertEqual(answer, None)

def test_will_return_none_for_two_empty_lists(self):
    # Arrange

    # List A: [] <-- empty list
    # List B: [] <-- empty list

    # Act
    answer = intersection_node(None, None)

    # Assert
    self.assertEqual(answer, None)

def test_will_return_none_for_tails_with_same_values_but_different_memory_location(self):
    # Arrange
    node_d = Node("D")
    node_e1 = Node("E")
    node_f1 = Node("F")

    node_x = Node("X")
    node_e2 = Node("E")
    node_f2 = Node("F")

    # List A: ["D", "E", "F"]
    node_d.next = node_e1
    node_e1.next = node_f1
    
    # List B:
    node_x.next = node_e2
    node_e2.next = node_f2

    # Act
    answer = intersection_node(node_d, node_x)

    # Assert
    self.assertEqual(answer, None)
```
</details>

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: d0c65caa-97b1-4ffb-8038-33303a412a8f
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
* id: efb51781-bbe5-4a86-9645-6ae1ce49f9f6
* title: Space Complexity of Solution
* points: 1 

##### !question

What is the space complexity of your solution? Please define and explain your variables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->