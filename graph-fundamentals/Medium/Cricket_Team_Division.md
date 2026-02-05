# Cricket Team Division

### Problem Statement

The BCCI is organizing a charity cricket match. They have a list of players and their rivalries (players who have had on-field conflicts and refuse to play on the same team). They want to divide all players into two teams such that no two rival players are on the same team.

Given `n` players (numbered 0 to n-1) and their rivalries represented as an adjacency list, determine if it's possible to divide them into two teams where no two players on the same team are rivals.

This is equivalent to checking if the rivalry graph is bipartite - a graph is bipartite if we can color its nodes with two colors such that no two adjacent nodes have the same color.

### Input Format

- First line contains the number of players `n`
- Next `n` lines each describe rivalries for players 0 to n-1
  - Each line starts with `k` (number of rivals), followed by `k` rival player numbers

### Output Format

- Print `true` if the division is possible, `false` otherwise

### Constraints

- `1 <= n <= 100`
- `0 <= graph[i].length < n`
- `graph[u]` does not contain `u` (no self-rivalry)
- If `v` is in `graph[u]`, then `u` is in `graph[v]` (rivalry is mutual)

### Test Cases

#### Test Case 1
**Input:**
```
4
2 1 3
2 0 2
2 1 3
2 0 2
```
**Output:**
```
true
```
**Explanation:** Team A: {0, 2}, Team B: {1, 3}. No rivals on the same team.

---

#### Test Case 2
**Input:**
```
4
3 1 2 3
2 0 2
2 0 1
1 0
```
**Output:**
```
false
```
**Explanation:** Players 0, 1, 2 form a triangle of rivalries. Cannot divide into two teams.

---

#### Test Case 3
**Input:**
```
3
0
0
0
```
**Output:**
```
true
```
**Explanation:** No rivalries, any division works.

---

#### Test Case 4
**Input:**
```
2
1 1
1 0
```
**Output:**
```
true
```
**Explanation:** Just two rivals, put them on different teams.

---

#### Test Case 5
**Input:**
```
5
1 1
2 0 2
2 1 3
2 2 4
1 3
```
**Output:**
```
true
```
**Explanation:** Linear chain: 0-1-2-3-4. Team A: {0, 2, 4}, Team B: {1, 3}.

---

#### Test Case 6
**Input:**
```
5
2 1 4
2 0 2
2 1 3
2 2 4
2 0 3
```
**Output:**
```
false
```
**Explanation:** Odd cycle exists (0-1-2-3-4-0 is length 5). Cannot be bipartite.

---

#### Test Case 7
**Input:**
```
6
1 1
2 0 2
2 1 3
2 2 4
2 3 5
1 4
```
**Output:**
```
true
```
**Explanation:** Linear chain of 6 players. Alternating teams work.

---

### Solutions

#### Python
```python
from collections import deque

class Solution:
    def isBipartite(self, graph: list[list[int]]) -> bool:
        # start your solution
        n = len(graph)
        color = [-1] * n
        
        for start in range(n):
            if color[start] != -1:
                continue
            
            queue = deque([start])
            color[start] = 0
            
            while queue:
                node = queue.popleft()
                
                for neighbor in graph[node]:
                    if color[neighbor] == -1:
                        color[neighbor] = 1 - color[node]
                        queue.append(neighbor)
                    elif color[neighbor] == color[node]:
                        return False
        
        return True
        # end your solution


def main():
    n = int(input())
    graph = []
    for _ in range(n):
        line = list(map(int, input().split()))
        k = line[0]
        neighbors = line[1:k+1] if k > 0 else []
        graph.append(neighbors)
    
    sol = Solution()
    print("true" if sol.isBipartite(graph) else "false")


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
    bool isBipartite(vector<vector<int>>& graph) {
        // start your solution
        int n = graph.size();
        vector<int> color(n, -1);
        
        for (int start = 0; start < n; start++) {
            if (color[start] != -1) continue;
            
            queue<int> q;
            q.push(start);
            color[start] = 0;
            
            while (!q.empty()) {
                int node = q.front();
                q.pop();
                
                for (int neighbor : graph[node]) {
                    if (color[neighbor] == -1) {
                        color[neighbor] = 1 - color[node];
                        q.push(neighbor);
                    } else if (color[neighbor] == color[node]) {
                        return false;
                    }
                }
            }
        }
        
        return true;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<vector<int>> graph(n);
    for (int i = 0; i < n; i++) {
        int k;
        cin >> k;
        for (int j = 0; j < k; j++) {
            int neighbor;
            cin >> neighbor;
            graph[i].push_back(neighbor);
        }
    }
    
    Solution sol;
    cout << (sol.isBipartite(graph) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public boolean isBipartite(int[][] graph) {
        // start your solution
        int n = graph.length;
        int[] color = new int[n];
        Arrays.fill(color, -1);
        
        for (int start = 0; start < n; start++) {
            if (color[start] != -1) continue;
            
            Queue<Integer> queue = new LinkedList<>();
            queue.offer(start);
            color[start] = 0;
            
            while (!queue.isEmpty()) {
                int node = queue.poll();
                
                for (int neighbor : graph[node]) {
                    if (color[neighbor] == -1) {
                        color[neighbor] = 1 - color[node];
                        queue.offer(neighbor);
                    } else if (color[neighbor] == color[node]) {
                        return false;
                    }
                }
            }
        }
        
        return true;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[][] graph = new int[n][];
        for (int i = 0; i < n; i++) {
            int k = sc.nextInt();
            graph[i] = new int[k];
            for (int j = 0; j < k; j++) {
                graph[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.isBipartite(graph) ? "true" : "false");
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
from collections import deque

class Solution:
    def isBipartite(self, graph: list[list[int]]) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    graph = []
    for _ in range(n):
        line = list(map(int, input().split()))
        k = line[0]
        neighbors = line[1:k+1] if k > 0 else []
        graph.append(neighbors)
    
    sol = Solution()
    print("true" if sol.isBipartite(graph) else "false")


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
    bool isBipartite(vector<vector<int>>& graph) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<vector<int>> graph(n);
    for (int i = 0; i < n; i++) {
        int k;
        cin >> k;
        for (int j = 0; j < k; j++) {
            int neighbor;
            cin >> neighbor;
            graph[i].push_back(neighbor);
        }
    }
    
    Solution sol;
    cout << (sol.isBipartite(graph) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public boolean isBipartite(int[][] graph) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[][] graph = new int[n][];
        for (int i = 0; i < n; i++) {
            int k = sc.nextInt();
            graph[i] = new int[k];
            for (int j = 0; j < k; j++) {
                graph[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.isBipartite(graph) ? "true" : "false");
        
        sc.close();
    }
}
```
