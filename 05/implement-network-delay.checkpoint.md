# Implement Network Delay Time

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 029a5285-6422-4acf-a71b-d4ee862a59ec
* title: Network Delay Time
* points: 3
### !question
For this exercise, create a function `network_delay_time` which accepts the following parameters:
- A list of travel times, `times`. Each element of `times` represents a directed edge `times[i] = (uᵢ, vᵢ, wᵢ)` where `uᵢ` is the source node, `vᵢ` is the target node, and `wᵢ` is the time it takes for a signal to travel from the source node to the target node
- The total number of nodes in the graph, `n`
- The node from which a signal is being sent, `source`

The nodes in the graph are labeled from `1` to `n`.

Return the **minimum** time it takes for **all** of the nodes in the graph to receive the signal from the `source` node. If it is not possible for all of the nodes to receive the signal, return `-1`.

**Example 1**
<br>
![example graph 1](../images/network_delay_example-1.png)
```
Input: times = [[2,1,1], [2,3,1], [3,4,1]], source = 2, n = 4
Output: 2
Explanation:
Starting from node 2 (our source node): it takes 1 unit of time to reach node 1, 1 unit of time to
reach node 3, and 2 units of time to reach node 4 (1 unit of time from 2 -> 3 and 
1 unit of time from 3 -> 4 so 2 units overall). 
Therefore, to reach all of the nodes, it would take a minimum of 2 units of time. 
```

**Example 2:**
<br>
![example graph 2](../images/network_delay_example-2.png)
```
Input: times =[[2,1,1], [2, 3, 2], [3, 1, 1]], source = 1, n = 3
Output: -1
It is not possible to reach any other node from node 1, so the function would return 
-1 to indicate it is not possible to reach all of the nodes in the graph from the given 
source node.
```

**Example 3:**
<br>
![example graph 3](../images/network_delay_example-3.png)
```
Input: times =[[2, 3, 2]], source = 2, n = 3
Output: -1
It is not possible to reach all of the nodes in the graph due to the graph being 
disconnected, so the function would return -1 to indicate it is not possible to 
reach all of the nodes in the graph from the given source node.
```
### !end-question
### !placeholder

```python
def network_delay_time(times, n, source):
    """
    A function which takes in a list of edges representing a graph of network nodes
    and the time to travel between the nodes, the number of nodes in the network
    graph, and a source node. 

    The function returns the minimum amount of time to travel to all of the nodes in
    the graph from the source node.
  
    Parameters:
    times (List[List[int]]): List of edges representing the time to travel between nodes in the graph.
    n (int): The total number of nodes in the network graph
    source (int): The source node from which to travel the network
  
    Returns:
    Int: The minimum amount of time to travel to all of the nodes in the graph.
    """
    pass
```

### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_network_delay_returns_correct_result_for_small_connected_graph(self):
        # Arrange
        times = [
            [2,1,1],
            [2,3,1],
            [3,4,1]
        ]
        n = 4
        source = 2

        # Act
        answer = network_delay_time(times, n, source)

        # Assert
        self.assertEqual(answer, 2)

    def test_network_delay_returns_minus_1_when_node_unreachable(self):
        # Arrange
        times = [
            [2,1,1],
            [2,3,2],
            [3,1,1]
        ]
        n = 3
        source = 1

        # Act
        answer = network_delay_time(times, n, source)

        # Assert
        self.assertEqual(answer, -1)

    def test_network_delay_returns_minus_1_for_disconnected_graph(self):
        # Arrange
        times = [
            [2,3,2]
        ]
        n = 3
        source = 2

        # Act
        answer = network_delay_time(times, n, source)

        # Assert
        self.assertEqual(answer, -1)

    def test_network_delay_returns_correct_result_for_larger_graph(self):
        # Arrange
        times = [
            [1, 2, 3],
            [2, 4, 1],
            [2, 5, 5],
            [2, 3, 6],
            [3, 5, 6],
            [4, 5, 7]
        ]
        n = 5
        source = 1

        # Act
        answer = network_delay_time(times, n, source)

        # Assert
        self.assertEqual(answer, 9)
```
### !end-tests
### !explanation

An example of a working implementation:

```python
import collections
from heapq import heappush, heappop
def network_delay_time(times, n, source):
    # Initialize dictionary with default value as a list
    # More information about defaultdict can be found in the documentation for Python: https://docs.python.org/3/library/collections.html#collections.defaultdict
    graph = collections.defaultdict(list)
    # For each edge in the graph, add the neighbors for a node to the graph
    # such that graph[node] = [(neighbor1, time1), (neighbor2, time2)...]
    # The graph is directed, so we only need to append one direction
    for u, v, time in times:
        graph[u].append((v, time))

    # initialize the time needed to reach each node in the graph, overestimating to infinity
    time_needed = [float('inf')] * n
    # set the time to reach the source node to 0
    time_needed[source-1] = 0
    # initialize min heap for traversal
    # priority 0 to travel to the source node
    heap = [(0, source)] 

    visited = set() # used to record all visited nodes

    # while there are nodes in the heap
    while heap:
        # pop off the closest node
        time, curr_node = heappop(heap)
        # if the current node has already been visited, continue
        if curr_node in visited:
            continue
        # add the current node to the list of visited nodes
        visited.add(curr_node)
        # traverse through the current node's neighbors
        for neighbor, neighbor_time in graph[curr_node]:
            # if the neighbor has already been visited, continue
            if neighbor in visited:
                continue
            # calculate the total time to travel to the neighbor
            total_time = time + neighbor_time
            # if the total time is less than the previous time stored to travel to the neighbor
            if total_time < time_needed[neighbor - 1]:
                # store the total time as the time needed to travel to the neighbor
                time_needed[neighbor - 1] = total_time
                # push onto heap to be visited later
                heappush(heap, (total_time, neighbor))

    # return the max time in time_needed list if all of the nodes have been visited, otherwise return -1
    return max(time_needed) if len(visited) == n else -1
```
### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
from pse.pse import network_delay_time

def test_network_delay_returns_correct_result_for_small_connected_graph():
    # Arrange
    times = [
        [2,1,1],
        [2,3,1],
        [3,4,1]
    ]
    n = 4
    source = 2

    # Act
    answer = network_delay_time(times, n, source)

    # Assert
    assert answer == 2

def test_network_delay_returns_minus_1_when_node_unreachable():
    # Arrange
    times = [
        [2,1,1],
        [2,3,2],
        [3,1,1]
    ]
    n = 3
    source = 1

    # Act
    answer = network_delay_time(times, n, source)

    # Assert
    assert answer == -1

def test_network_delay_returns_minus_1_for_disconnected_graph():
    # Arrange
    times = [
        [2,3,2]
    ]
    n = 3
    source = 2

    # Act
    answer = network_delay_time(times, n, source)

    # Assert
    assert answer == -1

def test_network_delay_returns_correct_result_for_larger_graph():
    # Arrange
    times = [
        [1, 2, 3],
        [2, 4, 1],
        [2, 5, 5],
        [2, 3, 6],
        [3, 5, 6],
        [4, 5, 7]
    ]
    n = 5
    source = 1

    # Act
    answer = network_delay_time(times, n, source)

    # Assert
    assert answer == 9
```

</details>

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: 5d1ff7ab-da11-4d64-95a9-3b07c55a9b2c
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
* id: ae994d0b-c54a-45e0-8793-9c0ceee33718
* title: Space Complexity of Solution
* points: 1 

##### !question

What is the space complexity of your solution? Please define and explain your variables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->