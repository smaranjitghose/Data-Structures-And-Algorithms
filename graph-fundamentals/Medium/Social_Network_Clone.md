# Social Network Clone

### Problem Statement

A tech startup in Bengaluru is building a backup system for their social network. They need to create an exact deep copy of their user connection graph. Each user (node) has a unique ID and a list of friends (neighbors).

Given a reference to a user in a connected undirected graph, return a deep copy (clone) of the entire network. Each node contains an integer value and a list of its neighbors.

The clone should be a completely new graph structure where:
- Each cloned node has the same value as the original
- Neighbor relationships are preserved in the clone
- No node in the clone references any node in the original graph

### Input Format

- First line contains the number of users `n`
- Next `n` lines each describe the adjacency list for users 1 to n
  - Each line contains space-separated neighbor IDs (or empty if no neighbors)
- The graph is always connected

### Output Format

- Print `n` lines, each showing the adjacency list of the cloned graph
- Each line: user ID followed by colon, then space-separated neighbor IDs in sorted order

### Constraints

- `1 <= n <= 100`
- `1 <= Node.val <= 100`
- Node values are unique
- No self-loops or duplicate edges

### Test Cases

#### Test Case 1
**Input:**
```
4
2 4
1 3
2 4
1 3
```
**Output:**
```
1: 2 4
2: 1 3
3: 2 4
4: 1 3
```
**Explanation:** User 1 connects to 2,4. User 2 connects to 1,3. And so on. Clone preserves all connections.

---

#### Test Case 2
**Input:**
```
1

```
**Output:**
```
1:
```
**Explanation:** Single user with no friends.

---

#### Test Case 3
**Input:**
```
2
2
1
```
**Output:**
```
1: 2
2: 1
```
**Explanation:** Two users connected to each other.

---

#### Test Case 4
**Input:**
```
3
2 3
1 3
1 2
```
**Output:**
```
1: 2 3
2: 1 3
3: 1 2
```
**Explanation:** Triangle graph - everyone knows everyone.

---

#### Test Case 5
**Input:**
```
5
2
1 3
2 4
3 5
4
```
**Output:**
```
1: 2
2: 1 3
3: 2 4
4: 3 5
5: 4
```
**Explanation:** Linear chain of friends.

---

#### Test Case 6
**Input:**
```
4
2 3 4
1
1
1
```
**Output:**
```
1: 2 3 4
2: 1
3: 1
4: 1
```
**Explanation:** Star graph with user 1 at center.

---

#### Test Case 7
**Input:**
```
6
2 6
1 3
2 4
3 5
4 6
1 5
```
**Output:**
```
1: 2 6
2: 1 3
3: 2 4
4: 3 5
5: 4 6
6: 1 5
```
**Explanation:** Circular graph with 6 users.

---

### Solutions

#### Python
```python
class Node:
    def __init__(self, val=0, neighbors=None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []


class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        # start your solution
        if not node:
            return None
        
        cloned = {}
        
        def dfs(original):
            if original in cloned:
                return cloned[original]
            
            copy = Node(original.val)
            cloned[original] = copy
            
            for neighbor in original.neighbors:
                copy.neighbors.append(dfs(neighbor))
            
            return copy
        
        return dfs(node)
        # end your solution


def main():
    n = int(input())
    
    # Create original nodes
    nodes = [None] + [Node(i) for i in range(1, n + 1)]
    
    # Read adjacency lists
    for i in range(1, n + 1):
        line = input().strip()
        if line:
            neighbors = list(map(int, line.split()))
            for neighbor in neighbors:
                nodes[i].neighbors.append(nodes[neighbor])
    
    sol = Solution()
    if n > 0:
        cloned_start = sol.cloneGraph(nodes[1])
        
        # Collect all cloned nodes using BFS
        from collections import deque
        visited = {}
        queue = deque([cloned_start])
        visited[cloned_start.val] = cloned_start
        
        while queue:
            curr = queue.popleft()
            for neighbor in curr.neighbors:
                if neighbor.val not in visited:
                    visited[neighbor.val] = neighbor
                    queue.append(neighbor)
        
        # Print in order
        for i in range(1, n + 1):
            node = visited[i]
            neighbor_vals = sorted([nb.val for nb in node.neighbors])
            print(f"{node.val}: {' '.join(map(str, neighbor_vals))}" if neighbor_vals else f"{node.val}:")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <queue>
#include <algorithm>
#include <sstream>
using namespace std;

class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() { val = 0; }
    Node(int _val) { val = _val; }
    Node(int _val, vector<Node*> _neighbors) { val = _val; neighbors = _neighbors; }
};

class Solution {
public:
    Node* cloneGraph(Node* node) {
        // start your solution
        if (!node) return nullptr;
        
        unordered_map<Node*, Node*> cloned;
        return dfs(node, cloned);
    }
    
private:
    Node* dfs(Node* original, unordered_map<Node*, Node*>& cloned) {
        if (cloned.find(original) != cloned.end()) {
            return cloned[original];
        }
        
        Node* copy = new Node(original->val);
        cloned[original] = copy;
        
        for (Node* neighbor : original->neighbors) {
            copy->neighbors.push_back(dfs(neighbor, cloned));
        }
        
        return copy;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    cin.ignore();
    
    vector<Node*> nodes(n + 1);
    for (int i = 1; i <= n; i++) {
        nodes[i] = new Node(i);
    }
    
    for (int i = 1; i <= n; i++) {
        string line;
        getline(cin, line);
        if (!line.empty()) {
            stringstream ss(line);
            int neighbor;
            while (ss >> neighbor) {
                nodes[i]->neighbors.push_back(nodes[neighbor]);
            }
        }
    }
    
    Solution sol;
    if (n > 0) {
        Node* clonedStart = sol.cloneGraph(nodes[1]);
        
        unordered_map<int, Node*> visited;
        queue<Node*> q;
        q.push(clonedStart);
        visited[clonedStart->val] = clonedStart;
        
        while (!q.empty()) {
            Node* curr = q.front();
            q.pop();
            for (Node* neighbor : curr->neighbors) {
                if (visited.find(neighbor->val) == visited.end()) {
                    visited[neighbor->val] = neighbor;
                    q.push(neighbor);
                }
            }
        }
        
        for (int i = 1; i <= n; i++) {
            Node* node = visited[i];
            vector<int> neighborVals;
            for (Node* nb : node->neighbors) {
                neighborVals.push_back(nb->val);
            }
            sort(neighborVals.begin(), neighborVals.end());
            
            cout << node->val << ":";
            for (int v : neighborVals) {
                cout << " " << v;
            }
            cout << endl;
        }
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Node {
    public int val;
    public List<Node> neighbors;
    public Node() { val = 0; neighbors = new ArrayList<>(); }
    public Node(int _val) { val = _val; neighbors = new ArrayList<>(); }
}

class Solution {
    public Node cloneGraph(Node node) {
        // start your solution
        if (node == null) return null;
        
        Map<Node, Node> cloned = new HashMap<>();
        return dfs(node, cloned);
    }
    
    private Node dfs(Node original, Map<Node, Node> cloned) {
        if (cloned.containsKey(original)) {
            return cloned.get(original);
        }
        
        Node copy = new Node(original.val);
        cloned.put(original, copy);
        
        for (Node neighbor : original.neighbors) {
            copy.neighbors.add(dfs(neighbor, cloned));
        }
        
        return copy;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        
        Node[] nodes = new Node[n + 1];
        for (int i = 1; i <= n; i++) {
            nodes[i] = new Node(i);
        }
        
        for (int i = 1; i <= n; i++) {
            String line = sc.nextLine().trim();
            if (!line.isEmpty()) {
                String[] parts = line.split(" ");
                for (String part : parts) {
                    int neighbor = Integer.parseInt(part);
                    nodes[i].neighbors.add(nodes[neighbor]);
                }
            }
        }
        
        Solution sol = new Solution();
        if (n > 0) {
            Node clonedStart = sol.cloneGraph(nodes[1]);
            
            Map<Integer, Node> visited = new HashMap<>();
            Queue<Node> queue = new LinkedList<>();
            queue.offer(clonedStart);
            visited.put(clonedStart.val, clonedStart);
            
            while (!queue.isEmpty()) {
                Node curr = queue.poll();
                for (Node neighbor : curr.neighbors) {
                    if (!visited.containsKey(neighbor.val)) {
                        visited.put(neighbor.val, neighbor);
                        queue.offer(neighbor);
                    }
                }
            }
            
            for (int i = 1; i <= n; i++) {
                Node node = visited.get(i);
                List<Integer> neighborVals = new ArrayList<>();
                for (Node nb : node.neighbors) {
                    neighborVals.add(nb.val);
                }
                Collections.sort(neighborVals);
                
                StringBuilder sb = new StringBuilder();
                sb.append(node.val).append(":");
                for (int v : neighborVals) {
                    sb.append(" ").append(v);
                }
                System.out.println(sb.toString());
            }
        }
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Node:
    def __init__(self, val=0, neighbors=None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []


class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    
    nodes = [None] + [Node(i) for i in range(1, n + 1)]
    
    for i in range(1, n + 1):
        line = input().strip()
        if line:
            neighbors = list(map(int, line.split()))
            for neighbor in neighbors:
                nodes[i].neighbors.append(nodes[neighbor])
    
    sol = Solution()
    if n > 0:
        cloned_start = sol.cloneGraph(nodes[1])
        
        from collections import deque
        visited = {}
        queue = deque([cloned_start])
        visited[cloned_start.val] = cloned_start
        
        while queue:
            curr = queue.popleft()
            for neighbor in curr.neighbors:
                if neighbor.val not in visited:
                    visited[neighbor.val] = neighbor
                    queue.append(neighbor)
        
        for i in range(1, n + 1):
            node = visited[i]
            neighbor_vals = sorted([nb.val for nb in node.neighbors])
            print(f"{node.val}: {' '.join(map(str, neighbor_vals))}" if neighbor_vals else f"{node.val}:")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <queue>
#include <algorithm>
#include <sstream>
using namespace std;

class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() { val = 0; }
    Node(int _val) { val = _val; }
    Node(int _val, vector<Node*> _neighbors) { val = _val; neighbors = _neighbors; }
};

class Solution {
public:
    Node* cloneGraph(Node* node) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    cin.ignore();
    
    vector<Node*> nodes(n + 1);
    for (int i = 1; i <= n; i++) {
        nodes[i] = new Node(i);
    }
    
    for (int i = 1; i <= n; i++) {
        string line;
        getline(cin, line);
        if (!line.empty()) {
            stringstream ss(line);
            int neighbor;
            while (ss >> neighbor) {
                nodes[i]->neighbors.push_back(nodes[neighbor]);
            }
        }
    }
    
    Solution sol;
    if (n > 0) {
        Node* clonedStart = sol.cloneGraph(nodes[1]);
        
        unordered_map<int, Node*> visited;
        queue<Node*> q;
        q.push(clonedStart);
        visited[clonedStart->val] = clonedStart;
        
        while (!q.empty()) {
            Node* curr = q.front();
            q.pop();
            for (Node* neighbor : curr->neighbors) {
                if (visited.find(neighbor->val) == visited.end()) {
                    visited[neighbor->val] = neighbor;
                    q.push(neighbor);
                }
            }
        }
        
        for (int i = 1; i <= n; i++) {
            Node* node = visited[i];
            vector<int> neighborVals;
            for (Node* nb : node->neighbors) {
                neighborVals.push_back(nb->val);
            }
            sort(neighborVals.begin(), neighborVals.end());
            
            cout << node->val << ":";
            for (int v : neighborVals) {
                cout << " " << v;
            }
            cout << endl;
        }
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Node {
    public int val;
    public List<Node> neighbors;
    public Node() { val = 0; neighbors = new ArrayList<>(); }
    public Node(int _val) { val = _val; neighbors = new ArrayList<>(); }
}

class Solution {
    public Node cloneGraph(Node node) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        
        Node[] nodes = new Node[n + 1];
        for (int i = 1; i <= n; i++) {
            nodes[i] = new Node(i);
        }
        
        for (int i = 1; i <= n; i++) {
            String line = sc.nextLine().trim();
            if (!line.isEmpty()) {
                String[] parts = line.split(" ");
                for (String part : parts) {
                    int neighbor = Integer.parseInt(part);
                    nodes[i].neighbors.add(nodes[neighbor]);
                }
            }
        }
        
        Solution sol = new Solution();
        if (n > 0) {
            Node clonedStart = sol.cloneGraph(nodes[1]);
            
            Map<Integer, Node> visited = new HashMap<>();
            Queue<Node> queue = new LinkedList<>();
            queue.offer(clonedStart);
            visited.put(clonedStart.val, clonedStart);
            
            while (!queue.isEmpty()) {
                Node curr = queue.poll();
                for (Node neighbor : curr.neighbors) {
                    if (!visited.containsKey(neighbor.val)) {
                        visited.put(neighbor.val, neighbor);
                        queue.offer(neighbor);
                    }
                }
            }
            
            for (int i = 1; i <= n; i++) {
                Node node = visited.get(i);
                List<Integer> neighborVals = new ArrayList<>();
                for (Node nb : node.neighbors) {
                    neighborVals.add(nb.val);
                }
                Collections.sort(neighborVals);
                
                StringBuilder sb = new StringBuilder();
                sb.append(node.val).append(":");
                for (int v : neighborVals) {
                    sb.append(" ").append(v);
                }
                System.out.println(sb.toString());
            }
        }
        
        sc.close();
    }
}
```
