# Metro Network Longest Route

### Problem Statement

The Delhi Metro Rail Corporation (DMRC) is analyzing its network topology for a new connectivity report. The metro network can be represented as a binary tree where each node is a station, and edges represent direct connections between stations. The planning team wants to find the longest possible route a passenger could take without visiting any station twice.

The diameter of the metro network is defined as the length of the longest path between any two stations. This path may or may not pass through the central hub (root). The length of a path is measured by the number of edges (connections) between stations.

Given the root of a binary tree representing the metro network, return the length of the diameter of the tree.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the tree, where `-1` denotes a null node

### Output Format

- A single integer representing the diameter (longest path length) of the binary tree

### Constraints

- `1 <= n <= 10^4`
- `-100 <= Node.val <= 100`

### Test Cases

#### Test Case 1
**Input:**
```
5
1 2 3 4 5
```
**Output:**
```
3
```
**Explanation:** The longest path is 4 → 2 → 1 → 3 or 5 → 2 → 1 → 3, both having 3 edges.

---

#### Test Case 2
**Input:**
```
2
1 2
```
**Output:**
```
1
```
**Explanation:** Only one edge exists between nodes 1 and 2.

---

#### Test Case 3
**Input:**
```
1
1
```
**Output:**
```
0
```
**Explanation:** Single node has no edges, so diameter is 0.

---

#### Test Case 4
**Input:**
```
7
1 2 3 4 5 -1 -1
```
**Output:**
```
3
```
**Explanation:** Longest path is 4 → 2 → 1 → 3 or 5 → 2 → 1 → 3 with 3 edges.

---

#### Test Case 5
**Input:**
```
9
1 2 3 4 5 6 7 8 -1
```
**Output:**
```
5
```
**Explanation:** Longest path is 8 → 4 → 2 → 1 → 3 → 6 or 8 → 4 → 2 → 1 → 3 → 7 with 5 edges.

---

#### Test Case 6
**Input:**
```
5
1 2 -1 3 -1 4 -1
```
**Output:**
```
3
```
**Explanation:** Left-skewed tree: 4 → 3 → 2 → 1 has 3 edges.

---

#### Test Case 7
**Input:**
```
15
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
```
**Output:**
```
6
```
**Explanation:** Complete binary tree of 4 levels. Longest path goes from a leaf on one side through root to a leaf on the other side.

---

### Solutions

#### Python
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        # start your solution
        self.diameter = 0
        
        def height(node: TreeNode) -> int:
            if not node:
                return 0
            
            left_height = height(node.left)
            right_height = height(node.right)
            
            self.diameter = max(self.diameter, left_height + right_height)
            
            return 1 + max(left_height, right_height)
        
        height(root)
        return self.diameter
        # end your solution


def build_tree(values: list) -> TreeNode:
    if not values or values[0] == -1:
        return None
    
    root = TreeNode(values[0])
    queue = [root]
    i = 1
    
    while queue and i < len(values):
        node = queue.pop(0)
        
        if i < len(values) and values[i] != -1:
            node.left = TreeNode(values[i])
            queue.append(node.left)
        i += 1
        
        if i < len(values) and values[i] != -1:
            node.right = TreeNode(values[i])
            queue.append(node.right)
        i += 1
    
    return root


def main():
    n = int(input())
    values = list(map(int, input().split()))
    root = build_tree(values)
    
    sol = Solution()
    print(sol.diameterOfBinaryTree(root))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int diameter;
    
    int diameterOfBinaryTree(TreeNode* root) {
        // start your solution
        diameter = 0;
        height(root);
        return diameter;
    }
    
private:
    int height(TreeNode* node) {
        if (node == nullptr) {
            return 0;
        }
        
        int leftHeight = height(node->left);
        int rightHeight = height(node->right);
        
        diameter = max(diameter, leftHeight + rightHeight);
        
        return 1 + max(leftHeight, rightHeight);
        // end your solution
    }
};

TreeNode* buildTree(vector<int>& values) {
    if (values.empty() || values[0] == -1) {
        return nullptr;
    }
    
    TreeNode* root = new TreeNode(values[0]);
    queue<TreeNode*> q;
    q.push(root);
    int i = 1;
    
    while (!q.empty() && i < values.size()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (i < values.size() && values[i] != -1) {
            node->left = new TreeNode(values[i]);
            q.push(node->left);
        }
        i++;
        
        if (i < values.size() && values[i] != -1) {
            node->right = new TreeNode(values[i]);
            q.push(node->right);
        }
        i++;
    }
    
    return root;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    cout << sol.diameterOfBinaryTree(root) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    private int diameter;
    
    public int diameterOfBinaryTree(TreeNode root) {
        // start your solution
        diameter = 0;
        height(root);
        return diameter;
    }
    
    private int height(TreeNode node) {
        if (node == null) {
            return 0;
        }
        
        int leftHeight = height(node.left);
        int rightHeight = height(node.right);
        
        diameter = Math.max(diameter, leftHeight + rightHeight);
        
        return 1 + Math.max(leftHeight, rightHeight);
        // end your solution
    }
}

public class Main {
    public static TreeNode buildTree(int[] values) {
        if (values.length == 0 || values[0] == -1) {
            return null;
        }
        
        TreeNode root = new TreeNode(values[0]);
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int i = 1;
        
        while (!queue.isEmpty() && i < values.length) {
            TreeNode node = queue.poll();
            
            if (i < values.length && values[i] != -1) {
                node.left = new TreeNode(values[i]);
                queue.offer(node.left);
            }
            i++;
            
            if (i < values.length && values[i] != -1) {
                node.right = new TreeNode(values[i]);
                queue.offer(node.right);
            }
            i++;
        }
        
        return root;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        System.out.println(sol.diameterOfBinaryTree(root));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        # start your solution
        
        
        
        # end your solution


def build_tree(values: list) -> TreeNode:
    if not values or values[0] == -1:
        return None
    
    root = TreeNode(values[0])
    queue = [root]
    i = 1
    
    while queue and i < len(values):
        node = queue.pop(0)
        
        if i < len(values) and values[i] != -1:
            node.left = TreeNode(values[i])
            queue.append(node.left)
        i += 1
        
        if i < len(values) and values[i] != -1:
            node.right = TreeNode(values[i])
            queue.append(node.right)
        i += 1
    
    return root


def main():
    n = int(input())
    values = list(map(int, input().split()))
    root = build_tree(values)
    
    sol = Solution()
    print(sol.diameterOfBinaryTree(root))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int diameterOfBinaryTree(TreeNode* root) {
        // start your solution
        
        
        
        // end your solution
    }
};

TreeNode* buildTree(vector<int>& values) {
    if (values.empty() || values[0] == -1) {
        return nullptr;
    }
    
    TreeNode* root = new TreeNode(values[0]);
    queue<TreeNode*> q;
    q.push(root);
    int i = 1;
    
    while (!q.empty() && i < values.size()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (i < values.size() && values[i] != -1) {
            node->left = new TreeNode(values[i]);
            q.push(node->left);
        }
        i++;
        
        if (i < values.size() && values[i] != -1) {
            node->right = new TreeNode(values[i]);
            q.push(node->right);
        }
        i++;
    }
    
    return root;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    cout << sol.diameterOfBinaryTree(root) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int val) { this.val = val; }
}

class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static TreeNode buildTree(int[] values) {
        if (values.length == 0 || values[0] == -1) {
            return null;
        }
        
        TreeNode root = new TreeNode(values[0]);
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int i = 1;
        
        while (!queue.isEmpty() && i < values.length) {
            TreeNode node = queue.poll();
            
            if (i < values.length && values[i] != -1) {
                node.left = new TreeNode(values[i]);
                queue.offer(node.left);
            }
            i++;
            
            if (i < values.length && values[i] != -1) {
                node.right = new TreeNode(values[i]);
                queue.offer(node.right);
            }
            i++;
        }
        
        return root;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        System.out.println(sol.diameterOfBinaryTree(root));
        
        sc.close();
    }
}
```