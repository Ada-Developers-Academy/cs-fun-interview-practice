# Most Frequent K Elements

## Problem Statement

Create a function, `most_frequent_k_elements`, that takes a non-empty array of integers and returns the `k` most frequent elements. 
- You may assume `k` is always valid, where `1 ≤ k ≤ number of unique elements`.

**Example 1:**
```
Input: numbers = [1, 1, 1, 2, 2, 3], k = 2
Output: [1, 2]
```

**Example 2:**
```
Input: numbers = [1], k = 1
Output: [1]
```

## Prompts

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: c5a19c81-1e98-416e-8bd6-4f32bb9975aa
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

1. We are told that we will be given a non-empty list of input and that `1 ≤ k ≤ number of unique elements`.
    - Since there will always be values in the input list, and `k` will always be valid and less than or equal to the number of unique elements in the list, our function can operate assuming that it will always be able to return a result.

2. The problem statement says that we should return `k` elements, but does not specify a data type. The examples show list syntax (`[]`) for the output.
       - While a tuple or set could work depending on if the result needs to be mutable or if we need to preserve a certain ordering, based on the examples I will return a list. 

3. What if there is a tie for the most frequent elements? E.g., what if k is 3, but there are two values tied for the 3rd most frequent element?
    - Since the problem statement says to return `k` most frequent elements, if there is a tie I will choose the first element found rather than returning all tied elements.

4. Will the input array always be sorted in ascending order?
    - We can write a more general function that processes the input list element by element building a frequency map and that would be fairly efficient for smaller lists. 
    - If we were working with a large input list with many duplicates, that is sorted in ascending order,
      we could find the counts for each value in the list a little differently: 
        1) As we reach an element that is a new value, we could do a binary search on the remainder of the list to find the last index holding that value (the index where the next element is a new number). 
        2) Then we can take the difference of the current index and the last index to get a count for that value update our frequency map, and move to the next number. 

      The notes around the list being large and having repeats is important, if we had a list of only unique elements, this searching approach would not be very efficient. 

5. Must the output list be in a particular order?
    - In the examples, it is unclear if the output is sorted by ordering the most frequent values first or by the order that the values were encountered in the input. Since this problem is concerned with the most frequent values, I will assume that the output should be sorted in desending frequency so that the most freqent item is at the start of the result list. 

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 3b9de43e-7ecf-4f2e-a6f6-5bcc6d70f76d
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

Reviewing the feedback confirmed that most of my observations about the problem were accurate or useful, especially getting clarification around ties, and the ordering of the result list. 

<br>

I received feedback that including implementation-specific details in my observations may be less useful here and distract from clarifying the problem itself. I also learned more about the idea of “stability” when tie breaking for coding problems and how it can be important for some problems to ensure that we always get the same output for a given input. 

<br>

Some additional questions presented were less useful, like whether negative integers are allowed. If they are allowed in the input, it would not change the approach or requirements for this problem space. 

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: afcb3fb9-b225-4d48-b255-b0f3508de237
* title: Write Unit Tests
* topics: pse
##### !question

1. Use the comments provided to write at least two example input/outputs:
    * Consider at least one nominal and one edge case.
    * What is the expected output for the given input?
    * You can use the examples provided in the prompt, or other examples.
2. Write unit tests for `most_frequent_k_elements` for the nominal and edge cases you identified in the first step.

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
def test_most_frequent_k_elements_negative_inputs_succeeds():
    # Arrange
    numbers = [-1, -1, 2, 3, 3, 3]
    k = 2 

    # Act
    result = most_frequent_k_elements(numbers, k)

    # Assert
    assert result == [3, -1]


def test_most_frequent_k_elements_single_element_input_succeeds():
    # Arrange
    numbers = [3]
    k = 1 

    # Act
    result = most_frequent_k_elements(numbers, k)

    # Assert
    assert result == [3]


def test_most_frequent_k_elements_unordered_numbers_succeeds():
    # Arrange
    numbers = [3, 1, 2, 3, 1, 3]
    k = 2 

    # Act
    result = most_frequent_k_elements(numbers, k)

    # Assert
    assert result == [3, 1]
```

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 2df04c34-94fb-45f3-869a-09f96fef5e6b
* title: Create Logical Steps
* topics: pse
##### !question

Without writing code, describe how you would implement `most k frequent elements` using hash tables in enough detail that another developer could reasonably implement a solution. We should capture the main use cases, but the steps do not need to be a detailed plan for every contingency. 
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

1. How could we use a hash/frequency map to keep track of how many times an integer shows up? 
2. Is there a way we could use the frequency map to sort the integers based on their number of occurrences? 

##### !end-hint
#### !explanation

1. Loop over the input list
    - As we loop over the elements, create a hashmap that contains keys for the unique integers in the list mapped to their counts.
2. Create a list of the unique integers from the input and sort the list by their frequency in descending order.
3. Return a list containing the first `k` elements of the new sorted list.

#### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: a4f3a0b5-7a98-42bf-acdb-991eb8121ddc
* title: Review Logical Steps
* topics: pse
##### !question

We want to know if we are laying out an approach to the coding problem that makes sense for our context and if that approach is clearly conveying our thoughts on technical topics to others. Let’s once more use an AI tool like ChatGPT, this time to review the Logical Steps we wrote above. Our goals are to check if:
- the steps make sense for the problem being solved
- the steps are not missing important steps or scenarios
- the steps are agnostic of any particular language – steps should not include code syntax.
- the steps are written with enough detail for another developer to understand how to create a solution

<br>

For this question we will:
1. Build a prompt using [the template linked here](https://gist.githubusercontent.com/ada-instructors/670252696f1625cf0ed77c0997cd165d/raw/pse_logical_steps_review_template.md)
2. Share the completed prompt with an AI tool like ChatGPT
3. After the initial review, ask *at least one* follow up question using the AI tool. We want to ask questions that help us understand: 
    - areas where we could add clarity
    - edge cases we might have missed
    - places where our steps do not meet the expectations of the problem statement
4. Reflect on the information shared by the AI tool and summarize its findings and your learnings

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

The ChatGPT review surfaced some things that would have been helpful to bring forward like clarifying how we're handling ties and generally adding more of the reasoning behind each step for clarity. 

<br>

Some suggestions weren't relevant or were already covered, like a suggestion to "explain what criteria should be used when sorting". The language of that step could be clarified further, but the sorting step states that we are sorting the list of unique integers in descending order using their count.   

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->