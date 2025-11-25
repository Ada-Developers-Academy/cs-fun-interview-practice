# Number of Provinces

Create a function `num_provinces` that takes in an adjacency matrix representing a graph of cities, `is_connected`. The function should return the total number of provinces represented by `is_connected` .

`is_connected` is a graph with `N` nodes. Each node represents a city. Two cities `a` and `b` belong to a single _province_ if there is a possible path from `a` to `b` or vice versa.

Paths from `a` to `b` through intermediary cities such as a city `c` are valid paths. 

`is_connected[i][j] = 1` indicates that cities `i` and `j` are directly connected. Otherwise `is_connected[i][j] = 0`, even if there is an indirect path from `i` to `j`. 

Return the total number of provinces in `is_connected`. 

*Adapted from: [https://leetcode.com/problems/number-of-provinces](https://leetcode.com/problems/number-of-provinces)*

## Example 1
![A graph consisting of three nodes. Two of the three nodes share a single edge. The third node is disconnected from the other two.](../images/number_of_provinces_example_1.png)
*Input:*
```py
is_connected = [
    [0, 0, 1],
    [0, 0, 0],
    [1, 0, 0]
]
```
*Output:* `2`

## Example 2
![A graph consisting of three nodes. All three nodes are connected to each other.](../images/number_of_provinces_example_2.png)
*Input:*
```py
is_connected = [
    [0, 1, 1],
    [1, 0, 1],
    [1, 1, 0]
]
```
*Output*: `1`

## Example 3
![A graph consisting of three nodes. None of the nodes are connected to any other nodes.](../images/number_of_provinces_example_3.png)
*Input:*
```py
is_connected = [
    [0, 0, 0],
    [0, 0, 0],
    [0, 0, 0]
]
```
*Output:* `3`

## Prompts

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 660061e6-a250-4f94-8b51-dccd6c402075
* title: Ask Clarifying Questions
* topics: pse
##### !question

List three or more questions whose answers would clarify the problem statement.

For each question, provide an explanation which includes the effect your decision would have on how you would approach the problem.

##### !end-question
##### !explanation

Here are some example clarifying questions:

1. What should be returned for an empty graph?
2. Will the graph edges always be undirected?
3. Will there be self loops in the graph?
4. What should we do in case of a malformed graph structure? *(Think about how the graph could be malformed and what the effects on your approach might be.)*

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: b2d7f05b-b227-4515-8c67-417eef373847
* title: Write Unit Tests
* topics: pse
##### !question

1. Use the comments provided to write at least two example input/outputs:
    * Consider at least one nominal and one edge case.
    * What is the expected output for the given input?
    * You can use the examples provided in the prompt, or other examples.
2. Write unit tests for `num_provinces` for the nominal and edge cases you identified in the first step.

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
def test_returns_two_for_two_provinces():
    # Arrange
    is_connected = [[0, 0, 1], [0, 0, 0], [1, 0, 0]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 2

def test_returns_zero_for_empty_connections():
    # Arrange
    is_connected = []

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 0
```

##### !end-explanation
##### !hint
Try drawing out some sample graphs and translating them into an adjacency matrix if coming up with an adjacency matrix representing a graph is challenging.
##### !end-hint
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 647614a1-13b7-42f8-aaa4-4487184cac43
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `num_provinces` in enough detail that someone else could write the code. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. For example, 1. Handle invalid input, 2. Given valid input, perform the computation/solve the problem/etc.
* Your logical steps could take the form of a numbered list, pseudo code, or anywhere in between. What's important at this stage is to think through and outline the implementation before writing code.

##### !end-question

##### !placeholder

Write the logical steps here.

##### !end-placeholder

##### !hint
When thinking about whether two cities are in the same province, do we need to consider all pairwise cities, or is there another way for us to find all of the cities in a particular province?
##### !end-hint

##### !hint
If we assume only undirected graphs, what would it mean when we have have visited everything reachable from some arbitrary starting node?
##### !end-hint

##### !hint
When starting from a node, how do we know whether or not the city is part of a province we've already counted?

The next hint presents the steps for one possible approach.
##### !end-hint

##### !hint
1. Initialize a list to keep track of the nodes we have visited.
2. Iterate over the nodes in the graph (in the adjacency matrix order, irrespective of edge connections).
3. For each node, if we have not yet visited it, increment the province count and perform a search (either depth-first or breadth-first could work) to find all of the nodes reachable from the current node.
4. For each node we find in the search, mark it as being visited.
5. Upon completing each search, we will have found all of the cities in a province. Continue iterating over the nodes in the graph.
6. Once we have iterated over all of the nodes in the graph, we will have found all of the provinces, so return the province count.
##### !end-hint

### !end-challenge
<!-- prettier-ignore-end -->
