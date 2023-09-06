# Instructor: Implement Most Frequent K Elements

An example of a working implementation:

```python
#Time Complexity: O(N log(N)) where N is the size of the array
# Space Complexity: O(K) where K is the number of unique integers in a given array
def top_k_frequent_elements(arr, k):
    if len(arr) == 1: return [arr[0]]
    
    frequency_map = {}
    uniques = []

    for num in arr:
        if num in frequency_map:
            frequency_map[num] += 1
            
        else:
            frequency_map[num] = 1
            uniques.append(num)
            
   result = sorted(uniques, key=lambda num: frequency_map[num], reverse=True)

    return result[:k]
```

