# Minimum-Height-Trees
A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree. 

class Solution:
  def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
    if n == 1 or not edges:
      return [0]

    ans = []
    graph = collections.defaultdict(set)

    for u, v in edges:
      graph[u].add(v)
      graph[v].add(u)

    for label, children in graph.items():
      if len(children) == 1:
        ans.append(label)

    while n > 2:
      n -= len(ans)
      nextLeaves = []
      for leaf in ans:
        u = next(iter(graph[leaf]))
        graph[u].remove(leaf)
        if len(graph[u]) == 1:
          nextLeaves.append(u)
      ans = nextLeaves

    return ans
