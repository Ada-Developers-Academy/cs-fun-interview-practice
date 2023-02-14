# Implement Hamming

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 911f2970
* title: PSE
* points: 3
### !question

Imagine working on software that analyzes mutations in DNA.

Create a function named `hamming_distance` that calculates the number of differences between two DNA strands (aka two strings). This method should take in two different DNA strands of the same length as parameters. This method should have a return value of the number of differences between each string.

For example, given these two DNA strands (strings), `hamming_distance` should return `7` because there are 7 differences:

|Example Input | Expected Ouput |
|--|--|
|`strand1 = "GAGCCTACTAACGGGAT"` <br> `strand2 = "CATCGTAATGACGGCCT"` | `7`|
|`strand1 = "GAG"` <br> `strand2 = "GAG"` | `0`|
|`strand1 = "GAG"` <br> `strand2 = ""`|Raise a ValueError|

(This problem is sourced from http://rosalind.info/problems/hamm/)

### !end-question
### !placeholder

```python
def hamming_distance(strand1, strand2):
    pass
```
### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_counts_correct_number_diffs(self):
        # Arrange
        strand1 = "GAGCCTACTAACGGGAT"
        strand2 = "CATCGTAATGACGGCCT"

        # Act
        result = hamming_distance(strand1, strand2)

        # Assert
        self.assertEqual(result, 7)

    def test_raises_exception_for_different_lengths(self):
        # Arrange
        strand1 = "GAG"
        strand2 = ""

        # Act
        with self.assertRaises(ValueError):
            hamming_distance(strand1, strand2)

    def test_distance_is_zero_for_identical(self):
        # Arrange
        strand1 = "GAG"
        strand2 = "GAG"

        # Act
        result = hamming_distance(strand1, strand2)

        # Assert
        self.assertEqual(result, 0)
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def hamming_distance(strand1, strand2):
    distance = 0

    if len(strand1) != len(strand2):
        raise ValueError("Strands must be the same length")

    for i in range(len(strand1)):
        if strand1[i] != strand2[i]:
            distance += 1

    return distance
```
### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->