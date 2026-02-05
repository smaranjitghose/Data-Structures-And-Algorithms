# Kumbh Mela Shortest Path

### Problem Statement

During the Kumbh Mela in Prayagraj, millions of pilgrims gather at the confluence of the Ganga and Yamuna rivers. The event area is organized as an n×n grid where some cells are open for walking (0) and some are blocked by tents, barriers, or restricted zones (1).

A pilgrim needs to travel from the top-left corner (0,0) to the sacred bathing ghat at the bottom-right corner (n-1, n-1). They can move in 8 directions: up, down, left, right, and the four diagonals. Each step counts as one unit of distance.

Find the length of the shortest clear path from top-left to bottom-right. A clear path is one where every cell is open (value 0). If no such path exists, return -1.

### Input Format

- First line contains the grid size `n`
- Next `n` lines each contain `n` space-separated integers (0 or 1)

### Output Format

- A single integer representing the shortest path length, or -1 if no path exists

### Constraints

- `1 <= n <= 100`
- `grid[i][j]` is 0 or 1

### Test Cases

#### Test Case 1
**Input:**
```
3
0 1 0
0 0 0
1 0 0
```
**Output:**
```
4
```
**Explanation:** Path: (0,0) → (1,0) → (1,1) → (2,1) → (2,2), length = 4 cells including start.

---

#### Test Case 2
**Input:**
```
3
0 0 0
1 1 0
1 1 0
```
**Output:**
```
4
```
**Explanation:** Path: (0,0) → (0,1) → (0,2) → (1,2) → (2,2).

---

#### Test Case 3
**Input:**
```
2
1 0
0 0
```
**Output:**
```
-1
```
**Explanation:** Starting cell (0,0) is blocked.

---

#### Test Case 4
**Input:**
```
2
0 0
0 1
```
**Output:**
```
-1
```
**Explanation:** Destination cell (1,1) is blocked.

---

#### Test Case 5
**Input:**
```
1
0
```
**Output:**
```
1
```
**Explanation:** Single cell path, start = destination.

---

#### Test Case 6
**Input:**
```
3
0 0 0
0 0 0
0 0 0
```
**Output:**
```
3
```
**Explanation:** Diagonal path: (0,0) → (1,1) → (2,2), length = 3.

---

#### Test Case 7
**Input:**
```
4
0 0 1 0
1 0 1 0
1 0 0 0
1 1 1 0
```
**Output:**
```
5
```
**Explanation:** Shortest path navigating around obstacles.

---

### Solutions

#### Python
```python
from collections import deque

class Solution:
    def shortestPathBinaryMatrix(self, grid: list[list[int]]) -> int:
        # start your solution
        n = len(grid)
        
        if grid[0][0] == 1 or grid[n-1][n-1] == 1:
            return -1
        
        if n == 1:
            return 1
        
        directions = [(-1, -1), (-1, 0), (-1, 1), (0, -1), (0, 1), (1, -1), (1, 0), (1, 1)]
        
        queue = deque([(0, 0, 1)])
        grid[0][0] = 1  # Mark as visited
        
        while queue:
            r, c, dist = queue.popleft()
            
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                
                if 0 <= nr < n and 0 <= nc < n and grid[nr][nc] == 0:
                    if nr == n - 1 and nc == n - 1:
                        return dist + 1
                    
                    grid[nr][nc] = 1  # Mark as visited
                    queue.append((nr, nc, dist + 1))
        
        return -1
        # end your solution


def main():
    n = int(input())
    grid = []
    for _ in range(n):
        row = list(map(int, input().split()))
        grid.append(row)
    
    sol = Solution()
    print(sol.shortestPathBinaryMatrix(grid))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        // start your solution
        int n = grid.size();
        
        if (grid[0][0] == 1 || grid[n-1][n-1] == 1) {
            return -1;
        }
        
        if (n == 1) {
            return 1;
        }
        
        int directions[8][2] = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
        
        queue<tuple<int, int, int>> q;
        q.push({0, 0, 1});
        grid[0][0] = 1;
        
        while (!q.empty()) {
            auto [r, c, dist] = q.front();
            q.pop();
            
            for (auto& dir : directions) {
                int nr = r + dir[0], nc = c + dir[1];
                
                if (nr >= 0 && nr < n && nc >= 0 && nc < n && grid[nr][nc] == 0) {
                    if (nr == n - 1 && nc == n - 1) {
                        return dist + 1;
                    }
                    
                    grid[nr][nc] = 1;
                    q.push({nr, nc, dist + 1});
                }
            }
        }
        
        return -1;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<vector<int>> grid(n, vector<int>(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid[i][j];
        }
    }
    
    Solution sol;
    cout << sol.shortestPathBinaryMatrix(grid) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int shortestPathBinaryMatrix(int[][] grid) {
        // start your solution
        int n = grid.length;
        
        if (grid[0][0] == 1 || grid[n-1][n-1] == 1) {
            return -1;
        }
        
        if (n == 1) {
            return 1;
        }
        
        int[][] directions = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
        
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{0, 0, 1});
        grid[0][0] = 1;
        
        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            int r = curr[0], c = curr[1], dist = curr[2];
            
            for (int[] dir : directions) {
                int nr = r + dir[0], nc = c + dir[1];
                
                if (nr >= 0 && nr < n && nc >= 0 && nc < n && grid[nr][nc] == 0) {
                    if (nr == n - 1 && nc == n - 1) {
                        return dist + 1;
                    }
                    
                    grid[nr][nc] = 1;
                    queue.offer(new int[]{nr, nc, dist + 1});
                }
            }
        }
        
        return -1;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[][] grid = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.shortestPathBinaryMatrix(grid));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
from collections import deque

class Solution:
    def shortestPathBinaryMatrix(self, grid: list[list[int]]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    grid = []
    for _ in range(n):
        row = list(map(int, input().split()))
        grid.append(row)
    
    sol = Solution()
    print(sol.shortestPathBinaryMatrix(grid))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<vector<int>> grid(n, vector<int>(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid[i][j];
        }
    }
    
    Solution sol;
    cout << sol.shortestPathBinaryMatrix(grid) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int shortestPathBinaryMatrix(int[][] grid) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[][] grid = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.shortestPathBinaryMatrix(grid));
        
        sc.close();
    }
}
```
