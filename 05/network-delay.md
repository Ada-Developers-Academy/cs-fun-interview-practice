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
##### !placeholder

Add observations, assumptions, and questions here:

Eg. from the sample PSE: 
I observe that the function should return a string indicating the result of the game: "Player 1 wins!", "Player 2 wins!", or "It's a tie!"
    - Aside from checking if someone wins, I need to consider the edge case where the players could tie.

##### !end-placeholder
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

When naming a test, we want to ensure the name describes the scenario we are testing by including information like the function being tested, inputs, and expected outputs. 
* e.g. from the example PSE: if we wanted to test that the function winner returns a tie when `player_1` and `player_2` have the same value, then we might name the test something like `test_winner_both_inputs_paper_returns_tie`.

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

Without writing code, describe how you would implement `network_delay_time` as if you were talking through the details with another developer who will have to implement the function. We should capture the main use cases, but the steps do not need to be a detailed plan for every contingency. 
* The objective is to practice describing algorithms and technical concepts while creating a roadmap that we can use to keep ourselves oriented towards our goal during the implementation step.
* It is okay to leave some of the finer details to be worked out in the implementation itself!

As you write your steps, keep the following guidelines in mind:
* We want to think about a general approach rather than what the code would look like line-by-line. 
* It may be helpful to break up the problem/algorithm into smaller subproblems/algorithms. 
    * For example: 1. Handle edge cases, 2. Perform the computation/solve the problem/etc.
* The steps should be a description as if you were talking out the problem with another person and should be agnostic of any particular language. 
    * As such, they should not include code syntax in the description.

What's important at this stage is to think through how you would put an approach into words, and outline the implementation before writing code.

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

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 68cf2c87-a448-4e40-b6bc-5cf7f301bd9b
* title: Review Logical Steps
* topics: pse
##### !question

We want to know if we are laying out an approach to the coding problem that makes sense for our context and if that approach is clearly conveying our thoughts on technical topics to others. While we build our skills in breaking down and describing algorithms, let's use an AI tool like ChatGPT to review the Logical Steps we wrote above. Our goals are to check if the steps:
- convey the technical concepts and requirements of the problem in a way that another person can understand
- make sense for the problem being solved
- are not missing important steps or scenarios
- are agnostic of any particular language – the steps should not include code syntax.

<br>

For this question we will:
1. Build a prompt using [the template linked here](https://gist.githubusercontent.com/ada-instructors/670252696f1625cf0ed77c0997cd165d/raw/pse_logical_steps_review_template.md)
2. Share the completed prompt with an AI tool like ChatGPT
3. Reflect on the information shared by the AI tool, then use the prompts below to summarize its findings and your learnings.

<br>

Reflection Prompts

1. Identify one specific strength the AI highlighted in your explanation. 
    * Quote or paraphrase the part of the feedback that mentions this strength, and explain why you think that aspect of your explanation was effective.
2. Point out at least one specific improvement the AI recommended.
    * Describe exactly which part of your explanation would benefit from strengthening then outline how you would revise that part if you were rewriting it now.
3. Identify one piece of AI feedback you believe was inaccurate, irrelevant, or unnecessary. 
    * Explain why it doesn't apply to this problem, and cite a source (docs, class notes, instructor explanation, or trusted online reference) that supports your reasoning.
4. Describe one change the AI suggested that was new or surprised you. 
    * Share how this suggestion shifted your understanding of the problem or your explanation.

<br>

In the box below, please submit:
1. A shareable link to your conversation in ChatGPT
    - [Documentation for creating a shareable link in ChatGPT](https://help.openai.com/en/articles/7925741-chatgpt-shared-links-faq)
2. Your reflections and summary of the discussion with ChatGPT

##### !end-question
##### !explanation

As an example, let’s say we used logical steps similar to the explanation for the question above in our prompt. Depending on how the supplied steps differ and exactly what ChatGPT shares, a reflection and summary might look like:

<br>

Chat Link: `<url to your conversation>`

<br>

One thing the feedback called out as a strength was keeping the "convert the edge list into an adjacency dict" step separate from the Dijkstra step itself, rather than folding the conversion logic into the traversal. The interviewer said this made it clear I recognized Dijkstra needs a different data shape than the raw input, without getting into implementation details about dictionaries or lists. I think this landed well because it showed I was thinking about data representation as its own concern, not just as a side effect of "doing the algorithm."

<br>

The main improvement suggested was to say more about why a priority queue is required rather than just listing it as one of the data structures I'm initializing. Right now my steps mention it alongside the visited set and cost list without explaining its role. If I revised this, I'd add a sentence explaining that the priority queue is what lets us always process the closest unvisited node next, which is the property that guarantees a node's cost is finalized the first time we visit it — otherwise it's not obvious why a plain queue or list wouldn't work just as well.

<br>

One suggestion I pushed back on was a recommendation to add a step for handling negative edge weights before running Dijkstra. That doesn't apply here — the problem defines wᵢ as a signal travel time, which can't be negative, and the hints for this problem already establish that assumption as the reason Dijkstra's algorithm is a valid choice in the first place. Adding a check for something the problem statement rules out would be solving for a case that can't occur, so I left that out of the implementation.

<br>

I was surprised by a comment pointing out that my final step, "return the maximum cost from the minimum cost list," is doing two jobs at once: confirming reachability (are we sure every node got a cost?) and then computing the answer (what's the slowest of those costs?). I wrote it as a single step, but separating those two ideas out clarified for me why the problem asks for a "maximum of minimums" instead of a sum or an average. It's because the overall delay is determined by whichever node is slowest to hear the signal, not by the total work done to reach everyone.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->