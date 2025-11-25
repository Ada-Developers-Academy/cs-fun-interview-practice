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
* type: paragraph
* id: 31a03295-400d-4a99-b0f6-d772987b9cdf
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

ChatGPT's feedback confirmed that most of my observations were accurate and directly related to understanding the problem, especially the idea that provinces are really connected components in a graph. 

<br>

Suggestion 9 (confirming that “provinces” don’t imply anything beyond connected components) was new to me and helped reinforce that narrative terms can hide potential implied constraints. A few suggestions overlapped with my original questions and thus were less useful, like whether diagonal entries follow a consistent convention which is mostly handeled by my question about the graph being directed or undirected, since that impacts the input's representation. 

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
