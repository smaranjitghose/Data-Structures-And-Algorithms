# Mango Spoilage Spread

### Problem Statement

During mango season in Ratnagiri, Maharashtra, a farmer stores Alphonso mangoes in a rectangular grid-shaped warehouse. Some mangoes are fresh (value 1), some are already rotten (value 2), and some cells are empty (value 0).

Every minute, any fresh mango that is 4-directionally adjacent (up, down, left, right) to a rotten mango becomes rotten. Determine the minimum number of minutes that must elapse until no fresh mango remains. If it's impossible for all mangoes to rot, return -1.

### Input Format

- First line contains two integers `m` and `n` (grid dimensions)
- Next `m` lines each contain `n` space-separated integers:
  - 0 = empty cell
  - 1 = fresh mango
  - 2 = rotten mango

### Output Format

- A single integer representing minimum minutes, or -1 if impossible

### Constraints

- `1 <= m, n <= 10`
- `grid[i][j]` is 0, 1, or 2

### Test Cases

#### Test Case 1
**Input:**
```
3 3
2 1 1
1 1 0
0 1 1
```
**Output:**
```
4
```
**Explanation:** Rot spreads: minute 1 (adjacent to initial rotten), minute 2, 3, 4 until all fresh mangoes are rotten.

---

#### Test Case 2
**Input:**
```
3 3
2 1 1
0 1 1
1 0 1
```
**Output:**
```
-1
```
**Explanation:** Bottom-left mango (2,0) cannot be reached - isolated by empty cells.

---

#### Test Case 3
**Input:**
```
1 2
0 2
```
**Output:**
```
0
```
**Explanation:** No fresh mangoes exist, answer is 0.

---

#### Test Case 4
**Input:**
```
2 2
2 2
2 2
```
**Output:**
```
0
```
**Explanation:** All mangoes are already rotten.

---

#### Test Case 5
**Input:**
```
3 3
1 1 1
1 1 1
1 1 2
```
**Output:**
```
4
```
**Explanation:** Rot spreads from bottom-right corner, taking 4 minutes to reach top-left.

---

#### Test Case 6
**Input:**
```
3 3
2 0 1
0 0 0
1 0 2
```
**Output:**
```
-1
```
**Explanation:** Fresh mangoes at (0,2) and (2,0) are isolated by empty cells.

---

#### Test Case 7
**Input:**
```
1 5
2 1 1 1 1
```
**Output:**
```
4
```
**Explanation:** Linear spread from left to right takes 4 minutes.

---

### Solutions

#### Python
```python
from collections import deque

class Solution:
    def orangesRotting(self, grid: list[list[int]]) -> int:
        # start your solution
        m, n = len(grid), len(grid[0])
        queue = deque()
        fresh_count = 0
        
        # Find all rotten oranges and count fresh ones
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 2:
                    queue.append((i, j, 0))
                elif grid[i][j] == 1:
                    fresh_count += 1
        
        if fresh_count == 0:
            return 0
        
        directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]
        max_time = 0
        
        while queue:
            r, c, time = queue.popleft()
            
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                if 0 <= nr < m and 0 <= nc < n and grid[nr][nc] == 1:
                    grid[nr][nc] = 2
                    fresh_count -= 1
                    max_time = time + 1
                    queue.append((nr, nc, time + 1))
        
        return max_time if fresh_count == 0 else -1
        # end your solution


def main():
    m, n = map(int, input().split())
    grid = []
    for _ in range(m):
        row = list(map(int, input().split()))
        grid.append(row)
    
    sol = Solution()
    print(sol.orangesRotting(grid))


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
    int orangesRotting(vector<vector<int>>& grid) {
        // start your solution
        int m = grid.size(), n = grid[0].size();
        queue<tuple<int, int, int>> q;
        int freshCount = 0;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) {
                    q.push({i, j, 0});
                } else if (grid[i][j] == 1) {
                    freshCount++;
                }
            }
        }
        
        if (freshCount == 0) return 0;
        
        int directions[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        int maxTime = 0;
        
        while (!q.empty()) {
            auto [r, c, time] = q.front();
            q.pop();
            
            for (auto& dir : directions) {
                int nr = r + dir[0], nc = c + dir[1];
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && grid[nr][nc] == 1) {
                    grid[nr][nc] = 2;
                    freshCount--;
                    maxTime = time + 1;
                    q.push({nr, nc, time + 1});
                }
            }
        }
        
        return freshCount == 0 ? maxTime : -1;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<vector<int>> grid(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid[i][j];
        }
    }
    
    Solution sol;
    cout << sol.orangesRotting(grid) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int orangesRotting(int[][] grid) {
        // start your solution
        int m = grid.length, n = grid[0].length;
        Queue<int[]> queue = new LinkedList<>();
        int freshCount = 0;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) {
                    queue.offer(new int[]{i, j, 0});
                } else if (grid[i][j] == 1) {
                    freshCount++;
                }
            }
        }
        
        if (freshCount == 0) return 0;
        
        int[][] directions = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        int maxTime = 0;
        
        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            int r = curr[0], c = curr[1], time = curr[2];
            
            for (int[] dir : directions) {
                int nr = r + dir[0], nc = c + dir[1];
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && grid[nr][nc] == 1) {
                    grid[nr][nc] = 2;
                    freshCount--;
                    maxTime = time + 1;
                    queue.offer(new int[]{nr, nc, time + 1});
                }
            }
        }
        
        return freshCount == 0 ? maxTime : -1;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[][] grid = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.orangesRotting(grid));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
from collections import deque

class Solution:
    def orangesRotting(self, grid: list[list[int]]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    m, n = map(int, input().split())
    grid = []
    for _ in range(m):
        row = list(map(int, input().split()))
        grid.append(row)
    
    sol = Solution()
    print(sol.orangesRotting(grid))


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
    int orangesRotting(vector<vector<int>>& grid) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<vector<int>> grid(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid[i][j];
        }
    }
    
    Solution sol;
    cout << sol.orangesRotting(grid) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int orangesRotting(int[][] grid) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[][] grid = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.orangesRotting(grid));
        
        sc.close();
    }
}
```
