# Network Delay

## Problem Statement  

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
Starting from node 2: it takes 1 unit of time to reach node 1, 1 unit of 
time to reach node 3, and 2 units of time to reach node 4 (1 unit of time from 
2 -> 3 and 1 unit of time from 3 -> 4 so 2 units overall). 

Therefore, to reach all of the nodes, it would take a minimum of 2 units of time. 
```

**Example 2**
<br>
![example graph 2](../images/network_delay_example-2.png)
```
Input: times =[[2,1,1], [2, 3, 2], [3, 1, 1]], source = 1, n = 3
Output: -1
It is not possible to reach any other node from node 1, so the function would 
return -1 to indicate it is not possible to reach all of the nodes in the graph
from the given source node.
```

**Example 3**
<br>
![example graph 3](../images/network_delay_example-3.png)
```
Input: times =[[2, 3, 2]], source = 2, n = 3
Output: -1
It is not possible to reach all of the nodes in the graph due to the graph being 
disconnected, so the function would return -1 to indicate it is not possible to 
reach all of the nodes in the graph from the given source node.
```

<br>

## Prompts

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: a2a0a745-a920-41b2-aa75-0a3659528e59
* title: Ask Clarifying Questions
* topics: pse
##### !question

List three or more questions whose answers would clarify the problem statement.

For each question, provide an explanation which includes the effect your decision would have on how you would approach the problem.

##### !end-question

##### !explanation

Here are some example clarifying questions:

1. In which way is the graph being represented?
2. Do the nodes start at 0 or 1?
3. Will the graph ever be empty? What should the result be?
4. Will the graph edges always be directed?
5. What if there are duplicate edges in the list?
6. What should we do in case of malformed graph data?

##### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->

### !challenge
* type: code-snippet
* language: python3.6
* id: de06db6c-7f06-4999-97ff-253b5af91e45
* title: Write Unit Tests
* topics: pse
##### !question

1. Use the comments provided to write at least two example input/outputs:
    * Consider at least one nominal and one edge case.
    * What is the expected output for the given input?
    * You can use the examples provided in the prompt, or other examples.
2. Write unit tests for `network_delay_time` for the nominal and edge cases you identified in the first step.

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
```

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: c2fe4d3a-38d9-4e42-8013-3ec782ac42a4
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `network_delay_time` in enough detail that someone else could write the code. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. For example, 1. Handle invalid input, 2. Given valid input, perform the computation/solve the problem/etc.
* Your logical steps could take the form of a numbered list, pseudo code, or anywhere in between. What's important at this stage is to think through and outline the implementation before writing code.

##### !end-question

##### !placeholder

Write the logical steps here.

##### !end-placeholder

##### !hint
One approach could be to figure out the cost from the start node to each of the other nodes individually. However, since weights are involved, we know that plain BFS isn't guaranteed to find the minimum cost to each other node. We'll need another approach.
##### !end-hint

##### !hint
Dijkstra's algorithm _does_ find the minimum path to each other node, but it is not guaranteed to work with negative weights. Since we are dealing with delay time, which we can assume to be non-negative, we can use Dijkstra's algorithm. Dijkstra's algorithm also has the benefit that it will find the shortest path to each node in the graph, all at once. So once we've visited all the nodes, we know we're done.

What would it mean if we completed Dijkstra's algorithm and there were still nodes we haven't visited?
##### !end-hint

##### !hint
We can't run Dijkstra's algorithm directly on an edge list, so we should also consider what we need to do to convert the input into a form that Dijkstra's algorithm can work with.
##### !end-hint

##### !hint
Once we've run Dijkstra's algorithm over our data, how can we distinguish between a successful result and an unsuccessful result?

The next hint presents the steps for one possible approach.
##### !end-hint

##### !hint
1. Convert the input edge data into an adjacency dict.
   1. Iterate over the edges.
   2. For each edge, add the target node (with weight) to the list of edges in the adjacency dict for the source node.
2. Set up the data structures we'll need to track the minimum cost to each node.
   1. Initialize a dict to track the minimum cost to each node.
   2. Initialize a set to track the nodes we have visited.
   3. Initialize a priority queue to track the nodes we have yet to visit.
3. Run Dijkstra's algorithm over the converted graph data, tracking the minimum cost to each node.
4. Upon completing Dijkstra's algorithm, we will have the minimum cost to each node. If there are nodes whose cost is still infinity, we know that we were unable to reach those nodes from the source node. Alternatively, we could check the length of the visited set against the number of nodes in the graph. If they are not equal, we know that we were unable to reach all of the nodes in the graph from the source node.
5. If not all nodes were reached, return -1. Otherwise, return the maximum cost from the minimum cost list. Dijkstra's algorithm finds minimum paths, but according to the challenge, we want to return the longest overall (how long it takes for _every_ node to receive a signal). In other words, we are looking for the maximum minimum.
##### !end-hint

### !end-challenge
<!-- prettier-ignore-end -->
