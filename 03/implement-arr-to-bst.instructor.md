# Instructor: Implement Array-to-BST

An example of a working implementation:

```python
class TreeNode:
    def __init__(self, value, left = None, right = None):
        self.val = value
        self.left = left
        self.right = right


def arr_to_bst(arr):
    if not arr:
        return None

    mid = (len(arr)) // 2

    root = TreeNode(arr[mid])
    root.left = arr_to_bst(arr[:mid])
    root.right = arr_to_bst(arr[mid + 1:])
    return root
```
