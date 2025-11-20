# Linked List Intersection

## Problem Statement

Given the heads of two singly linked-lists `head_a` and `head_b`, return the node at which the two lists intersect. If the two linked lists do not intersect, the function should return `None`.

For example, the following two linked lists begin to intersect at the node containing 8:

![intersecting linked lists example 1](../images/intersection_linked_list_example_1.png)

Text representation for ChatGPT reviews:
```
A:      4 -> 1 ->
                  8 -> 4 -> 5
B: 5 -> 6 -> 1 ->
```

The following two linked lists do _not_ intersect at all.

![intersecting linked lists example 2](../images/intersection_linked_list_example_2.png)

Text representation for ChatGPT reviews:
```
A: 2 -> 6 -> 4
                  
B:      1 -> 5
```

For this problem, we want to focus on the nodes themselves and not necessarily the *value* inside of the node.

For example, while the following linked lists have tails that share the same values, they are not considered intersecting because the nodes of the linked lists are not the same nodes in memory.

![intersecting linked lists example 3](../images/intersection_linked_list_example_3.png)

Text representation for ChatGPT reviews:
```
A: 5 -> 2 -> 4 -> 1

B: 3 -> 8 -> 4 -> 1
```

There are no cycles anywhere in the linked list structures. Assume any intersection includes the tails of each list.

The linked lists must retain their original structure after the function returns.

## Prompts

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: c273469f-8ac2-4c98-a876-521b74d6e7e0
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

Here are some example clarifying questions:

1. What should be returned if one or both lists are empty?
    - If either list is empty there can be no intersection, so by the problem description we should return `None`.

2. Can the lists intersect more than once?
    - The examples do not clarify this, but the problem statement has the line "Assume any intersection includes the tails of each list." Since the tail is the last element of a list I can assume that this means that from the point of intersection the entire rest of the lists will be part of the intersection.

3. Based on the problem statement, I recognize that the data type or types held by the nodes will not impact the implementation. 
    - Because we are only interested in where the nodes intersect in memory, we will not need to examine the held values. 

4. There are no cycles anywhere in the linked list structures
    - This means the solution does not need to worry about detecting cycles to avoid getting stuck in an infinite loop. If I start at the head of one list and keep moving through the pointers from node to node, I will eventaully reach a `None` value for the next node when I reach the end of the list. 

5. The problem statement says "The linked lists must retain their original structure after the function returns."
    - This tells me that however I move through the lists, I should not change the links between the nodes, I should only traverse the nodes to ensure there are no side effects to the function. 

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 83f03637-f3af-42b0-8b21-feb42f4646e0
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

Here’s a concise, learner-style summary in 10 sentences or fewer:

The feedback confirmed that empty lists, single intersections, and the importance of node identity were all correctly understood. It also reinforced that cycles are not part of this problem, so normal traversal is safe. 

<br>

The reviewer pointed out additional useful observations, like the fact that the two lists can have different lengths, which affects how their positions relate before the intersection, and that it could be helpful to check whether the intersection can occur at the head. There were suggestions such as confirming list validity that are less useful for this specific problem space but would be handled somewhere in a real project.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: c52a82cc-4062-405a-b475-0f269b8494c0
* title: Write Unit Tests
* topics: pse
##### !question

1. Use the comments provided to write at least two example input/outputs:
    * Consider at least one nominal and one edge case.
    * What is the expected output for the given input?
    * You can use the examples provided in the prompt, or other examples.
2. Write unit tests for `find_intersecting_node` for the nominal and edge cases you identified in the first step.

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
def test_find_intersecting_node_returns_intersection_for_lists_of_same_length():
    # Arrange
    node_d = Node("D")
    node_x = Node("X")
    node_one = Node("1")
    node_two = Node("2")
    node_three = Node("3")

    node_one.next = node_two
    node_two.next = node_three

    # List A: D -> 1 -> 2 -> 3
    node_d.next = node_one

    # List B: X -> 1 -> 2 -> 3
    node_x.next = node_one

    head_a = node_d
    head_b = node_x

    # Act
    result = find_intersecting_node(head_a, head_b)

    # Assert
    assert result == node_one

def test_find_intersecting_node_returns_none_with_one_empty_list():
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    # List A: D -> E -> F
    node_d.next = node_e
    node_e.next = node_f

    # List B: None, the list is empty

    # Act
    result = find_intersecting_node(node_d, None)

    # Assert
    assert result is None
```

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 10510a7b-e915-42cc-8cea-26555f96c34d
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `find_intersecting_node` in enough detail that another developer could reasonably implement a solution. We should capture the main use cases, but the steps do not need to be a detailed plan for every contingency. 
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

How do we iterate through a singly linked list?

An intersection isn't guaranteed to be at matching indices in each list, so how can we compare each element in one list to each element in another?

How do we know if two nodes are the same in memory?

##### !end-hint
##### !explanation 

1. Initialize a pointer to the head node of list 1
2. Iterate through the nodes of list 1. For each node in list 1:
    1. Initialize a pointer to the head of list 2
    2. Iterate through the nodes of list 2. For each node in list 2:
        1. Check if the current node of list 1 from the outer loop is the same node in memory as the current node of list 2
           1. If they are the same nodes, return the current node
           2. If they are not the same node, update the list 2 pointer to the next node of list 2 to continue iterating through list 2
    3. Update the list 1 pointer to the next node of list 1 to continue iterating
3. If we reach the end of either list 1 or list 2 and have not returned, then return `None` since there was no intersection 

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

