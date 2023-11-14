# Instructor: Implement Network Delay

Sample clarifying questions:

Note that for strictly defined challenges, there may not be many points that feel unclear from a specification perspective. However, we can still take the opportunity for clarification to consider what the impact of certain requirements we have been given will have on our implementation. Don't hesitate to observe something that has been specified, restate it in your own words to show your understanding, then go on to postulate why that information was given and how it might impact your approach.

1. In which way is the graph being represented?

   From the parameter descriptions, `times` is described as a list whose elements represented directed edges of the format `(from, to, cost)`. This means the supplied graph representation is expected to take the form of a list of edges, which we are also able to verify from the examples.

   Observing this is useful, as it lets us consider whether we want to convert the list of edges into some other format that will allow us to approach the challenge more efficiently overall. In this case, we know that we'll need to efficiently iterate over the neighbors of a given node, so we'll want to convert the list of edges into an adjacency dict, allowing us to look up the neighbors using the node value as the key.

2. Do the nodes start at 0 or 1?

   The problem defines the nodes as being labeled from 1 to n, and the examples support this, showing nodes starting at 1. So we will work with this as a requirement.

   This is useful to consider as it impacts how we relate our node data (1-based) to supplemental data (such as the total cost list, or potentially a previous list if we were asked to return path data). If we use a list to track the total cost to reach each node, we'll need to be careful about how we index into the list, either adjusting the node value to be 0-based or inserting a dummy value to effectively make the list 1-based. In the latter case, we would also need to ensure that the dummy value didn't interfere with our logic for determining the maximum cost.

3. Will the graph ever be empty? What should the result be?

   Since the data is being presented as a list of edges, there is a dta configuration that might feel like a natural representation of an empty graph (a graph having neither nodes nor edges): an empty list. However, technically, we can really only tell that there are no edges in such a graph. There could be any number of nodes, simple that share no edges. So we can't really tell whether the graph is empty or not. That is, we cannot tell the difference between a graph with no nodes and a graph with potentially many unconnected nodes.
   
   However, we are also given the count of nodes int he graph as a separate input, which does allow us to differentiate. A truly empty graph will have an empty list of edges and a count of zero nodes. A graph with no edges will have an empty list of edges and a count of some non-zero number of nodes.

   The problem statement does not specify what should be returned in the case of an empty graph, though it does stipulate the behavior if there are unreachable nodes (and edgeless graph trivially would have unreachable nodes). So we can infer that for an edgeless graph, we should return -1 (the same result for a graph with unreachable nodes). For a truly empty graph, we consider what should the reported maximum delay across nodes be when there are no nodes? A fair argument could be made for several values, including 0, -1, or even `float('inf')`.
   
   However, since the problem statement does not specify a behavior (there are no examples), unless we encounter a test that expressly tests for this case, we can assume that we will not be asked to handle it. In practice, we would want to clarify this with the interviewer, and account for it in our implementation.

4. Will the graph edges always be directed?

   The prompt reports that the data in the edge list represent directed edges, so we will assume that is the intended interpretation throughout.

   Noting whether edges in an edge list are directed or undirected is important because it impacts how we construct the adjacency dict. If the edges are undirected, we will need to add both directions to the adjacency dict. If the edges are directed, we only need to add one direction.

5. What if there are duplicate edges in the list?

   Logically, this shouldn't present a problem for converting from the edge list to an adjacency dict. There are many cases where there could be multiple edges between nodes in a graph. However, the problem statement does not specify how we should handle duplicate edges. Does it make sense for _this_ case?

   In the absence of any specific guidance, we'll naïvely plan to process them as usual (Dijkstra isn't bothered by this situation). However, we should be prepared to discuss this with the interviewer, and potentially handle it in our implementation.

6. What should we do in case of malformed graph data?

   Our implementation will make specific assumptions about the structure of the edge list and the defined number of nodes. What if the edge data wasn't consistently formatted? What if an edge referred to an invalid node? What if the edge data cost contained negative values? What if the edge data contained non-numeric values?

   No specific error handling was requested, so we can assume that the graph will be well-formed. In practice we would at the least want to consider what behavior our implementation would exhibit when faced with various kinds of "invalid" data. In the time constraints of an interview, we often focus on good data (unless there are specific requirements to the contrary). Situations to pay particular attention to are cases where silently "handling" bad data may lead to a result that is incorrect but not obviously so. Sometimes outright crashing (or at least detecting and raising an error) is the best option.

An example of a working implementation:

```python
import collections
from heapq import heappush, heappop
def network_delay_time(times, n, source):
    # Initialize dictionary with default value as a list
    graph = collections.defaultdict(list)
    # For each edge in the graph, add the neighbors for a node to the graph
    # such that graph[node] = [(neighbor1, time1), (neighbor2, time2)...]
    # The graph is directed, so we only need to append one direction
    for u, v, time in times:
        graph[u].append((v, time))

    # initialize the time needed to reach each node in the graph, overestimating to infinity
    time_needed = [float('inf')] * n
    # set the time to reach the source node to 0
    time_needed[source-1] = 0
    # initialize min heap for traversal
    # priority 0 to travel to the source node
    heap = [(0, source)] 

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
                heappush(heap, (total_time, neighbor))

    # return the max time in time_needed list if all of the nodes have been visited, otherwise return -1
    return max(time_needed) if len(visited) == n else -1
```
