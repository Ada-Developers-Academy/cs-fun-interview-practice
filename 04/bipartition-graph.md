# Bipartition Graph

## Problem Statement

In this exercise you will take in an adjacency list and determine if you can divide dogs into two groups where no two dogs that are known for fighting each other are in the same group.  

Given a set of N puppies, we would like to split them into two groups of any size to use two play areas.

Some dogs have a history of fighting with specific other dogs and shouldn't be put into the same play area.

Formally, if `dislikes[i] = [a, b]`, it means dog `i` is not allowed to put in the same group as dog `a` or dog `b`.

Dislike is mutual. If dog `a` dislikes dog `b`, dog `b` also dislikes dog `a`.

Return `True` if and only if it is possible to split the dogs into two groups where no fighting will occur. Otherwise, return `False`.

**Example 1**
```
Input:
dislikes = { 
    "Fido": [],
    "Nala": ["Cooper", "Spot"],
    "Cooper": ["Nala", "Bruno"],
    "Spot": ["Nala"],
    "Bruno": ["Cooper"]
}

Output: True

Explanation:
Fido can be placed in Group 1.
Nala can be placed in Group 1.
Cooper can be placed in Group 2.
Spot can be placed in Group 2.
Bruno can be placed in Group 1.

None of the dogs who would fight with each other are placed in the same group.
```

**Example 2:**
```
Input:
dislikes = {
    "Fido": [],
    "Nala": ["Cooper", "Spot"],
    "Cooper": ["Nala", "Spot"],
    "Spot": ["Nala", "Cooper"]
}

Output: False

There is no way to place all of the dogs into two separate groups such that no dogs would fight with each other. 

If we were to place Fido and Nala in Group 1, we could place Cooper in Group 2. Then, when we tried to place Spot in either
group, we would find that there's no where for him to be placed because he is disliked by a dog in both
Group 1 and Group 2.
```

<br>
<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
def test_example_1():
    # Arrange
    dislikes = {
      "Fido": [],
      "Rufus": ["James", "Alfie"],
      "James": ["Rufus", "T-Bone"],
      "Alfie": ["Rufus"],
      "T-Bone": ["James"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert answer

def test_example_2():
    dislikes = {
      "Fido": [],
      "Rufus": ["James", "Alfie"],
      "James": ["Rufus", "Alfie"],
      "Alfie": ["Rufus", "James"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert not answer

def test_example_3():
    # Arrange
    dislikes = {
      "Fido": [],
      "Rufus": ["James", "Scruffy"],
      "James": ["Rufus", "Alfie"],
      "Alfie": ["T-Bone", "James"],
      "T-Bone": ["Alfie", "Scruffy"],
      "Scruffy": ["Rufus", "T-Bone"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert not answer

def test_will_return_true_for_a_graph_which_can_be_bipartitioned():
    # Arrange
    dislikes = {
      "Fido": ["Alfie", "Bruno"],
      "Rufus": ["James", "Scruffy"],
      "James": ["Rufus", "Alfie"],
      "Alfie": ["Fido", "James"],
      "T-Bone": ["Scruffy"],
      "Scruffy": ["Rufus", "T-Bone"],
      "Bruno": ["Fido"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert answer

def test_will_return_false_for_graph_which_cannot_be_bipartitioned():
    # Arrange
    dislikes = {
      "Fido": ["Alfie", "Bruno"],
      "Rufus": ["James", "Scruffy"],
      "James": ["Rufus", "Alfie"],
      "Alfie": ["Fido", "James", "T-Bone"],
      "T-Bone": ["Alfie", "Scruffy"],
      "Scruffy": ["Rufus", "T-Bone"],
      "Bruno": ["Fido"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert not answer


def test_will_return_true_for_empty_graph():
    assert possible_bipartition({})
  
def test_will_return_false_for_another_graph_which_cannot_be_bipartitioned():
    # Arrange
    dislikes = {
      "Fido": ["Alfie", "Bruno"],
      "Rufus": ["James", "Scruffy"],
      "James": ["Rufus", "Alfie"],
      "Alfie": ["Fido", "James", "T-Bone"],
      "T-Bone": ["Alfie", "Scruffy"],
      "Scruffy": ["Rufus", "T-Bone"],
      "Bruno": ["Fido"],
      "Spot": ["Nala"],
      "Nala": ["Spot"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert not answer

def test_multiple_dogs_at_beginning_dont_dislike_any_others():
  # Arrange
    dislikes = {
      "Fido": [],
      "Rufus": [],
      "James": [],
      "Alfie": ["T-Bone"],
      "T-Bone": ["Alfie", "Scruffy"],
      "Scruffy": ["T-Bone"],
      "Bruno": ["Nala"],
      "Spot": ["Nala"],
      "Nala": ["Bruno", "Spot"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert answer


def test_multiple_dogs_in_middle_dont_dislike_any_others():
    # Arrange
    dislikes = {
      "Fido": ["Alfie"],
      "Rufus": ["James", "Scruffy"],
      "James": ["Rufus", "Alfie"],
      "Alfie": ["Fido", "James"],
      "T-Bone": [],
      "Scruffy": ["Rufus"],
      "Bruno": [],
      "Spot": ["Nala"],
      "Nala": ["Spot"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert answer

def test_will_return_false_for_disconnected_graph_which_cannot_be_bipartitioned():
    # Arrange
    dislikes = {
      "Ralph": ["Tony"],
      "Tony": ["Ralph"],
      "Fido": ["Alfie", "Bruno"],
      "Rufus": ["James", "Scruffy"],
      "James": ["Rufus", "Alfie"],
      "Alfie": ["Fido", "James", "T-Bone"],
      "T-Bone": ["Alfie", "Scruffy"],
      "Scruffy": ["Rufus", "T-Bone"],
      "Bruno": ["Fido"]
    }

    # Act
    answer = possible_bipartition(dislikes)

    # Assert
    assert not answer
```

</details>

## Prompts

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: d0a2663c-8528-41b6-8e21-333812b18876
* title: Ask Clarifying Questions
* topics: pse
##### !question

List three or more questions whose answers would clarify the problem statement.

For each question, provide an explanation which includes the effect your decision would have on how you would approach the problem.

##### !end-question

##### !explanation

Here are some example clarifying questions:

1. What kind of data is stored in the Tree Nodes?
2. Is the array guaranteed to be non-empty?

##### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->

### !challenge
* type: code-snippet
* language: python3.6
* id: 275e4d6e-accf-4dd3-89c4-9f23729615e8
* title: Write Unit Tests
* topics: pse
##### !question

1. Use the comments provided to write at least two example input/outputs:
    * Consider at least one nominal and one edge case.
    * What is the expected output for the given input?
    * You can use the examples provided in the prompt, or other examples.
2. Write unit tests for `arr_to_bst` for the nominal and edge cases you identified in the first step.

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
def test_will_return_balanced_bst_for_odd_lengthed_list(self):
        # Arrange
        arr = [5, 10, 15, 20, 25, 30, 35, 40, 45]

        # Act
        result = arr_to_bst(arr)

        # Assert
        self.assertEqual(result.val, 25)
        self.assertTrue(is_bst(result))
        self.assertTrue(is_balanced_tree(result))

def test_will_return_none_for_empty_list(self):
        # Arrange
        arr = []

        # Act
        result = arr_to_bst(arr)

        # Assert
        self.assertEqual(result, None)
```

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: eeadcbbb-7fda-4fac-8ef2-309bf97d7245
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `arr_to_bst` in enough detail that someone else could write the code. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. For example, 1. Handle invalid input, 2. Given valid input, perform the computation/solve the problem/etc.
* Your logical steps could take the form of a numbered list, pseudo code, or anywhere in between. What's important at this stage is to think through and outline the implementation before writing code.

##### !end-question

##### !placeholder

Write the logical steps here.

##### !end-placeholder

### !end-challenge
<!-- prettier-ignore-end -->