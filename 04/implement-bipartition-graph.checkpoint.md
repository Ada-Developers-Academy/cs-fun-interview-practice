# Implement Possible Graph Bipartition

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: b2640327-8294-4e0c-a982-a4edd3aa095f
* title: Possible Graph Bipartition
* points: 3
### !question

### !end-question
### !placeholder

```python
def possible_bipartition(dislikes):
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
        self.assertTrue(answer)

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
        self.assertFalse(answer)

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
        self.assertFalse(answer)

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
        self.assertTrue(answer)

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
        self.assertFalse(answer)


    def test_will_return_true_for_empty_graph():
        self.assertTrue(possible_bipartition({}))
    
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
        self.assertFalse(answer)

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
        self.assertTrue(answer)


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
        self.assertTrue(answer)

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
        self.assertFalse(answer)
```
### !end-tests
### !explanation

An example of a working implementation:

```python
COLORS = ["red", "green"]

def dfs(dislikes, current_node, painted_graph, current_color):
    neighbors = dislikes[current_node]
    next_color = (current_color + 1) % len(COLORS)

    for neighbor in neighbors:
        color = painted_graph.get(neighbor)

        if not color:
            painted_graph[neighbor] = COLORS[next_color]
            if not dfs(dislikes=dislikes, current_node=neighbor, painted_graph=painted_graph, current_color=next_color):
                return False
        elif color != COLORS[next_color]:
            return False
    
    return True
    

def possible_bipartition(dislikes):
    painted_graph = {}
    current_color = 0

    for node in dislikes.keys():
        neighbors = dislikes[node]
        if not painted_graph.get(node):
            painted_graph[node] = COLORS[current_color]

            if not dfs(dislikes=dislikes, current_node=node, painted_graph=painted_graph, current_color=current_color):
                return False
    return True
```
### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

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