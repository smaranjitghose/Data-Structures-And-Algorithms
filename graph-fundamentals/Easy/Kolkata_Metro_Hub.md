# Kolkata Metro Hub

### Problem Statement

The Kolkata Metro Rail Corporation is analyzing their network topology. They have identified a special "star" configuration where one central hub station is directly connected to all other stations, but the other stations are not connected to each other.

Given the connections in this star-shaped metro network, find the central hub station. In a star graph with `n` nodes, there are exactly `n-1` edges, and the center node appears in every edge.

### Input Format

- First line contains the number of edges `e` (which equals n-1 for a star graph)
- Next `e` lines each contain two integers `u v` representing a connection between stations

### Output Format

- A single integer representing the center station number

### Constraints

- `3 <= n <= 10^5`
- `edges.length == n - 1`
- `edges[i].length == 2`
- `1 <= u, v <= n`
- All edges form a valid star graph

### Test Cases

#### Test Case 1
**Input:**
```
3
1 2
2 3
4 2
```
**Output:**
```
2
```
**Explanation:** Station 2 is connected to all other stations (1, 3, 4). It's the hub.

---

#### Test Case 2
**Input:**
```
4
1 2
5 1
1 3
1 4
```
**Output:**
```
1
```
**Explanation:** Station 1 is connected to 2, 3, 4, 5. It's the center.

---

#### Test Case 3
**Input:**
```
2
1 5
5 2
```
**Output:**
```
5
```
**Explanation:** Station 5 connects stations 1 and 2.

---

#### Test Case 4
**Input:**
```
5
3 1
3 2
3 4
3 5
3 6
```
**Output:**
```
3
```
**Explanation:** Station 3 is the central hub connected to all others.

---

#### Test Case 5
**Input:**
```
2
10 20
20 30
```
**Output:**
```
20
```
**Explanation:** Station 20 is in both edges, making it the center.

---

#### Test Case 6
**Input:**
```
6
7 1
7 2
7 3
7 4
7 5
7 6
```
**Output:**
```
7
```
**Explanation:** Station 7 connects to all 6 other stations.

---

#### Test Case 7
**Input:**
```
3
100 200
200 300
200 400
```
**Output:**
```
200
```
**Explanation:** Station 200 appears in all edges.

---

### Solutions

#### Python
```python
class Solution:
    def findCenter(self, edges: list[list[int]]) -> int:
        # start your solution
        # The center must appear in the first two edges
        # Check which node is common in first two edges
        if edges[0][0] == edges[1][0] or edges[0][0] == edges[1][1]:
            return edges[0][0]
        return edges[0][1]
        # end your solution


def main():
    e = int(input())
    edges = []
    for _ in range(e):
        u, v = map(int, input().split())
        edges.append([u, v])
    
    sol = Solution()
    print(sol.findCenter(edges))


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
    int findCenter(vector<vector<int>>& edges) {
        // start your solution
        // The center must appear in the first two edges
        if (edges[0][0] == edges[1][0] || edges[0][0] == edges[1][1]) {
            return edges[0][0];
        }
        return edges[0][1];
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int e;
    cin >> e;
    
    vector<vector<int>> edges(e, vector<int>(2));
    for (int i = 0; i < e; i++) {
        cin >> edges[i][0] >> edges[i][1];
    }
    
    Solution sol;
    cout << sol.findCenter(edges) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int findCenter(int[][] edges) {
        // start your solution
        // The center must appear in the first two edges
        if (edges[0][0] == edges[1][0] || edges[0][0] == edges[1][1]) {
            return edges[0][0];
        }
        return edges[0][1];
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int e = sc.nextInt();
        
        int[][] edges = new int[e][2];
        for (int i = 0; i < e; i++) {
            edges[i][0] = sc.nextInt();
            edges[i][1] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findCenter(edges));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def findCenter(self, edges: list[list[int]]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    e = int(input())
    edges = []
    for _ in range(e):
        u, v = map(int, input().split())
        edges.append([u, v])
    
    sol = Solution()
    print(sol.findCenter(edges))


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
    int findCenter(vector<vector<int>>& edges) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int e;
    cin >> e;
    
    vector<vector<int>> edges(e, vector<int>(2));
    for (int i = 0; i < e; i++) {
        cin >> edges[i][0] >> edges[i][1];
    }
    
    Solution sol;
    cout << sol.findCenter(edges) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int findCenter(int[][] edges) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int e = sc.nextInt();
        
        int[][] edges = new int[e][2];
        for (int i = 0; i < e; i++) {
            edges[i][0] = sc.nextInt();
            edges[i][1] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findCenter(edges));
        
        sc.close();
    }
}
```
