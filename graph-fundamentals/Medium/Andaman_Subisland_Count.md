# Andaman Subisland Count

### Problem Statement

The Indian Navy is comparing two satellite surveys of the Andaman and Nicobar Islands taken at different times. They have two maps (grid1 and grid2) where '1' represents land and '0' represents water.

An island in grid2 is considered a "sub-island" if every land cell of that island in grid2 is also a land cell in grid1 (at the same position). In other words, the island in grid2 must be completely contained within the land of grid1.

Count the number of islands in grid2 that are sub-islands.

### Input Format

- First line contains two integers `m` and `n` (grid dimensions)
- Next `m` lines contain grid1 (n space-separated integers per line)
- Next `m` lines contain grid2 (n space-separated integers per line)

### Output Format

- A single integer representing the number of sub-islands

### Constraints

- `1 <= m, n <= 500`
- `grid1[i][j]` and `grid2[i][j]` are 0 or 1

### Test Cases

#### Test Case 1
**Input:**
```
3 3
1 1 1
0 0 0
1 1 1
1 0 1
0 0 0
1 0 1
```
**Output:**
```
2
```
**Explanation:** Grid2 has 2 islands (top-left+top-right as one, bottom corners). Both are sub-islands of grid1.

---

#### Test Case 2
**Input:**
```
3 3
1 0 1
0 0 0
1 0 1
1 1 1
0 0 0
1 0 1
```
**Output:**
```
1
```
**Explanation:** Top row island in grid2 has cell (0,1) which is water in grid1. Only bottom island qualifies.

---

#### Test Case 3
**Input:**
```
2 2
1 1
1 1
1 1
1 1
```
**Output:**
```
1
```
**Explanation:** Single island in grid2 is completely contained in grid1.

---

#### Test Case 4
**Input:**
```
2 2
0 0
0 0
1 1
1 1
```
**Output:**
```
0
```
**Explanation:** Grid2 has an island, but grid1 has no land. Not a sub-island.

---

#### Test Case 5
**Input:**
```
4 4
1 1 0 0
1 1 0 0
0 0 1 1
0 0 1 1
1 0 0 0
0 0 0 0
0 0 1 0
0 0 0 0
```
**Output:**
```
2
```
**Explanation:** Both single-cell islands in grid2 are sub-islands.

---

#### Test Case 6
**Input:**
```
3 4
1 1 1 0
1 1 1 0
0 0 0 1
1 1 0 0
1 1 0 0
0 0 0 1
```
**Output:**
```
2
```
**Explanation:** Top-left 2x2 island and bottom-right single cell are both sub-islands.

---

#### Test Case 7
**Input:**
```
1 5
1 0 1 0 1
1 0 0 0 1
```
**Output:**
```
2
```
**Explanation:** Two islands in grid2 (positions 0 and 4) are sub-islands. Middle cell in grid2 is 0.

---

### Solutions

#### Python
```python
class Solution:
    def countSubIslands(self, grid1: list[list[int]], grid2: list[list[int]]) -> int:
        # start your solution
        m, n = len(grid1), len(grid1[0])
        
        def dfs(i, j):
            if i < 0 or i >= m or j < 0 or j >= n or grid2[i][j] == 0:
                return True
            
            grid2[i][j] = 0
            is_sub = grid1[i][j] == 1
            
            is_sub = dfs(i + 1, j) and is_sub
            is_sub = dfs(i - 1, j) and is_sub
            is_sub = dfs(i, j + 1) and is_sub
            is_sub = dfs(i, j - 1) and is_sub
            
            return is_sub
        
        count = 0
        for i in range(m):
            for j in range(n):
                if grid2[i][j] == 1:
                    if dfs(i, j):
                        count += 1
        
        return count
        # end your solution


def main():
    m, n = map(int, input().split())
    grid1 = []
    for _ in range(m):
        row = list(map(int, input().split()))
        grid1.append(row)
    grid2 = []
    for _ in range(m):
        row = list(map(int, input().split()))
        grid2.append(row)
    
    sol = Solution()
    print(sol.countSubIslands(grid1, grid2))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    int countSubIslands(vector<vector<int>>& grid1, vector<vector<int>>& grid2) {
        // start your solution
        int m = grid1.size(), n = grid1[0].size();
        int count = 0;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid2[i][j] == 1) {
                    if (dfs(grid1, grid2, i, j, m, n)) {
                        count++;
                    }
                }
            }
        }
        
        return count;
    }
    
private:
    bool dfs(vector<vector<int>>& grid1, vector<vector<int>>& grid2, int i, int j, int m, int n) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid2[i][j] == 0) {
            return true;
        }
        
        grid2[i][j] = 0;
        bool isSub = (grid1[i][j] == 1);
        
        isSub = dfs(grid1, grid2, i + 1, j, m, n) && isSub;
        isSub = dfs(grid1, grid2, i - 1, j, m, n) && isSub;
        isSub = dfs(grid1, grid2, i, j + 1, m, n) && isSub;
        isSub = dfs(grid1, grid2, i, j - 1, m, n) && isSub;
        
        return isSub;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<vector<int>> grid1(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid1[i][j];
        }
    }
    
    vector<vector<int>> grid2(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid2[i][j];
        }
    }
    
    Solution sol;
    cout << sol.countSubIslands(grid1, grid2) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int countSubIslands(int[][] grid1, int[][] grid2) {
        // start your solution
        int m = grid1.length, n = grid1[0].length;
        int count = 0;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid2[i][j] == 1) {
                    if (dfs(grid1, grid2, i, j, m, n)) {
                        count++;
                    }
                }
            }
        }
        
        return count;
    }
    
    private boolean dfs(int[][] grid1, int[][] grid2, int i, int j, int m, int n) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid2[i][j] == 0) {
            return true;
        }
        
        grid2[i][j] = 0;
        boolean isSub = (grid1[i][j] == 1);
        
        isSub = dfs(grid1, grid2, i + 1, j, m, n) && isSub;
        isSub = dfs(grid1, grid2, i - 1, j, m, n) && isSub;
        isSub = dfs(grid1, grid2, i, j + 1, m, n) && isSub;
        isSub = dfs(grid1, grid2, i, j - 1, m, n) && isSub;
        
        return isSub;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[][] grid1 = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid1[i][j] = sc.nextInt();
            }
        }
        
        int[][] grid2 = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid2[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.countSubIslands(grid1, grid2));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def countSubIslands(self, grid1: list[list[int]], grid2: list[list[int]]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    m, n = map(int, input().split())
    grid1 = []
    for _ in range(m):
        row = list(map(int, input().split()))
        grid1.append(row)
    grid2 = []
    for _ in range(m):
        row = list(map(int, input().split()))
        grid2.append(row)
    
    sol = Solution()
    print(sol.countSubIslands(grid1, grid2))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    int countSubIslands(vector<vector<int>>& grid1, vector<vector<int>>& grid2) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<vector<int>> grid1(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid1[i][j];
        }
    }
    
    vector<vector<int>> grid2(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid2[i][j];
        }
    }
    
    Solution sol;
    cout << sol.countSubIslands(grid1, grid2) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int countSubIslands(int[][] grid1, int[][] grid2) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[][] grid1 = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid1[i][j] = sc.nextInt();
            }
        }
        
        int[][] grid2 = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid2[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.countSubIslands(grid1, grid2));
        
        sc.close();
    }
}
```
