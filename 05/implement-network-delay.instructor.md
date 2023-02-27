# Instructor: Implement Network Delay

An example of a working implementation:

```python
def network_delay(times, n, source):
    # Initialize dictionary with default value as a list
    graph = collections.defaultdict(list)
    # For each edge in the graph, add the neighbors for a node to the graph
    # such that graph[node] = [(neighbor1, time1), (neighbor2, time2)...]
    # The graph is directed, so we only need to append one direction
    for u, v, time in times:
        graph[u].append([v, time])

    # initialize the time needed to reach each node in the graph, overestimating to infinity
    time_needed = [float('inf')] * n
    # set the time to reach the source node to 0
    time_needed[source-1] = 0
    # initialize min heap for traversal
    # priority 0 to travel to the source node
    heap = [[0, source]] 

    visited = set() # used to record all visited nodes
    visited.add(source)

    # while there are nodes in the heap
    while heap:
        # pop off the closest node
        time, curr_node = heappop(heap)
        # traverse through the current node's neighbors
        for neighbor, neighbor_time in graph[curr_node]:
            # calculate the total time to travel to the neighbor
            total_time = time + neighbor_time
            # if the total time is less than the previous time stored to travel to the neighbor
            if total_time < time_needed[neighbor - 1]:
                # store the total time as the time needed to travel to the neighbor
                time_needed[neighbor - 1] = total_time
                # add the node to the list of visited nodes
                visited.add(neighbor)
                # push onto heap to be visited later
                heappush(heap, [total_time, neighbor])

    # return the max time in time_needed list if all of the nodes have been visited, otherwise return -1
    return max(time_needed) if len(visited) == n else -1
```
