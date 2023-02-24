# Bipartition Graph

## Problem Statement

For this exercise, create a function `possible_bipartition` which takes in an adjacency list representing a graph of puppies, `dislikes`, to determine if the puppies can be divided into two groups where no two puppies that are known for fighting each other are in the same group.   

Given a set of N puppies, we would like to split them into two groups of any size to use two play areas.

Formally, if `dislikes[i] = [a, b]`, it means puppies `i` is not allowed to put in the same group as puppies `a` or puppies `b`.

Dislike is mutual. If puppy `a` dislikes puppy `b`, puppy `b` also dislikes puppy `a`.

Return `True` if and only if it is possible to split the puppies into two groups where no fighting will occur. Otherwise, return `False`.

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

None of the pups who would fight with each other are placed in the same group.
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

There is no way to place all of the pups into two separate groups such that no pups would fight with each other. 

If we were to place Fido and Nala in Group 1, we could place Cooper in Group 2. Then, when we tried to place Spot in either
group, we would find that there's no where for him to be placed because he is disliked by a pup in both
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
* id: 52d7f6a8-f170-4c7b-bfb3-2474e6c065b2
* title: Ask Clarifying Questions
* topics: pse
##### !question

List three or more questions whose answers would clarify the problem statement.

For each question, provide an explanation which includes the effect your decision would have on how you would approach the problem.

##### !end-question

##### !explanation

Here are some example clarifying questions:

1. What should be returned for an empty graph?
2. Is it possible for the graph to be disconnected?

##### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->

### !challenge
* type: code-snippet
* language: python3.6
* id: 5b87969b-372d-40fa-abdb-040573105c95
* title: Write Unit Tests
* topics: pse
##### !question

1. Use the comments provided to write at least two example input/outputs:
    * Consider at least one nominal and one edge case.
    * What is the expected output for the given input?
    * You can use the examples provided in the prompt, or other examples.
2. Write unit tests for `possible_bipartition` for the nominal and edge cases you identified in the first step.

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
```

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: d0b1fa9d-27f8-4209-bcc0-1ca45b868b80
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `possible_bipartition` in enough detail that someone else could write the code. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. For example, 1. Handle invalid input, 2. Given valid input, perform the computation/solve the problem/etc.
* Your logical steps could take the form of a numbered list, pseudo code, or anywhere in between. What's important at this stage is to think through and outline the implementation before writing code.

##### !end-question

##### !placeholder

Write the logical steps here.

##### !end-placeholder

### !end-challenge
<!-- prettier-ignore-end -->
