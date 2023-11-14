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

### !end-challenge
<!-- prettier-ignore-end -->
