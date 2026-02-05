# Pilgrimage Route Finder

### Problem Statement

The Char Dham Yatra is one of India's most sacred pilgrimages. A travel agency is developing a route planning system for pilgrims. Given a network of temples and one-way paths between them, they want to find all possible routes from the starting temple (node 0) to the final destination temple (node n-1).

The temple network is represented as a Directed Acyclic Graph (DAG) where `graph[i]` contains all temples directly reachable from temple `i`. Find all possible paths from temple 0 to temple n-1.

### Input Format

- First line contains the number of temples `n`
- Next `n` lines each describe outgoing paths from temples 0 to n-1
  - Each line starts with `k` (number of outgoing paths), followed by `k` destination temples

### Output Format

- Print the number of paths found
- Print each path on a new line as space-separated temple numbers

### Constraints

- `2 <= n <= 15`
- `0 <= graph[i][j] < n`
- `graph[i][j] != i` (no self-loops)
- All elements in `graph[i]` are unique
- The graph is a DAG (no cycles)

### Test Cases

#### Test Case 1
**Input:**
```
4
2 1 2
1 3
1 3
0
```
**Output:**
```
2
0 1 3
0 2 3
```
**Explanation:** Two paths exist: 0→1→3 and 0→2→3.

---

#### Test Case 2
**Input:**
```
5
2 4 3
1 3
1 4
2 2 4
0
```
**Output:**
```
4
0 4
0 3 2 4
0 3 4
0 1 3 2 4
```
**Explanation:** Four different paths from temple 0 to temple 4.

---

#### Test Case 3
**Input:**
```
2
1 1
0
```
**Output:**
```
1
0 1
```
**Explanation:** Direct path from 0 to 1.

---

#### Test Case 4
**Input:**
```
3
1 1
1 2
0
```
**Output:**
```
1
0 1 2
```
**Explanation:** Single linear path 0→1→2.

---

#### Test Case 5
**Input:**
```
4
3 1 2 3
1 3
1 3
0
```
**Output:**
```
3
0 1 3
0 2 3
0 3
```
**Explanation:** Three paths including direct 0→3.

---

#### Test Case 6
**Input:**
```
5
2 1 2
2 2 3
1 4
1 4
0
```
**Output:**
```
3
0 1 2 4
0 1 3 4
0 2 4
```
**Explanation:** Three paths through different intermediate temples.

---

#### Test Case 7
**Input:**
```
3
2 1 2
0
0
```
**Output:**
```
1
0 2
```
**Explanation:** Only path to node 2 is direct from 0.

---

### Solutions

#### Python
```python
class Solution:
    def allPathsSourceTarget(self, graph: list[list[int]]) -> list[list[int]]:
        # start your solution
        n = len(graph)
        result = []
        
        def dfs(node, path):
            if node == n - 1:
                result.append(path[:])
                return
            
            for neighbor in graph[node]:
                path.append(neighbor)
                dfs(neighbor, path)
                path.pop()
        
        dfs(0, [0])
        return result
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
    result = sol.allPathsSourceTarget(graph)
    
    print(len(result))
    for path in result:
        print(" ".join(map(str, path)))


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
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        // start your solution
        int n = graph.size();
        vector<vector<int>> result;
        vector<int> path;
        path.push_back(0);
        
        dfs(graph, 0, n, path, result);
        return result;
    }
    
private:
    void dfs(vector<vector<int>>& graph, int node, int n, vector<int>& path, vector<vector<int>>& result) {
        if (node == n - 1) {
            result.push_back(path);
            return;
        }
        
        for (int neighbor : graph[node]) {
            path.push_back(neighbor);
            dfs(graph, neighbor, n, path, result);
            path.pop_back();
        }
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
    vector<vector<int>> result = sol.allPathsSourceTarget(graph);
    
    cout << result.size() << endl;
    for (auto& path : result) {
        for (int i = 0; i < path.size(); i++) {
            if (i > 0) cout << " ";
            cout << path[i];
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
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        // start your solution
        int n = graph.length;
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        path.add(0);
        
        dfs(graph, 0, n, path, result);
        return result;
    }
    
    private void dfs(int[][] graph, int node, int n, List<Integer> path, List<List<Integer>> result) {
        if (node == n - 1) {
            result.add(new ArrayList<>(path));
            return;
        }
        
        for (int neighbor : graph[node]) {
            path.add(neighbor);
            dfs(graph, neighbor, n, path, result);
            path.remove(path.size() - 1);
        }
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
        List<List<Integer>> result = sol.allPathsSourceTarget(graph);
        
        System.out.println(result.size());
        for (List<Integer> path : result) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < path.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(path.get(i));
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
class Solution:
    def allPathsSourceTarget(self, graph: list[list[int]]) -> list[list[int]]:
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
    result = sol.allPathsSourceTarget(graph)
    
    print(len(result))
    for path in result:
        print(" ".join(map(str, path)))


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
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
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
    vector<vector<int>> result = sol.allPathsSourceTarget(graph);
    
    cout << result.size() << endl;
    for (auto& path : result) {
        for (int i = 0; i < path.size(); i++) {
            if (i > 0) cout << " ";
            cout << path[i];
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
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
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
        List<List<Integer>> result = sol.allPathsSourceTarget(graph);
        
        System.out.println(result.size());
        for (List<Integer> path : result) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < path.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(path.get(i));
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```
