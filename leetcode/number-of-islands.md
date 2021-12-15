---
description: >-
  Given an m x n 2D binary grid grid which represents a map of '1's (land) and
  '0's (water), return the number of islands.An island is surrounded by water
  and is formed by connecting adjacent lands ho
---

# Number of Islands

```
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid:
            return 0
        self.island_count = 0;
        for i in range(len(grid)):
            for j in range(len(grid[i])):
                if grid[i][j] == "1":
                    self.island_count += 1
                    self.bfs(grid, i, j)
        return self.island_count
    def bfs(self, grid, i, j):
        queue = []
        queue.append((i, j))
        while queue:
            length = len(queue)
            for _ in range(length):
                x, y = queue.pop()
                grid[x][y] = "0"
                if x - 1 >= 0 and grid[x - 1][y] == "1":
                    queue.append((x - 1, y))
                if x + 1 < len(grid) and grid[x + 1][y] == "1":
                    queue.append((x + 1, y))
                if y - 1 >= 0 and grid[x][y - 1] == "1":
                    queue.append((x, y - 1))
                if y + 1 < len(grid[0]) and grid[x][y + 1] == "1":
                    queue.append((x, y + 1))
```
