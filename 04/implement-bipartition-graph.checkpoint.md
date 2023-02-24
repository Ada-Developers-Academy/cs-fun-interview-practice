# Implement Possible Graph Bipartition

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 5875e4c4-dab1-427e-935b-c5983b45bd92
* title: Possible Graph Bipartition
* points: 3
### !question
For this exercise, create a function `possible_bipartition` which takes in an adjacency list representing a graph of puppies, `dislikes`, to determine if the puppies can be divided into two groups where no two puppies that are known for fighting each other are in the same group.  

Given a set of N puppies, we would like to split them into two groups of any size to use two play areas.

Some puppies have a history of fighting with specific other puppies and shouldn't be put into the same play area.

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
### !end-question
### !placeholder

```python
def possible_bipartition(dislikes):
    """
    A function which takes in an adjacency list which represents a graph of puppies who dislike each other and
    returns True if the graph can be partitioned into two groups such that no two pups who dislike
    each other are placed in the same group.

    If the puppies cannot be partitioned into two groups, the function returns False.
  
    Parameters:
    dislikes (dict of string:string): An adjacency dictionary representing a graph of puppies
    who dislike each other.
  
    Returns:
    Boolean: True if the puppies can be partitioned into two groups where none of the pups want to fight each other.
    """
    pass
```

### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_example_1(self):
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

    def test_example_2(self):
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

    def test_example_3(self):
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

    def test_will_return_true_for_a_graph_which_can_be_bipartitioned(self):
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

    def test_will_return_false_for_graph_which_cannot_be_bipartitioned(self):
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


    def test_will_return_true_for_empty_graph(self):
        self.assertTrue(possible_bipartition({}))
    
    def test_will_return_false_for_another_graph_which_cannot_be_bipartitioned(self):
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

    def test_multiple_dogs_at_beginning_dont_dislike_any_others(self):
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


    def test_multiple_dogs_in_middle_dont_dislike_any_others(self):
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

    def test_will_return_false_for_disconnected_graph_which_cannot_be_bipartitioned(self):
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
* id: b70d559e-2a87-4010-8e02-9ee658de9402
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
* id: 06376c61-2207-4bdb-94a3-39aa38705c57
* title: Space Complexity of Solution
* points: 1 

##### !question

What is the space complexity of your solution? Please define and explain your variables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->