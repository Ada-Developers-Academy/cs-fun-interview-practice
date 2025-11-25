# Implement Number of Provinces

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: ced162bb-b413-4e2e-ad5a-7da2c814e752
* title: Number of Provinces
* points: 3
### !question
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

### !end-question
### !placeholder

```python
def num_provinces(is_connected):
    """
    A function that takes in an adjacency list representing a graph of
    cities, and returns the total number of provinces represented by
    the graph.

    Parameters:
    is_connected (2D matrix of integers): An adjacency matrix
        representing a graph of cities and their connections. The value
        at is_connected[i][j] is 1 if cities i and j are connected, and
        0 otherwise.
  
    Returns:
    Integer: The total number of provinces represented by the graph.
    """

    pass
```

### !end-placeholder
### !tests

```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_num_provinces_two_provinces_returns_two(self):
        # Arrange
        is_connected = [[0, 0, 1], [0, 0, 0], [1, 0, 0]]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 2)


    def test_num_provinces_all_nodes_connected_returns_one(self):
        # Arrange
        is_connected = [[0, 1, 1], [1, 0, 1], [1, 1, 0]]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 1)

    def test_num_provinces_three_unconnected_nodes_returns_three(self):
        # Arrange
        is_connected = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 3)

    def test_num_provinces_input_with_no_rows_returns_zero(self):
        # Arrange
        is_connected = []

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 0)

    def test_num_provinces_one_node_graph_returns_one(self):
        # Arrange
        is_connected = [[0]]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 1)

    def test_num_provinces_graph_with_cycle_returns_two(self):
        # Arrange
        is_connected = [[0, 1, 1, 0], [1, 0, 1, 0], [1, 1, 0, 0], [0, 0, 0, 0]]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 2)

    def test_num_provinces_large_graph_with_four_provinces_returns_four(self):
        # Arrange
        is_connected = [
            [0, 1, 0, 0, 0, 0, 0, 0, 0, 0],
            [1, 0, 1, 0, 0, 0, 0, 0, 0, 0],
            [0, 1, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 1, 0, 1, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 1, 0, 0],
            [0, 0, 0, 0, 0, 0, 1, 0, 1, 0],
            [0, 0, 0, 0, 0, 0, 0, 1, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        ]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 4)

    def test_num_provinces_two_provinces_with_self_loops_returns_two(self):
        # Arrange
        is_connected = [[1, 0, 1], [0, 1, 0], [1, 0, 1]]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 2)

    def test_num_provinces_all_nodes_connected_with_self_loops_returns_one(self):
        # Arrange
        is_connected = [[1, 1, 1], [1, 1, 1], [1, 1, 1]]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 1)

    def test_num_provinces_three_unconnected_nodes_with_self_loops_returns_three(self):
        # Arrange
        is_connected = [[1, 0, 0], [0, 1, 0], [0, 0, 1]]

        # Act
        result = num_provinces(is_connected)

        # Assert
        self.assertEqual(result, 3)

```

### !end-tests
### !explanation

An example of a working implementation:

```python
def num_provinces(is_connected):
    num_nodes = len(is_connected)
    provinces = 0

    # Allocate a list of zeros to keep track of which nodes we have visited.
    # We could use a set, which also has constant reads and writes, but since
    # we know the number of nodes from the start, and can use consecutive
    # integers as the "keys", a list will work and ends up being more efficient
    # (sets do have some overhead above and beyond a list). If we didn't have
    # numeric keys, or they weren't consecutive, a set would be able to serve
    # in this role.

    visited = [0] * num_nodes
    pending = []

    # we need an outer iteration to handle disconnected graphs
    for start_node in range(num_nodes):
        # only start tracing a new province if this node hasn't been visited
        if not visited[start_node]:
            provinces += 1  # this is a new province

            # add the start node to the pending list to kick off our dfs
            pending.append(start_node)
            while pending:
                node = pending.pop()  # get the most recently added node
                if not visited[node]:
                    # mark the current node as visited
                    visited[node] = 1

                    # we must iterate over all nodes to check for edges
                    for next_node in range(num_nodes):
                        # if there is an edge to an unvisited node, add it
                        if (is_connected[node][next_node]
                                and not visited[next_node]):
                            pending.append(next_node)

    # after checking each node in the graph, we have counted all provinces
    return provinces
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<br>
<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
def test_num_provinces_two_provinces_returns_two():
    # Arrange
    is_connected = [[0, 0, 1], [0, 0, 0], [1, 0, 0]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 2


def test_num_provinces_all_nodes_connected_returns_one():
    # Arrange
    is_connected = [[0, 1, 1], [1, 0, 1], [1, 1, 0]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 1


def test_num_provinces_three_unconnected_nodes_returns_three():
    # Arrange
    is_connected = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 3


def test_num_provinces_input_with_no_rows_returns_zero():
    # Arrange
    is_connected = []

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 0


def test_num_provinces_one_node_graph_returns_one():
    # Arrange
    is_connected = [[0]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 1


def test_num_provinces_graph_with_cycle_returns_two():
    # Arrange
    is_connected = [[0, 1, 1, 0], [1, 0, 1, 0], [1, 1, 0, 0], [0, 0, 0, 0]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 2


def test_num_provinces_large_graph_with_four_provinces_returns_four():
    # Arrange
    is_connected = [
        [0, 1, 0, 0, 0, 0, 0, 0, 0, 0],
        [1, 0, 1, 0, 0, 0, 0, 0, 0, 0],
        [0, 1, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
        [0, 0, 0, 1, 0, 1, 0, 0, 0, 0],
        [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 1, 0, 0],
        [0, 0, 0, 0, 0, 0, 1, 0, 1, 0],
        [0, 0, 0, 0, 0, 0, 0, 1, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    ]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 4


def test_num_provinces_two_provinces_with_self_loops_returns_two():
    # Arrange
    is_connected = [[1, 0, 1], [0, 1, 0], [1, 0, 1]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 2


def test_num_provinces_all_nodes_connected_with_self_loops_returns_one():
    # Arrange
    is_connected = [[1, 1, 1], [1, 1, 1], [1, 1, 1]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 1


def test_num_provinces_three_unconnected_nodes_with_self_loops_returns_three():
    # Arrange
    is_connected = [[1, 0, 0], [0, 1, 0], [0, 0, 1]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 3
```

</details>

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 8fee38b2-e84c-4227-821f-b7a9015ca6bb
* title: Time Complexity of Solution
* points: 1
##### !question

What is the time complexity of your solution? Please define and explain your variables.

##### !end-question
##### !placeholder

##### !end-placeholder
##### !hint

Check the next hint for some points to keep in mind that might impact the time complexity of the sample implementation.

##### !end-hint
##### !hint

The sample implementation is based on depth first search, an ideal implementation of which has a time complexity as discussed in the graph reading. But keep in mind that we are using an adjacency matrix rather than an adjacency list to represent the graph. Think about how this might impact the time complexity of the solution. 

The next hint presents a discussion of the time complexity of the sample solution.

##### !end-hint
##### !hint

Even though the sample implementation is based on depth first search, the time complexity is O(N^2), where N is the number of nodes. Since we are using an adjacency matrix, we have to check every node for every other node to see whether there is an edge between them. If the prompt used an adjacency list, we would only have to check each node's neighbors, resulting in the more typical O(N+E) (N being the number of nodes and E being the number of edges) for depth first search.

##### !end-hint
### !end-challenge
<!-- prettier-ignore-end -->


<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 0d865480-af7d-4754-bd39-4520d1bc48cb
* title: Space Complexity of Solution
* points: 1 
##### !question

What is the space complexity of your solution? Please define and explain your variables.

##### !end-question
##### !placeholder

##### !end-placeholder
##### !hint

Check the next hint for some points to keep in mind that might impact the space complexity of the sample implementation.

##### !end-hint
##### !hint

The sample implementation is based on depth first search, an ideal implementation of which has a space complexity as discussed in the graph reading. We are using an iterative approach rather than recursive. Iterative implementations usually have space complexity at least as good as recursive implementations, if not better, due to not needing to add stack frames for each call. However, there are some additional data structures we create that depend on the number of input nodes: the visited list, and the pending list. How are nodes tracked in these lists? How does our usage of them differ? Does this impact the space complexity of the solution?

The next hint presents a discussion of the space complexity of the sample solution.

##### !end-hint
##### !hint

Even though the sample implementation is based on depth first search, the space complexity is O(N^2), where N is the number of nodes. There are two data structures we create that depend on the number of input nodes: the visited list, and the pending list.

The visited list is used to keep track of which nodes we have already visited. We initialize it to a list of zeros, and then set the value at each index to 1 when we visit that node. This means that the visited list will be the same size as the number of nodes in the graph, which is O(N).

The pending list is used to keep track of which nodes we have yet to visit. We initialize it to an empty list, and then add nodes to it as we visit them. Unlike the visited list, we don't know exactly how long the pending list will grow, since it depends on the structure of the graph. The sample solution doesn't check whether a node is already in the pending list (recall that checking membership in a list is itself a linear time operation), and as a result, the same node might appear in the pending list more than once. If we are very unlucky with the structure of the graph, visiting node 1 could add nodes 2 through N, visiting node 2 could add nodes 3 through N, and so on. This would result in a pending list of size (N-1) + (N-2) + ... + 1, which is O(N^2).

But depth first search is usually considered to take O(N) space. How could we improve the space complexity of this implementation? Take a moment to think about it before checking the next hint.

##### !end-hint
##### !hint

The problem with the current implementation is that we could end up with duplicate nodes in the pending list. This situation is unique to the iterative depth first search implementation. If we were to use a recursive implementation, the call stack would grow no larger than O(N), since the neighbors of a node are explored one by one rather than being added to a list. Since the visited list is updated as we explore, we could only get N calls deep before we have visited all of the nodes.

Short of reworking with a recursive approach, we could do some additional bookkeeping to ensure duplicate nodes don't get added to the pending list. We could switch entirely to using a set to track the pending nodes if we don't particularly care about the iteration order of the pending nodes (in this case, we don't). Alternatively, we could add a supplemental set to keep track of nodes we have already seen, and only add nodes to the pending list if they are not already in the set. As with the visited list in this example, since we are working with numeric nodes and we know the number of them from the start, a simple list can serve this purpose without the additional overhead of a set. The additional tracking data is only O(N) itself, bringing our size complexity back down to O(N) overall.

A final approach, but one we'd probably want to avoid, would be to introduce a membership check for the pending list. This would require us to iterate over the pending list to check whether a node is already in it, which would be O(N) for each node we visit. Though this would bring our *space* complexity down to O(N), this would also result in a *time* complexity of O(N^3) for the sample implementation, which is even worse than the O(N^2) we have now.

##### !end-hint
### !end-challenge
<!-- prettier-ignore-end -->