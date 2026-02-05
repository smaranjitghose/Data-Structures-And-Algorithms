# Temple Exit Distance

### Problem Statement

The Meenakshi Temple in Madurai has a complex layout with multiple corridors, walls, and exit gates. Temple authorities want to help devotees find the nearest exit from any location within the temple.

The temple floor plan is represented as a 2D grid where:
- `-1` represents a wall or pillar (impassable)
- `0` represents an exit gate
- `2147483647` (INF) represents an empty corridor

Fill each empty corridor cell with the distance to its nearest exit gate. If it's impossible to reach any gate from a cell, leave it as INF. Distance is measured in steps (4-directional movement: up, down, left, right).

### Input Format

- First line contains two integers `m` and `n` (grid dimensions)
- Next `m` lines each contain `n` space-separated integers:
  - -1 = wall
  - 0 = exit gate
  - 2147483647 = empty corridor (INF)

### Output Format

- Print the modified grid with `m` lines, each containing `n` space-separated integers

### Constraints

- `1 <= m, n <= 250`
- `grid[i][j]` is -1, 0, or 2147483647

### Test Cases

#### Test Case 1
**Input:**
```
4 4
2147483647 -1 0 2147483647
2147483647 2147483647 2147483647 -1
2147483647 -1 2147483647 -1
0 -1 2147483647 2147483647
```
**Output:**
```
3 -1 0 1
2 2 1 -1
1 -1 2 -1
0 -1 3 4
```
**Explanation:** Each empty cell shows distance to nearest gate.

---

#### Test Case 2
**Input:**
```
2 2
0 2147483647
2147483647 2147483647
```
**Output:**
```
0 1
1 2
```
**Explanation:** Single gate at (0,0), distances spread from there.

---

#### Test Case 3
**Input:**
```
2 2
-1 -1
-1 -1
```
**Output:**
```
-1 -1
-1 -1
```
**Explanation:** All walls, no changes needed.

---

#### Test Case 4
**Input:**
```
1 4
0 2147483647 2147483647 0
```
**Output:**
```
0 1 1 0
```
**Explanation:** Two gates, middle cells are 1 step from nearest gate.

---

#### Test Case 5
**Input:**
```
3 3
0 0 0
0 2147483647 0
0 0 0
```
**Output:**
```
0 0 0
0 1 0
0 0 0
```
**Explanation:** Center cell is 1 step from any surrounding gate.

---

#### Test Case 6
**Input:**
```
3 3
2147483647 -1 2147483647
-1 -1 -1
2147483647 -1 0
```
**Output:**
```
2147483647 -1 2147483647
-1 -1 -1
2147483647 -1 0
```
**Explanation:** Top-left and top-right cells can't reach the gate due to walls.

---

#### Test Case 7
**Input:**
```
3 4
2147483647 2147483647 0 2147483647
2147483647 2147483647 2147483647 2147483647
0 2147483647 2147483647 2147483647
```
**Output:**
```
2 1 0 1
1 2 1 2
0 1 2 3
```
**Explanation:** Two gates, each cell gets distance to nearest.

---

### Solutions

#### Python
```python
from collections import deque

class Solution:
    def wallsAndGates(self, rooms: list[list[int]]) -> None:
        # start your solution
        if not rooms:
            return
        
        m, n = len(rooms), len(rooms[0])
        INF = 2147483647
        queue = deque()
        
        # Find all gates
        for i in range(m):
            for j in range(n):
                if rooms[i][j] == 0:
                    queue.append((i, j))
        
        directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]
        
        while queue:
            r, c = queue.popleft()
            
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                if 0 <= nr < m and 0 <= nc < n and rooms[nr][nc] == INF:
                    rooms[nr][nc] = rooms[r][c] + 1
                    queue.append((nr, nc))
        # end your solution


def main():
    m, n = map(int, input().split())
    rooms = []
    for _ in range(m):
        row = list(map(int, input().split()))
        rooms.append(row)
    
    sol = Solution()
    sol.wallsAndGates(rooms)
    
    for row in rooms:
        print(" ".join(map(str, row)))


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
    void wallsAndGates(vector<vector<int>>& rooms) {
        // start your solution
        if (rooms.empty()) return;
        
        int m = rooms.size(), n = rooms[0].size();
        int INF = 2147483647;
        queue<pair<int, int>> q;
        
        // Find all gates
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (rooms[i][j] == 0) {
                    q.push({i, j});
                }
            }
        }
        
        int directions[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        
        while (!q.empty()) {
            auto [r, c] = q.front();
            q.pop();
            
            for (auto& dir : directions) {
                int nr = r + dir[0], nc = c + dir[1];
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && rooms[nr][nc] == INF) {
                    rooms[nr][nc] = rooms[r][c] + 1;
                    q.push({nr, nc});
                }
            }
        }
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<vector<int>> rooms(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> rooms[i][j];
        }
    }
    
    Solution sol;
    sol.wallsAndGates(rooms);
    
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (j > 0) cout << " ";
            cout << rooms[i][j];
        }
        cout << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public void wallsAndGates(int[][] rooms) {
        // start your solution
        if (rooms == null || rooms.length == 0) return;
        
        int m = rooms.length, n = rooms[0].length;
        int INF = 2147483647;
        Queue<int[]> queue = new LinkedList<>();
        
        // Find all gates
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (rooms[i][j] == 0) {
                    queue.offer(new int[]{i, j});
                }
            }
        }
        
        int[][] directions = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        
        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            int r = curr[0], c = curr[1];
            
            for (int[] dir : directions) {
                int nr = r + dir[0], nc = c + dir[1];
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && rooms[nr][nc] == INF) {
                    rooms[nr][nc] = rooms[r][c] + 1;
                    queue.offer(new int[]{nr, nc});
                }
            }
        }
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[][] rooms = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                rooms[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        sol.wallsAndGates(rooms);
        
        for (int i = 0; i < m; i++) {
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < n; j++) {
                if (j > 0) sb.append(" ");
                sb.append(rooms[i][j]);
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
from collections import deque

class Solution:
    def wallsAndGates(self, rooms: list[list[int]]) -> None:
        # start your solution
        
        
        
        # end your solution


def main():
    m, n = map(int, input().split())
    rooms = []
    for _ in range(m):
        row = list(map(int, input().split()))
        rooms.append(row)
    
    sol = Solution()
    sol.wallsAndGates(rooms)
    
    for row in rooms:
        print(" ".join(map(str, row)))


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
    void wallsAndGates(vector<vector<int>>& rooms) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<vector<int>> rooms(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> rooms[i][j];
        }
    }
    
    Solution sol;
    sol.wallsAndGates(rooms);
    
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (j > 0) cout << " ";
            cout << rooms[i][j];
        }
        cout << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public void wallsAndGates(int[][] rooms) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[][] rooms = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                rooms[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        sol.wallsAndGates(rooms);
        
        for (int i = 0; i < m; i++) {
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < n; j++) {
                if (j > 0) sb.append(" ");
                sb.append(rooms[i][j]);
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```
