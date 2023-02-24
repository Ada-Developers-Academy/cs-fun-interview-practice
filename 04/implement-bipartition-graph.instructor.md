# Instructor: Implement Bipartition Graph

An example of a working implementation:

```python
COLORS = ["red", "green"]

def dfs(dislikes, current_node, painted_graph, current_color):
    neighbors = dislikes[current_node]
    next_color = (current_color + 1) % len(COLORS)

    for neighbor in neighbors:
        color = painted_graph.get(neighbor)

        if not color:
            painted_graph[neighbor] = COLORS[next_color]
            if not dfs(dislikes=dislikes, current_node=neighbor, painted_graph=painted_graph, current_color=next_color):
                return False
        elif color != COLORS[next_color]:
            return False
    
    return True
    

def possible_bipartition(dislikes):
    painted_graph = {}
    current_color = 0

    for node in dislikes.keys():
        neighbors = dislikes[node]
        if not painted_graph.get(node):
            painted_graph[node] = COLORS[current_color]

            if not dfs(dislikes=dislikes, current_node=node, painted_graph=painted_graph, current_color=current_color):
                return False
    return True
```
