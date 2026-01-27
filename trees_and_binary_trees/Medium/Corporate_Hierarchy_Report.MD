# Corporate Hierarchy Report at TCS

### Problem Statement

Tata Consultancy Services (TCS) maintains its organizational structure as a binary tree where each node represents an employee with their employee ID. The HR department needs to generate a level-wise report of all employees for the annual review process. Each level in the hierarchy should be reported separately, starting from the CEO at the top.

The level order traversal visits all nodes at depth 0 (root), then all nodes at depth 1, then all nodes at depth 2, and so on. Within each level, nodes are visited from left to right.

Given the root of a binary tree representing the corporate hierarchy, return the level order traversal of its nodes' values as a list of lists, where each inner list contains all employee IDs at that level.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the tree, where `-1` denotes a null node

### Output Format

- Print each level on a separate line
- Each line contains space-separated values of nodes at that level
- If the tree is empty, print nothing

### Constraints

- `0 <= n <= 2000`
- `-1000 <= Node.val <= 1000`

### Test Cases

#### Test Case 1
**Input:**
```
7
3 9 20 -1 -1 15 7
```
**Output:**
```
3
9 20
15 7
```
**Explanation:** Level 0 has node 3, level 1 has nodes 9 and 20, level 2 has nodes 15 and 7.

---

#### Test Case 2
**Input:**
```
1
1
```
**Output:**
```
1
```
**Explanation:** Single node tree has only one level.

---

#### Test Case 3
**Input:**
```
0

```
**Output:**
```

```
**Explanation:** Empty tree produces no output.

---

#### Test Case 4
**Input:**
```
5
1 2 3 4 5
```
**Output:**
```
1
2 3
4 5
```
**Explanation:** Complete binary tree with 3 levels.

---

#### Test Case 5
**Input:**
```
4
1 2 -1 3
```
**Output:**
```
1
2
3
```
**Explanation:** Left-skewed tree with nodes going down the left side, then left again.

---

#### Test Case 6
**Input:**
```
15
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
```
**Output:**
```
1
2 3
4 5 6 7
8 9 10 11 12 13 14 15
```
**Explanation:** Complete binary tree with 4 levels, each level has 2^level nodes.

---

#### Test Case 7
**Input:**
```
6
1 2 3 -1 4 -1 5
```
**Output:**
```
1
2 3
4 5
```
**Explanation:** Sparse tree where some nodes have only one child.

---

### Solutions

#### Python
```python
from collections import deque


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def levelOrder(self, root: TreeNode) -> list[list[int]]:
        # start your solution
        if not root:
            return []
        
        result = []
        queue = deque([root])
        
        while queue:
            level_size = len(queue)
            current_level = []
            
            for _ in range(level_size):
                node = queue.popleft()
                current_level.append(node.val)
                
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            
            result.append(current_level)
        
        return result
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
    if n == 0:
        return
    
    values = list(map(int, input().split()))
    root = build_tree(values)
    
    sol = Solution()
    result = sol.levelOrder(root)
    
    for level in result:
        print(" ".join(map(str, level)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        // start your solution
        vector<vector<int>> result;
        if (root == nullptr) {
            return result;
        }
        
        queue<TreeNode*> q;
        q.push(root);
        
        while (!q.empty()) {
            int levelSize = q.size();
            vector<int> currentLevel;
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode* node = q.front();
                q.pop();
                currentLevel.push_back(node->val);
                
                if (node->left) {
                    q.push(node->left);
                }
                if (node->right) {
                    q.push(node->right);
                }
            }
            
            result.push_back(currentLevel);
        }
        
        return result;
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
    
    if (n == 0) {
        return 0;
    }
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    vector<vector<int>> result = sol.levelOrder(root);
    
    for (const auto& level : result) {
        for (int i = 0; i < level.size(); i++) {
            if (i > 0) cout << " ";
            cout << level[i];
        }
        cout << endl;
    }
    
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        // start your solution
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            List<Integer> currentLevel = new ArrayList<>();
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                currentLevel.add(node.val);
                
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            
            result.add(currentLevel);
        }
        
        return result;
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
        
        if (n == 0) {
            sc.close();
            return;
        }
        
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        List<List<Integer>> result = sol.levelOrder(root);
        
        for (List<Integer> level : result) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < level.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(level.get(i));
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


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def levelOrder(self, root: TreeNode) -> list[list[int]]:
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
    if n == 0:
        return
    
    values = list(map(int, input().split()))
    root = build_tree(values)
    
    sol = Solution()
    result = sol.levelOrder(root)
    
    for level in result:
        print(" ".join(map(str, level)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
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
    
    if (n == 0) {
        return 0;
    }
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    vector<vector<int>> result = sol.levelOrder(root);
    
    for (const auto& level : result) {
        for (int i = 0; i < level.size(); i++) {
            if (i > 0) cout << " ";
            cout << level[i];
        }
        cout << endl;
    }
    
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
    public List<List<Integer>> levelOrder(TreeNode root) {
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
        
        if (n == 0) {
            sc.close();
            return;
        }
        
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        List<List<Integer>> result = sol.levelOrder(root);
        
        for (List<Integer> level : result) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < level.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(level.get(i));
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```