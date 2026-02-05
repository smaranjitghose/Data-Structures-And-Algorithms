# Kashmir Valley Enclaves

### Problem Statement

The Survey of India is mapping the Kashmir Valley region. The terrain is represented as a 2D grid where '1' represents accessible land and '0' represents impassable mountains or water bodies.

Land cells connected to the boundary of the grid can be accessed from outside the region. However, some land cells are completely surrounded by mountains and cannot be reached from any boundary - these are called "enclaves."

Count the total number of land cells that are enclaves (cannot walk off the grid's boundary in any number of moves by only crossing land cells).

### Input Format

- First line contains two integers `m` and `n` (grid dimensions)
- Next `m` lines each contain `n` space-separated integers (0 or 1)

### Output Format

- A single integer representing the number of enclave cells

### Constraints

- `1 <= m, n <= 500`
- `grid[i][j]` is 0 or 1

### Test Cases

#### Test Case 1
**Input:**
```
4 4
0 0 0 0
1 0 1 0
0 1 1 0
0 0 0 0
```
**Output:**
```
3
```
**Explanation:** The three 1s in the middle cannot reach the boundary.

---

#### Test Case 2
**Input:**
```
4 4
0 1 1 0
0 0 1 0
0 0 1 0
0 0 0 0
```
**Output:**
```
0
```
**Explanation:** All land cells connect to boundary through top row.

---

#### Test Case 3
**Input:**
```
3 3
1 1 1
1 0 1
1 1 1
```
**Output:**
```
0
```
**Explanation:** All land cells touch or connect to the boundary.

---

#### Test Case 4
**Input:**
```
3 3
0 0 0
0 1 0
0 0 0
```
**Output:**
```
1
```
**Explanation:** Single land cell in center is an enclave.

---

#### Test Case 5
**Input:**
```
5 5
0 0 0 0 0
0 1 1 1 0
0 1 0 1 0
0 1 1 1 0
0 0 0 0 0
```
**Output:**
```
8
```
**Explanation:** 8 land cells form a ring, all are enclaves.

---

#### Test Case 6
**Input:**
```
3 4
1 0 0 1
0 1 1 0
1 0 0 1
```
**Output:**
```
2
```
**Explanation:** Only middle 1s at (1,1) and (1,2) are enclaves.

---

#### Test Case 7
**Input:**
```
1 5
1 0 1 0 1
```
**Output:**
```
0
```
**Explanation:** All land cells are on the boundary.

---

### Solutions

#### Python
```python
class Solution:
    def numEnclaves(self, grid: list[list[int]]) -> int:
        # start your solution
        m, n = len(grid), len(grid[0])
        
        def dfs(i, j):
            if i < 0 or i >= m or j < 0 or j >= n or grid[i][j] == 0:
                return
            grid[i][j] = 0
            dfs(i + 1, j)
            dfs(i - 1, j)
            dfs(i, j + 1)
            dfs(i, j - 1)
        
        for i in range(m):
            dfs(i, 0)
            dfs(i, n - 1)
        for j in range(n):
            dfs(0, j)
            dfs(m - 1, j)
        
        count = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 1:
                    count += 1
        
        return count
        # end your solution


def main():
    m, n = map(int, input().split())
    grid = []
    for _ in range(m):
        row = list(map(int, input().split()))
        grid.append(row)
    
    sol = Solution()
    print(sol.numEnclaves(grid))


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
    int numEnclaves(vector<vector<int>>& grid) {
        // start your solution
        int m = grid.size(), n = grid[0].size();
        
        for (int i = 0; i < m; i++) {
            dfs(grid, i, 0, m, n);
            dfs(grid, i, n - 1, m, n);
        }
        for (int j = 0; j < n; j++) {
            dfs(grid, 0, j, m, n);
            dfs(grid, m - 1, j, m, n);
        }
        
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) count++;
            }
        }
        return count;
    }
    
private:
    void dfs(vector<vector<int>>& grid, int i, int j, int m, int n) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == 0) return;
        grid[i][j] = 0;
        dfs(grid, i + 1, j, m, n);
        dfs(grid, i - 1, j, m, n);
        dfs(grid, i, j + 1, m, n);
        dfs(grid, i, j - 1, m, n);
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
    cout << sol.numEnclaves(grid) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int numEnclaves(int[][] grid) {
        // start your solution
        int m = grid.length, n = grid[0].length;
        
        for (int i = 0; i < m; i++) {
            dfs(grid, i, 0, m, n);
            dfs(grid, i, n - 1, m, n);
        }
        for (int j = 0; j < n; j++) {
            dfs(grid, 0, j, m, n);
            dfs(grid, m - 1, j, m, n);
        }
        
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) count++;
            }
        }
        return count;
    }
    
    private void dfs(int[][] grid, int i, int j, int m, int n) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == 0) return;
        grid[i][j] = 0;
        dfs(grid, i + 1, j, m, n);
        dfs(grid, i - 1, j, m, n);
        dfs(grid, i, j + 1, m, n);
        dfs(grid, i, j - 1, m, n);
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
        System.out.println(sol.numEnclaves(grid));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def numEnclaves(self, grid: list[list[int]]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    m, n = map(int, input().split())
    grid = []
    for _ in range(m):
        row = list(map(int, input().split()))
        grid.append(row)
    
    sol = Solution()
    print(sol.numEnclaves(grid))


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
    int numEnclaves(vector<vector<int>>& grid) {
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
    cout << sol.numEnclaves(grid) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int numEnclaves(int[][] grid) {
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
        System.out.println(sol.numEnclaves(grid));
        
        sc.close();
    }
}
```
