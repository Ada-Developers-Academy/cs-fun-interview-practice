# Instructor: Implement Most Frequent K Elements

An example of a working implementation:

```python
# Time Complexity: O(N log(N)) where N is the size of the array
# Space Complexity: O(N) where N is the size of the array
def most_frequent_k_elements(numbers, k):
    if len(numbers) == 1: 
        return [numbers[0]]
    
    frequency_map = {}
    for number in numbers:
        if number in frequency_map:
            frequency_map[number] += 1
        else:
            frequency_map[number] = 1
    
    unique_numbers = list(frequency_map.keys())
    sorted_numbers = sorted(
                unique_numbers, 
                key=lambda num: frequency_map[num], 
                reverse=True
            )

    return sorted_numbers[:k]

# ----- Alternative O(N) solution (provided by Ansel) -----

# assuming we avoid the degenerate pivot case, this will tend towards O(n). the
# following argument assumes we get "good" pivot selection. In this case, the
# maximum number of outer iterations will be log n. during each iteration, we
# halve the number of elements being inspected. The first iteration, we inspect
# all n items. the next, n/2, then n/4, n/8, n/16, etc. The sum of the series of
# halves of n is n, plus the n of the first iteration is 2n, which is O(n).
def select_in_place(el_cnt_arr, k):
    start = 0
    end = len(el_cnt_arr)

    # if fewer than 2 items, there's no need to rearrange
    if end - start < 2:
        return

    # run until the k largest things are at the front of the array
    # (condition is checked internal to the infinite loop and returns when met)
    while True:
        pivot_pos = end - 1  # use final element as the pivot
        _, pivot_cnt = el_cnt_arr[pivot_pos]

        # track the end of the larger array (left), which is the eventual destination
        # of the pivot value
        dest_pos = start

        # compare each value with the pivot, starting at the beginning of the list
        for i in range(start, pivot_pos):
            _, cmp_cnt = el_cnt_arr[i]
            if cmp_cnt > pivot_cnt:
                # higher count than the pivot, so add to the larger array
                el_cnt_arr[dest_pos], el_cnt_arr[i] = el_cnt_arr[i], el_cnt_arr[dest_pos]

                # advance the pivot destination (also the end of the larger list)
                dest_pos += 1

        # move the pivot to its destination
        el_cnt_arr[dest_pos], el_cnt_arr[pivot_pos] = el_cnt_arr[pivot_pos], el_cnt_arr[dest_pos]

        # if we've found k larger things (minus 1 for 0-based index)
        if dest_pos == k-1:
            return
        elif dest_pos < k-1:
            # need more larger items to reach k, and they are to the right of the
            # current pivot destination, so shift start to the right
            start = dest_pos + 1
        else:
            # need fewer larger items to reach k, and they are in the region to
            # the left of the current pivot destination, so shift end to the left
            end = dest_pos
            
def select_top_k(items, k):
    arr_cp = list(items)  # copy (and make sure we even have a list) since we'll work in place
    select_in_place(arr_cp, k)  # make sure the k largest (el, cnt) are at the front
    result = [el for el, _ in arr_cp]  # unpack to just have the values
    return result[:k]  # take the first k

# Time Complexity: O(N) where N is the size of the array
# Space Complexity: O(M) where M is the number of unique integers in a given array (which is N in the worst case)
def most_frequent_k_elements(arr, k):
    if len(arr) == 1: return [arr[0]]
    
    frequency_map = {}
    uniques = []
    # looping through array and creating hash where key value pairs are unique integers and number of occurrences
    for num in arr:
        if num in frequency_map:
            frequency_map[num] += 1
            
        else:
            frequency_map[num] = 1
            uniques.append(num)
            
    # select_top_k tends towards O(n) assuming good pivot selection. though, like
    # quick sort, it could degenerate to O(n^2). unlike the use of sorting, there
    # is no guarantee made as to the order the top k will be returned in.
    result = select_top_k(frequency_map.items(), k)

    # use k to return the k most frequent integers
    return result[:k]

```

