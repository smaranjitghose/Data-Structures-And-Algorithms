# State District Grouping

### Problem Statement

The Ministry of Home Affairs is reorganizing administrative divisions across India. They have data showing which districts are directly connected (share a border). A "province" is defined as a group of districts where each district is connected to at least one other district in the group, either directly or through other districts.

Given an `n x n` adjacency matrix where `isConnected[i][j] = 1` indicates district `i` and district `j` are directly connected, and `isConnected[i][j] = 0` otherwise, find the total number of provinces.

Note: A district is always connected to itself, so `isConnected[i][i] = 1`.

### Input Format

- First line contains the number of districts `n`
- Next `n` lines each contain `n` space-separated integers (0 or 1) representing the adjacency matrix

### Output Format

- A single integer representing the number of provinces

### Constraints

- `1 <= n <= 200`
- `isConnected[i][i] == 1`
- `isConnected[i][j] == isConnected[j][i]`

### Test Cases

#### Test Case 1
**Input:**
```
3
1 1 0
1 1 0
0 0 1
```
**Output:**
```
2
```
**Explanation:** Districts 0 and 1 are connected (Province 1). District 2 is isolated (Province 2).

---

#### Test Case 2
**Input:**
```
3
1 0 0
0 1 0
0 0 1
```
**Output:**
```
3
```
**Explanation:** No districts are connected. Each is its own province.

---

#### Test Case 3
**Input:**
```
3
1 1 1
1 1 1
1 1 1
```
**Output:**
```
1
```
**Explanation:** All districts are interconnected. One province.

---

#### Test Case 4
**Input:**
```
1
1
```
**Output:**
```
1
```
**Explanation:** Single district, single province.

---

#### Test Case 5
**Input:**
```
4
1 1 0 0
1 1 0 0
0 0 1 1
0 0 1 1
```
**Output:**
```
2
```
**Explanation:** Districts {0,1} form one province, {2,3} form another.

---

#### Test Case 6
**Input:**
```
5
1 0 0 0 0
0 1 1 0 0
0 1 1 0 0
0 0 0 1 1
0 0 0 1 1
```
**Output:**
```
3
```
**Explanation:** Three provinces: {0}, {1,2}, {3,4}.

---

#### Test Case 7
**Input:**
```
6
1 1 0 0 0 0
1 1 1 0 0 0
0 1 1 0 0 0
0 0 0 1 1 0
0 0 0 1 1 1
0 0 0 0 1 1
```
**Output:**
```
2
```
**Explanation:** Two provinces: {0,1,2} and {3,4,5}.

---

### Solutions

#### Python
```python
class Solution:
    def findCircleNum(self, isConnected: list[list[int]]) -> int:
        # start your solution
        n = len(isConnected)
        visited = [False] * n
        provinces = 0
        
        def dfs(district):
            visited[district] = True
            for neighbor in range(n):
                if isConnected[district][neighbor] == 1 and not visited[neighbor]:
                    dfs(neighbor)
        
        for i in range(n):
            if not visited[i]:
                provinces += 1
                dfs(i)
        
        return provinces
        # end your solution


def main():
    n = int(input())
    isConnected = []
    for _ in range(n):
        row = list(map(int, input().split()))
        isConnected.append(row)
    
    sol = Solution()
    print(sol.findCircleNum(isConnected))


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
    int findCircleNum(vector<vector<int>>& isConnected) {
        // start your solution
        int n = isConnected.size();
        vector<bool> visited(n, false);
        int provinces = 0;
        
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                provinces++;
                dfs(isConnected, visited, i, n);
            }
        }
        
        return provinces;
    }
    
private:
    void dfs(vector<vector<int>>& isConnected, vector<bool>& visited, int district, int n) {
        visited[district] = true;
        for (int neighbor = 0; neighbor < n; neighbor++) {
            if (isConnected[district][neighbor] == 1 && !visited[neighbor]) {
                dfs(isConnected, visited, neighbor, n);
            }
        }
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<vector<int>> isConnected(n, vector<int>(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> isConnected[i][j];
        }
    }
    
    Solution sol;
    cout << sol.findCircleNum(isConnected) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int findCircleNum(int[][] isConnected) {
        // start your solution
        int n = isConnected.length;
        boolean[] visited = new boolean[n];
        int provinces = 0;
        
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                provinces++;
                dfs(isConnected, visited, i, n);
            }
        }
        
        return provinces;
    }
    
    private void dfs(int[][] isConnected, boolean[] visited, int district, int n) {
        visited[district] = true;
        for (int neighbor = 0; neighbor < n; neighbor++) {
            if (isConnected[district][neighbor] == 1 && !visited[neighbor]) {
                dfs(isConnected, visited, neighbor, n);
            }
        }
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[][] isConnected = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                isConnected[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findCircleNum(isConnected));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def findCircleNum(self, isConnected: list[list[int]]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    isConnected = []
    for _ in range(n):
        row = list(map(int, input().split()))
        isConnected.append(row)
    
    sol = Solution()
    print(sol.findCircleNum(isConnected))


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
    int findCircleNum(vector<vector<int>>& isConnected) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<vector<int>> isConnected(n, vector<int>(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> isConnected[i][j];
        }
    }
    
    Solution sol;
    cout << sol.findCircleNum(isConnected) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int findCircleNum(int[][] isConnected) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[][] isConnected = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                isConnected[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findCircleNum(isConnected));
        
        sc.close();
    }
}
```
