# Instructor: Implement Most Frequent K Elements

An example of a working implementation:

```python
def top_k_frequent_elements(arr, k):
    if len(arr) == 1: return [arr[0]]
    
    hash_table = {}
    result = []

    for num in arr:
        if hash_table.get(num, False):
            hash_table[num] += 1
            
        else:
            hash_table[num] = 1
            result.append(num)
            
    i = 0
    while i < len(result) - 1:
        for j in range(len(result) - 1):
            if hash_table[result[j]] < hash_table[result[j+1]]:
                result[j], result[j+1] = result[j+1], result[j]
        i += 1

    return result[:k]
```

