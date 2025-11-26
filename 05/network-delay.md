# Network Delay

## Problem Statement  

For this exercise, create a function `network_delay_time` which accepts the following parameters:
- A list of travel times, `times`. Each element of `times` represents a directed edge `times[i] = (uᵢ, vᵢ, wᵢ)` where:
    - `uᵢ` is the source node
    - `vᵢ` is the target node 
    - `wᵢ` is the time it takes for a signal to travel from the source node to the target node
- The total number of nodes in the graph, `n`
- The node from which a signal is being sent, `source`

The nodes in the graph are labeled from `1` to `n`.

Return the **minimum** time it takes for **all** of the nodes in the graph to receive the signal from the `source` node. If it is not possible for all of the nodes to receive the signal, return `-1`.

### Example 1

![example graph 1](../images/network_delay_example-1.png)

```py
Inputs: times = [[2,1,1], [2,3,1], [3,4,1]], n = 4, source = 2 

Output: 2
```

**Explanation:** Starting from node 2: it takes 1 unit of time to reach node 1, 1 unit of 
time to reach node 3, and 2 units of time to reach node 4 (1 unit of time from 
2 -> 3 and 1 unit of time from 3 -> 4 so 2 units overall). 

Therefore, to reach all of the nodes, it would take a minimum of 2 units of time. 

### Example 2

![example graph 2](../images/network_delay_example-2.png)  

```py
Inputs: times = [[2,1,1], [2, 3, 2], [3, 1, 1]], n = 3, source = 1

Output: -1
```

**Explanation:** It is not possible to reach any other node from node 1, so the function would 
return -1 to indicate it is not possible to reach all of the nodes in the graph
from the given source node.

### Example 3

![example graph 3](../images/network_delay_example-3.png)

```py
Input: times = [[2, 3, 2]], n = 3, source = 2

Output: -1
```

**Explanation:** It is not possible to reach all of the nodes in the graph due to the graph being 
disconnected, so the function would return -1 to indicate it is not possible to 
reach all of the nodes in the graph from the given source node.

## Prompts

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: a2a0a745-a920-41b2-aa75-0a3659528e59
* title: Describe Your Understanding
* topics: pse
##### !question

Before you begin solving this problem, take a moment to think like a professional software engineer. 
- What do we know about the problem? 
- What assumptions can we make based on the information in the problem statement? 
- What further information do the example inputs and outputs give us?
- What questions would you ask a teammate, product manager, or interviewer to better understand the problem before writing any code?

<br>

In the box below, list 5 or more observations about the problem or questions whose answers would clarify the problem statement. For each observation or question, include information on why that observation is important or why you are asking the question.
- For each observation, answer how that observation will affect your approach to the problem.
- For each question, describe what you are hoping to clarify about the problem and provide an answer which includes the effect your decision would have on how you might approach the problem.

<br>

As you come up with observations and questions, assume that error handling for invalid data is managed outside the function. We want to focus on the core behavior of the function we will write.

##### !end-question
##### !hint

Further questions to ask as you read through the problem statement and examples:
- What is the goal of the function?
- What are the types of the expected inputs and outputs?
- Are there any restrictions on any of the inputs?
  - For example: if any of the inputs are a list, do we know anything about how the list is ordered?
- What do the examples show us about the data types and values that are allowed for our inputs?
- What do the examples tell us about the return value in different scenarios?
- Reflecting on the observations you have made so far, what questions would give you new information?

<br>

Consider the following for inspiration:
- [About PSEs](../about-pses/about-pses.md)
- [Our example PSE with example answers](../about-pses/example-pse.md)
- Previous PSEs

##### !end-hint
##### !explanation

One of many possible responses could look like:

1. The problem statement gives our node and edge information in a non-standard graph representation which is not set up to work easily with traditional graph searching algorithms.
    - The `times` list still tells us which nodes are connected and their edge weights. Using this I could convert the data into something like an adjacency matrix that would allow me to apply common graph searching techniques.

2. Each entry in `times` represents a directed edge and the problem statement says to return -1 if it's not possible for all nodes to receive the signal.
    - There are 2 cases where the node might not reach the signal: the node is fully disconnected from the graph, or there is no path through the directed edges to a node from the source. 

3. I see that the nodes will be labeled from 1 - `n`
    - I need to keep indexing in mind as I create my own representation of the graph data and index into it as we traverse nodes to avoid off by 1 index errors.

4. We need to return the minimum time it takes for all nodes to receive a signal from the `source` node.
    - If we know the minimum distance it takes to get from the source node to each other node, then the minimum time to reach all nodes would be the largest of these minimum path values from source to nodes. 

5. We are given the total number of nodes in the graph, and we will need some way to track the nodes we have visited.
    - If we traverse all the connected nodes and our set of visited nodes is less than the total nodes in the graph, some node must be disconnected.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

### !challenge
* type: paragraph
* id: ee8e73b0-2435-4fb9-b3f2-f695fb989b3b
* title: Review Observations & Questions
* topics: pse
##### !question

While we build our skills in breaking down a problem and choosing clarifying questions, let’s use an external tool like ChatGPT to review the observations and questions we wrote while describing our understanding. 

<br>

Our goals are to: 
- confirm if our observations and assumptions make sense in the context of the code problem
- ensure we are asking questions that will tell us new information about the problem space
- check our understanding of the information we expect to get from those questions
- uncover other observations that would help shape our approach and understand how they would affect our approach
- uncover further questions that could be useful to ask and understand why those other questions could be helpful

<br>

For this question we will:
1. Build a prompt using [the template linked here](https://gist.githubusercontent.com/ada-instructors/16c97dc4b16ab2bf449d9d7a81caeb16/raw/pse_observations_questions_review_template.md)
2. Share the completed prompt with an AI tool like ChatGPT
3. After the initial review, ask the AI tool *at least one* follow up question that furthers your understanding of the problem and why certain observations or questions are useful. Some examples could be asking questions to: 
    - ensure your understanding of the analysis of the observations
    - get more details on the information we could get from asking particular questions
    - learn more about new information shared by the tool
4. Reflect on the information shared by the AI tool and summarize its findings and your learnings

<br>

In the box below, please submit:
1. A shareable link to your conversation in ChatGPT
    - [Documentation for creating a shareable link in ChatGPT](https://help.openai.com/en/articles/7925741-chatgpt-shared-links-faq)
2. Your reflections and summary of the discussion with ChatGPT

##### !end-question
##### !hint

**Troubleshooting**
- If you are having issues with the tool understanding the prompt, try formatting the problem statement or examples differently.
- If you’ve reformatted the information and are still not getting useful results, reach out in #study-hall and share what you are experiencing and the link to your chat so folks can take a look and help you troubleshoot!

<br>

**Summarizing the Review**
- Did the AI tool uncover anything about the observations you made that you hadn’t considered?
- Did the AI tool uncover anything about the questions you asked that you hadn’t considered?
- Did the AI tool suggest updates to the observations you made or questions you asked? 
    - If so, what updates and why?
- Did the AI tool suggest any new observations or questions?
    - If so, what? Why would they be useful?

##### !end-hint
##### !explanation 

For an example of what a review response might look like, let’s say that we provided observations similar to the example response from the "Explanation" section of the previous question to complete the review prompt. 

<br>

Depending on exactly what ChatGPT shares, a reflection and summary might look like:

<br>

Chat link: `<url to your conversation>`

<br>

The feedback confirmed that most of my observations were relevant and showed solid reasoning about the problem space. I was given some new points to consider or clarify, such as the possibility of multiple edges between the same nodes and that edge weights aren’t explicitly stated to be positive (though for a problem space like network delay, a negative value would not make sense). 

<br>

Some suggestions repeated ideas I had already touched on, like emphasizing the importance of directionality and unreachable nodes, but they pushed me to state those ideas more explicitly. There was also overlap in the advice about not drifting into implementation thinking, which I had been starting to do when mentioning representation conversion. 

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

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
    result = network_delay_time(times, n, source)

    # Assert
    assert result == 2

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
    result = network_delay_time(times, n, source)

    # Assert
    assert result == -1
```

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: c2fe4d3a-38d9-4e42-8013-3ec782ac42a4
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `network_delay_time` in enough detail that another developer could reasonably implement a solution. We should capture the main use cases, but the steps do not need to be a detailed plan for every contingency. 
- The objective is to create a roadmap that we can use to keep ourselves oriented towards our goal
- It is okay to leave some of the finer details to be worked out in the implementation itself!

As you write your steps, keep the following guidelines in mind:
* We want to think about a general approach rather than what the code would look like line-by-line. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. 
    * For example: 1. Handle edge cases, 2. Perform the computation/solve the problem/etc.
* The steps should be a description as if you were talking out the problem with another person and should be agnostic of any particular language. 
    * As such, they should not include code syntax in the description.

What's important at this stage is to think through and outline the implementation before writing code.

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

We can't efficiently run Dijkstra's algorithm directly on an edge list, so we should also consider what we need to do to convert the input into a form that Dijkstra's algorithm can work with.

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
   1. Initialize a list to track the minimum cost to each node, with the value for each node starting at infinity.
   2. Initialize a set to track the nodes we have visited.
   3. Initialize a priority queue to track the nodes we have yet to visit.
3. Run Dijkstra's algorithm over the converted graph data, tracking the minimum cost to each node.
4. Upon completing Dijkstra's algorithm, we will have the minimum cost to each node. If there are nodes whose cost is still infinity, we know that we were unable to reach those nodes from the source node. Alternatively, we could check the length of the visited set against the number of nodes in the graph. If they are not equal, we know that we were unable to reach all of the nodes in the graph from the source node.
5. If not all nodes were reached, return -1. Otherwise, return the maximum cost from the minimum cost list. Dijkstra's algorithm finds minimum paths, but according to the challenge, we want to return the longest overall (how long it takes for _every_ node to receive a signal). In other words, we are looking for the maximum minimum.

##### !end-hint
##### !explanation 

Example approach:

1. Convert the input edge data into an adjacency dict.
   1. Iterate over the edges.
   2. For each edge, add the target node (with weight) to the list of edges in the adjacency dict for the source node.
2. Set up the data structures we'll need to track the minimum cost to each node.
   1. Initialize a list to track the minimum cost to each node, with the value for each node starting at infinity.
   2. Initialize a set to track the nodes we have visited.
   3. Initialize a priority queue to track the nodes we have yet to visit.
3. Run Dijkstra's algorithm over the converted graph data, tracking the minimum cost to each node.
4. Upon completing Dijkstra's algorithm, we will have the minimum cost to each node. If there are nodes whose cost is still infinity, we know that we were unable to reach those nodes from the source node. Alternatively, we could check the length of the visited set against the number of nodes in the graph. If they are not equal, we know that we were unable to reach all of the nodes in the graph from the source node.
5. If not all nodes were reached, return -1. Otherwise, return the maximum cost from the minimum cost list. Dijkstra's algorithm finds minimum paths, but according to the challenge, we want to return the longest overall (how long it takes for _every_ node to receive a signal). In other words, we are looking for the maximum minimum.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->
