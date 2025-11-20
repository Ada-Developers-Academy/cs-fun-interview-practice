# Implement Linked List Intersection

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 2aba725d-bef8-4175-b73b-286c91373494
* title: Linked List Intersection
* points: 3
### !question

Given the heads of two singly linked-lists `head_a` and `head_b`, return the node at which the two lists intersect. If the two linked lists do not intersect, the function should return `None`.

For example, the following two linked lists begin to intersect at the node 8:

![intersecting linked lists example 1](../images/intersection_linked_list_example_1.png)

The following two linked lists do _not_ intersect at all.

![intersecting linked lists example 2](../images/intersection_linked_list_example_2.png)

For this problem, we want to focus on the nodes themselves and not necessarily the *value* inside of the node.

For example, while the following linked lists have tails that share the same values, they are not considered to intersect because the nodes of the linked lists are not the same nodes in memory.

![intersecting linked lists example 3](../images/intersection_linked_list_example_3.png)

There are no cycles anywhere in the linked list structures. Assume any intersection includes the tails of each list.

The linked lists must retain their original structure after the function returns.

### !end-question
### !placeholder

```python
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None

def find_intersecting_node(head_a, head_b):
    """
    Given the heads of two singly linked-lists `head_a` and `head_b`, 
    return the node at which the two lists intersect.
  
    Parameters:
    head_a (Node): head node of list A
    head_b (Node): head node of list B
  
    Returns:
    Node: the node at which list A and list B intersect, 
    or None if they do not intersect.
    """
    pass
```

### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_will_return_intersection_for_lists_of_same_length(self):
        # Arrange
        node_d = Node("D")
        node_e = Node("E")
        node_f = Node("F")

        node_x = Node("X")
        node_y = Node("Y")
        node_z = Node("Z")

        node_one = Node("1")
        node_two = Node("2")
        node_three = Node("3")
        node_one.next = node_two
        node_two.next = node_three

        # List A: ["D", "E", "F", "1", "2", "3"]
        node_d.next = node_e
        node_e.next = node_f
        node_f.next = node_one

        # List B: ["X", "Y", "Z", "1", "2", "3"]
        node_x.next = node_y
        node_y.next = node_z
        node_z.next = node_one

        head_a = node_d
        head_b = node_x

        # Act
        answer = find_intersecting_node(head_a, head_b)

        # Assert
        self.assertEqual(answer, node_one)

    def test_will_return_intersection_with_lists_of_differing_lengths(self):
        # Arrange
        node_d = Node("D")
        node_e = Node("E")
        node_f = Node("F")

        node_x = Node("X")

        node_one = Node("1")
        node_two = Node("2")
        node_three = Node("3")
        node_one.next = node_two
        node_two.next = node_three

        # List A: ["D", "E", "F", "1", "2", "3"]
        node_d.next = node_e
        node_e.next = node_f
        node_f.next = node_one

        # List B: ["X", "1", "2", "3"]
        node_x.next = node_one

        head_a = node_d
        head_b = node_x

        # Act
        answer = find_intersecting_node(head_a, head_b)

        # Assert
        self.assertEqual(answer, node_one)

    def test_will_return_none_with_one_empty_list(self):
        # Arrange
        node_d = Node("D")
        node_e = Node("E")
        node_f = Node("F")

        # List A: ["D", "E", "F"]
        node_d.next = node_e
        node_e.next = node_f

        # List B: [] <-- empty list

        # Act
        answer = find_intersecting_node(node_d, None)

        # Assert
        self.assertEqual(answer, None)

    def test_will_return_none_when_no_intersection(self):
        # Arrange
        node_d = Node("D")
        node_e = Node("E")
        node_f = Node("F")

        node_x = Node("X")
        node_y = Node("Y")
        node_z = Node("Z")

        # List A: ["D", "E", "F"]
        node_d.next = node_e
        node_e.next = node_f

        # List B: ["X", "Y", "Z"]
        node_x.next = node_y
        node_y.next = node_z

        head_a = node_d
        head_b = node_x

        # Act
        answer = find_intersecting_node(head_a, head_b)

        # Assert
        self.assertEqual(answer, None)

    def test_will_return_none_for_two_empty_lists(self):
        # Arrange

        # List A: [] <-- empty list
        # List B: [] <-- empty list

        # Act
        answer = find_intersecting_node(None, None)

        # Assert
        self.assertEqual(answer, None)

    def test_will_return_none_for_tails_with_same_values_but_different_memory_location(self):
        # Arrange
        node_d = Node("D")
        node_e1 = Node("E")
        node_f1 = Node("F")

        node_x = Node("X")
        node_e2 = Node("E")
        node_f2 = Node("F")

        # List A: ["D", "E", "F"]
        node_d.next = node_e1
        node_e1.next = node_f1
        
        # List B:
        node_x.next = node_e2
        node_e2.next = node_f2

        # Act
        answer = find_intersecting_node(node_d, node_x)

        # Assert
        self.assertEqual(answer, None)
```
### !end-tests
### !explanation

Examples of Working Implementations:<br><br>

An initial approach to this problem is to keep track of visited nodes. The solution would traverse the first linked list and store the addresses of the visited nodes in a set and then traverse the second linked list. While traversing the second list, if you encounter an address that already exists in the set then you've identified the intersecting node and can return it.<br><br>

```python
def find_intersecting_node(head_a, head_b):
    # create a set for storing the addresses of the nodes of the first linked list
    nodes = set()

    # traverse the first linked list with a loop and put each node's address in the set
    while head_a:
        nodes.add(id(head_a)) 
        head_a = head_a.next

    # then loop through second linked list and check if each node's address is in the set
    while head_b:
        if id(head_b) in nodes: 
            # if node is in the set, then return that node 
            return head_b
        head_b = head_b.next
    
    # if there is no intersection, return None
    return None
```

***

**Note About id():**<br>
In the solution above, we used the Python `id` function to get the address of each node object. However, in Python, user classes (or developer-created classes) are implicitly hashable which means Python takes their id automatically. It is not necessary or encouraged to use the `id` function in general code, but is done so here for clarity. Therefore, instead of `nodes.add(id(head_a))` we can just write `nodes.add(head_a)` and instead of `if id(head_b) in nodes` and we can just write `if head_b in nodes` and get the same result.<br><br>

The time complexity of the above solution is O(A+B) where A and B are the lengths of the singly linked lists that we access with head_a and head_b. In the worst case scenario, we would need to traverse the first list all the way through to add all the nodes' addresses to the set, and then traverse the second list all the way through to see if an intersection exists.<br><br>

The space complexity of the above solution is O(A), which represents the number of node addresses in the set.

***

Here's another approach to this problem that is more optimal because it does not require an additional data structure to store node addresses, which would bring the space complexity down to O(1). We can traverse the two linked lists with two pointers at the same speed, moving one node forward at a time.<br><br>

When a pointer reaches the end of a linked list, it will be reassigned the value of the head of the other list and continue to traverse the other list. Since the two pointers are moving at the same speed, they will eventually point to the same node (the intersecting node) or `None` at the same time.<br><br>

Example When There is an Intersection:<br>
```text
Two pointers, a and b, will traverse the lists at the same speed moving  
one node at a time.

            a 
list a      1 -> 2 -> 3 ->
                           \
                            > 5 -> 6 -> None
list b                4 -> / 
                      b

                  a
list a      1 -> 2 -> 3 ->
                           \
                            > 5 -> 6 -> None
list b                4 -> /  b

                      a
list a      1 -> 2 -> 3 ->
                           \
                            > 5 -> 6 -> None
list b                4 -> /       b 
Now that pointer b has reached the end of the list, it needs to move to  
the head of list a.

Pointer b is now pointing to the head of list a.    
            b    
list a      1 -> 2 -> 3 ->
                           \  a
                            > 5 -> 6 -> None
list b                4 -> /       

                 b      
list a      1 -> 2 -> 3 ->
                           \       a 
                            > 5 -> 6 -> None
list b                4 -> /     
Now that pointer a has reached the end of the list, it needs to move to  
the head of list b.

                      b      
list a      1 -> 2 -> 3 ->
                           \       
                            > 5 -> 6 -> None
list b                4 -> /   
                      a

                            
list a      1 -> 2 -> 3 ->
                           \  b      
                            > 5 -> 6 -> None
list b                4 -> /  a 
Pointer a and pointer b are now pointing at the same node so we have  
found the intersection and can return the intersecting node.    
```

Example When There is Not an Intersection:<br>
```text
The pointers will cycle through the linked lists until they  
both point to None.

            a
list a      1 -> 2 -> 3 -> 4 -> None
                          
list b      5 -> 6  -> 7 -> None
            b

                 a
list a      1 -> 2 -> 3 -> 4 -> None
                          
list b      5 -> 6  -> 7 -> None
                 b

                      a
list a      1 -> 2 -> 3 -> 4 -> None
                          
list b      5 -> 6  -> 7 -> None
                       b
Now that pointer b has reached the end of the list, it needs to move to  
the head of list a.

Pointer b is now pointing to the head of list a. Pointer a now needs to  
be moved to the head of list b.
            b              a
list a      1 -> 2 -> 3 -> 4 -> None
                          
list b      5 -> 6  -> 7 -> None

Pointer a is now pointing to the head of list b.             
                 b              
list a      1 -> 2 -> 3 -> 4 -> None
                          
list b      5 -> 6  -> 7 -> None
            a

                      b              
list a      1 -> 2 -> 3 -> 4 -> None
                          
list b      5 -> 6  -> 7 -> None
                 a

                           b              
list a      1 -> 2 -> 3 -> 4 -> None
                          
list b      5 -> 6  -> 7 -> None
                       a

                                 b              
list a      1 -> 2 -> 3 -> 4 -> None
                          
list b      5 -> 6  -> 7 -> None
                             a
Pointer a and pointer b are now both pointing at None which means that  
the two linked lists do not have an intersection.
```

***

```python
def find_intersecting_node(head_a, head_b):
    # assign a and b to point to the heads of list A and list B
    a, b = head_a, head_b

    # while a and b do not reference the same node or None
    while a != b:
        # once we've traversed through an entire list, we will set the pointer for the smaller list to the head of the other list
        # on the next iteration of the lists:
        #   if there is NO intersection, both pointers will reach None at the same time.
        #   if there is an intersection, both pointers will reach the intersecting node at the same time.

        # set a to be a.next if a is not None, otherwise set a to be the head of list B 
        a = a.next if a else head_b
        # likewise, set b to be b.next if b is not None, otherwise set b to be the head of list A
        b = b.next if b else head_a
        
    # since a and b are equal, you could return either value, but we'll choose to return a here
    return a
```

The time complexity is O(A + B) where A is the size of list A and B is the size of list B. The loop will traverse through the lists at most twice.<br><br>

The space complexity is O(1) since the space needed for the two additional pointers, a and b, does not scale with the input data.
### !end-explanation

### !end-challenge
<!-- prettier-ignore-end -->

<br>
<details style="max-width: 700px; margin: auto;">
<summary>Click here to see the tests that will be run against your code</summary>

```py
def test_will_return_intersection_for_lists_of_same_length(self):
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    node_x = Node("X")
    node_y = Node("Y")
    node_z = Node("Z")

    node_one = Node("1")
    node_two = Node("2")
    node_three = Node("3")
    node_one.next = node_two
    node_two.next = node_three

    # List A: ["D", "E", "F", "1", "2", "3"]
    node_d.next = node_e
    node_e.next = node_f
    node_f.next = node_one

    # List B: ["X", "Y", "Z", "1", "2", "3"]
    node_x.next = node_y
    node_y.next = node_z
    node_z.next = node_one

    head_a = node_d
    head_b = node_x

    # Act
    answer = find_intersecting_node(head_a, head_b)

    # Assert
    self.assertEqual(answer, node_one)

def test_will_return_intersection_with_lists_of_differing_lengths(self):
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    node_x = Node("X")

    node_one = Node("1")
    node_two = Node("2")
    node_three = Node("3")
    node_one.next = node_two
    node_two.next = node_three

    # List A: ["D", "E", "F", "1", "2", "3"]
    node_d.next = node_e
    node_e.next = node_f
    node_f.next = node_one

    # List B: ["X", "1", "2", "3"]
    node_x.next = node_one

    head_a = node_d
    head_b = node_x

    # Act
    answer = find_intersecting_node(head_a, head_b)

    # Assert
    self.assertEqual(answer, node_one)

def test_will_return_none_with_one_empty_list(self):
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    # List A: ["D", "E", "F"]
    node_d.next = node_e
    node_e.next = node_f

    # List B: [] <-- empty list

    # Act
    answer = find_intersecting_node(node_d, None)

    # Assert
    self.assertEqual(answer, None)

def test_will_return_none_when_no_intersection(self):
    # Arrange
    node_d = Node("D")
    node_e = Node("E")
    node_f = Node("F")

    node_x = Node("X")
    node_y = Node("Y")
    node_z = Node("Z")

    # List A: ["D", "E", "F"]
    node_d.next = node_e
    node_e.next = node_f

    # List B: ["X", "Y", "Z"]
    node_x.next = node_y
    node_y.next = node_z

    head_a = node_d
    head_b = node_x

    # Act
    answer = find_intersecting_node(head_a, head_b)

    # Assert
    self.assertEqual(answer, None)

def test_will_return_none_for_two_empty_lists(self):
    # Arrange

    # List A: [] <-- empty list
    # List B: [] <-- empty list

    # Act
    answer = find_intersecting_node(None, None)

    # Assert
    self.assertEqual(answer, None)

def test_will_return_none_for_tails_with_same_values_but_different_memory_location(self):
    # Arrange
    node_d = Node("D")
    node_e1 = Node("E")
    node_f1 = Node("F")

    node_x = Node("X")
    node_e2 = Node("E")
    node_f2 = Node("F")

    # List A: ["D", "E", "F"]
    node_d.next = node_e1
    node_e1.next = node_f1
    
    # List B:
    node_x.next = node_e2
    node_e2.next = node_f2

    # Act
    answer = find_intersecting_node(node_d, node_x)

    # Assert
    self.assertEqual(answer, None)
```
</details>

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: d0c65caa-97b1-4ffb-8038-33303a412a8f
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
* id: efb51781-bbe5-4a86-9645-6ae1ce49f9f6
* title: Space Complexity of Solution
* points: 1 

##### !question

What is the space complexity of your solution? Please define and explain your variables.

##### !end-question

##### !placeholder

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->