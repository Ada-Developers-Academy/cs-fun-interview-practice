# Instructor: Implement Linked List Intersection

An example of a working implementation:

```python
def intersection_node(head_a, head_b):
    l1, l2 = head_a, head_b
    while l1 != l2:
        l1 = l1.next if l1 else head_b
        l2 = l2.next if l2 else head_a
    return l1
```
