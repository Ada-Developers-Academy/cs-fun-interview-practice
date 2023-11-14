# Instructor: Implement Number of Provinces

Sample clarifying questions:

1. What should be returned for an empty graph?

   While we _could_ raise some sort of error, since we are only asked to return a count (a number) and 0 is a perfectly valid count, we will return 0.
   
2. Will the graph edges always be undirected?

   All of the examples show undirected edges. This matters because depending on the approach for determining the extent of a province, it could look like there are more provinces than there actually are. If a province had all directed edges and we happened to start on a node in the "middle" of the province, we would not be able to get at the nodes "before" this node. This would make it look like there are two provinces when there is actually only one.

3. Will there be self loops in the graph?

   It shouldn't matter whether there are or not. If we encounter a self loop, that would just point us to a node we've already visited, so we would just skip it.

4. What should we do in case of a malformed graph structure?

   No specific error handling was requested, so we can assume that the graph will be well-formed. In practice, we could encounter a jagged matrix, which could result in an `IndexError` when checking neighbors. We could also have values in the matrix that are neither 0 nor 1. Even if we are expecting undirected edges, we could have a matrix that is asymmetric. All of these could cause our implementation to give incorrect results or raise an error. But for now we can focus on the happy path.

An example of a working implementation:

```python
def num_provinces(is_connected):
    num_nodes = len(is_connected)
    provinces = 0

    visited = [0] * num_nodes
    pending = []

    for start_node in range(num_nodes):
        if not visited[start_node]:
            provinces += 1

            pending.append(start_node)
            while pending:
                node = pending.pop()
                if not visited[node]:
                    for next_node in range(num_nodes):
                        if (is_connected[node][next_node]
                                and not visited[next_node]):
                            pending.append(next_node)
                    visited[node] = 1

    return provinces
```

This approach is similar to the iterative DFS implementation presented in Learn. And while Learn gives a time complexity of O(N+E) and space complexity of O(N) for general DFS, the implementation shown here would be O(N^2) time and O(N^2) space. This is because we are using an adjacency matrix, which means that we have to check every node for every other node to see whether there is an edge between them. If we were using an adjacency list, we would only have to check each node's neighbors, resulting in the more typical O(N+E).

If the graph is fully connected, and assuming an "unfortunate" ordering of nodes, rather than O(N), the pending list could grow proportional to O(N^2) as well, even though we would still only "visit" a given node once. Consider that visiting node 1 would result in enqueuing nodes 2 through N, visiting node 2 would result in enqueuing nodes 3 through N, and so on. This would result in a pending list of size (N-1) + (N-2) + ... + 1, which is O(N^2).

In order to avoid quadratic growth of the pending list, we could either use a recursive approach, in which case the stack can grow no larger than O(N), or we could do some additional bookkeeping to ensure duplicate nodes are not in the list. We could switch entirely to a set if we don't particularly care about the iteration order of the pending list (in this case, we don't). Alternatively, we could add an additional set to keep track of nodes we have already seen, and only add nodes to the pending list if they are not already in the set. As with the visited list in this example, since we are working with numeric nodes and we know the number, a simple list can serve this purpose without the additional overhead of a set. The additional tracking data is only O(N) itself, bringing our size complexity back down to O(N) overall.

```python
def num_provinces(is_connected):
    num_nodes = len(is_connected)
    provinces = 0

    visited = [0] * num_nodes
    seen = [0] * num_nodes
    pending = []

    for start_node in range(num_nodes):
        if not visited[start_node]:
            provinces += 1

            pending.append(start_node)
            while pending:
                node = pending.pop()
                if not visited[node]:
                    for next_node in range(num_nodes):
                        if (is_connected[node][next_node]
                                and not visited[next_node]
                                and not seen[next_node]):
                            pending.append(next_node)
                            seen[next_node] = 1
                    visited[node] = 1

    return provinces
```