# Linked List Intersection

## Problem Statement

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

## Prompts

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: c273469f-8ac2-4c98-a876-521b74d6e7e0
* title: Ask Clarifying Questions
* topics: pse
##### !question

List three or more questions whose answers would clarify the problem statement.

For each question, provide an explanation which includes the effect your decision would have on how you would approach the problem.

##### !end-question

##### !explanation

Here are some example clarifying questions:

1. What should be returned if one or both lists are empty?
2. What kind of data is stored in the nodes?

##### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->

### !challenge
* type: code-snippet
* language: python3.6
* id: c52a82cc-4062-405a-b475-0f269b8494c0
* title: Write Unit Tests
* topics: pse
##### !question

1. Use the comments provided to write at least two example input/outputs:
    * Consider at least one nominal and one edge case.
    * What is the expected output for the given input?
    * You can use the examples provided in the prompt, or other examples.
2. Write unit tests for `intersection_node` for the nominal and edge cases you identified in the first step.

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
def test_will_return_intersection_for_lists_of_same_length():
    # Arrange
    node_d = Node("D")

    node_x = Node("X")

    node_one = Node("1")
    node_two = Node("2")
    node_three = Node("3")
    node_one.next = node_two
    node_two.next = node_three

    # List A: D -> 1 -> 2 -> 3
    node_d.next = node_one

    # List B: X -> 1 -> 2 -> 3
    node_x.next = node_one

    head_a = node_d
    head_b = node_x

    # Act
    answer = intersection_node(head_a, head_b)

    # Assert
    assert answer == node_one

def test_will_return_none_with_one_empty_list():
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    # List A: D -> E -> F
    node_d.next = node_e
    node_e.next = node_f

    # List B: None, the list is empty

    # Act
    answer = intersection_node(node_d, None)

    # Assert
    assert answer is None
```

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 10510a7b-e915-42cc-8cea-26555f96c34d
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `intersection_node` in enough detail that someone else could write the code. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. For example, 1. Handle invalid input, 2. Given valid input, perform the computation/solve the problem/etc.
* Your logical steps could take the form of a numbered list, pseudo code, or anywhere in between. What's important at this stage is to think through and outline the implementation before writing code.

##### !end-question

##### !placeholder

Write the logical steps here.

##### !end-placeholder

### !end-challenge
<!-- prettier-ignore-end -->
