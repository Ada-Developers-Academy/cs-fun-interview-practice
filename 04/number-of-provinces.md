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

1. In the problem statement it says that 2 cities belong to the same province if there is a path from one city to the other
    - To solve this problem, I will need to determine how many subsets of connected nodes exist in the input `is_connected`.

2. The problem statement says that a path between 2 cities which runs through an intermediary city is a valid path.
    - This tells me that when determining a province, I am not only interested in directly connected nodes, but all nodes that can create a path to each other. We only have a separate province if a city or set of cities has no path through any node to the cities of another province.

3. The problem statement does not state if the graph is directed or undircted. The images in the examples show undirected edges connecting the nodes, and the example inputs for `is_connected` show each edge as bidirectional. 
    - I will assume this is an undirected graph based on the examples. This impacts whether we need to follow directional edges to see if nodes have a path between them, or if it can be assumed that if there is a path in one direction, there must be a path back.

4. What should be returned if the graph `is_connected` is empty (has no rows or columns representing cities)?
    - It would depend on if this counts as a valid graph or invalid data that would be removed by a validation function before `num_provinces` was called. If an empty graph is valid, then since there are no cities, the data is not representing any provinces, so I will assume that we can return 0 in that scenario. 

5. Can a node be connected to itself by an edge?
    - I want to better understand the expected allowed structure of the input data. If a node can be connected to itself, as we process that node, we need to ensure that we do not repeat effort by processing the same node more than once as we move through the connected nodes. 

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
##### !hint

Try drawing out some sample graphs and translating them into an adjacency matrix if coming up with an adjacency matrix representing a graph is challenging.

##### !end-hint
##### !explanation 

Example tests:

```python
def test_num_provinces_returns_two_for_two_provinces():
    # Arrange
    is_connected = [[0, 0, 1], [0, 0, 0], [1, 0, 0]]

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 2

def test_num_provinces_returns_zero_if_input_empty():
    # Arrange
    is_connected = []

    # Act
    result = num_provinces(is_connected)

    # Assert
    assert result == 0
```

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: a195485b-2f22-498c-ae19-8aba00d821fb
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `num_provinces` as if you were talking through the details with another developer who will have to implement the function. We should capture the main use cases, but the steps do not need to be a detailed plan for every contingency. 
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
##### !explanation 

Example steps:

1. Initialize a list to keep track of the nodes we have visited.
2. Iterate over the nodes in the graph (in the adjacency matrix order, irrespective of edge connections).
3. For each node, if we have not yet visited it, increment the province count and perform a search (either depth-first or breadth-first could work) to find all of the nodes reachable from the current node.
4. For each node we find in the search, mark it as being visited.
5. Upon completing each search, we will have found all of the cities in a province. Continue iterating over the nodes in the graph.
6. Once we have iterated over all of the nodes in the graph, we will have found all of the provinces, so return the province count.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: d424be4c-55d2-4c7f-be56-e14240f51c01
* title: Review Logical Steps
* topics: pse
##### !question

We want to know if we are laying out an approach to the coding problem that makes sense for our context and if that approach is clearly conveying our thoughts on technical topics to others.  While we build our skills in breaking down and describing algorithms, let's use an AI tool like ChatGPT to review the Logical Steps we wrote above. Our goals are to check if the steps:
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
    * Explain why it doesn’t apply to this problem, and cite a source (docs, class notes, instructor explanation, or trusted online reference) that supports your reasoning.
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

The feedback noted that separating "detect an unvisited node" from "explore everything reachable from that node" makes the two-part structure of the algorithm easy to follow — an outer loop that finds new provinces, and an inner search that fully explores each one. I think this was effective because it shows I understood that these are two distinct responsibilities before describing how they work together.

<br>

One improvement the AI recommended was to be more explicit about what "reachable" means in terms of the adjacency matrix, rather than just saying I would "perform a search." If I were rewriting my steps, I would clarify that from a given city, the directly reachable cities are found by reading its row in the matrix, and the search continues by checking the rows of each newly discovered city in turn, so that indirectly connected cities are eventually reached as well.

<br>

A piece of feedback I believe was unnecessary was the suggestion that I should specify whether the search should be depth-first or breadth-first in order for my steps to be correct. My steps already state that "either depth-first or breadth-first could work," and since both approaches visit each node and edge within a component exactly once, they produce the same result and the same overall time complexity here, so choosing one over the other doesn't change the correctness of the roadmap.

<br>

The suggestion that surprised me was pointing out that because the outer loop only starts a new search from a node that hasn't been visited yet, every node is guaranteed to be the starting point of at most one search, which is what prevents the same province from being counted more than once. I had described the visited check as just a way to avoid repeating work, but framing it as the reason we don't double-count provinces made the connection between the visited list and the correctness of the final count much clearer to me.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->