# EPFO Account Number Gap Analysis

### Problem Statement

The Employees' Provident Fund Organisation (EPFO) maintains member account numbers in a Binary Search Tree for efficient retrieval. Each node contains a unique Universal Account Number (UAN), with smaller numbers in the left subtree and larger numbers in the right subtree.

For a security audit, the compliance team needs to find the minimum gap between any two consecutive account numbers when all accounts are arranged in sorted order. This helps identify potential numbering anomalies or clustering patterns in account allocation.

Given the root of a BST containing EPFO account numbers, return the minimum absolute difference between the values of any two different nodes in the tree.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node

### Output Format

- A single integer representing the minimum absolute difference between any two nodes

### Constraints

- `2 <= n <= 10^4`
- `0 <= Node.val <= 10^5`
- All node values are unique

### Test Cases

#### Test Case 1
**Input:**
```
3
4 2 6
```
**Output:**
```
2
```
**Explanation:** Inorder traversal gives [2, 4, 6]. Minimum difference is min(4-2, 6-4) = 2.

---

#### Test Case 2
**Input:**
```
5
1 0 48 -1 -1 12 49
```
**Output:**
```
1
```
**Explanation:** Inorder gives [0, 1, 12, 48, 49]. Minimum difference is 49-48 = 1 or 1-0 = 1.

---

#### Test Case 3
**Input:**
```
2
1 -1 2
```
**Output:**
```
1
```
**Explanation:** Only two nodes: 1 and 2. Difference is 1.

---

#### Test Case 4
**Input:**
```
5
10 5 15 3 7
```
**Output:**
```
2
```
**Explanation:** Inorder gives [3, 5, 7, 10, 15]. Minimum difference is 5-3 = 2 or 7-5 = 2.

---

#### Test Case 5
**Input:**
```
7
100 50 150 25 75 125 175
```
**Output:**
```
25
```
**Explanation:** Inorder gives [25, 50, 75, 100, 125, 150, 175]. All consecutive differences are 25.

---

#### Test Case 6
**Input:**
```
4
8 3 10 1
```
**Output:**
```
2
```
**Explanation:** Inorder gives [1, 3, 8, 10]. Minimum is 3-1 = 2 or 10-8 = 2.

---

#### Test Case 7
**Input:**
```
6
4 2 6 1 3 5
```
**Output:**
```
1
```
**Explanation:** Inorder gives [1, 2, 3, 4, 5, 6]. All consecutive differences are 1.

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
    def getMinimumDifference(self, root: TreeNode) -> int:
        # start your solution
        self.prev = None
        self.min_diff = float('inf')
        
        def inorder(node: TreeNode):
            if not node:
                return
            
            inorder(node.left)
            
            if self.prev is not None:
                self.min_diff = min(self.min_diff, node.val - self.prev)
            self.prev = node.val
            
            inorder(node.right)
        
        inorder(root)
        return self.min_diff
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
    print(sol.getMinimumDifference(root))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int prev = -1;
    int minDiff = INT_MAX;
    
    int getMinimumDifference(TreeNode* root) {
        // start your solution
        prev = -1;
        minDiff = INT_MAX;
        inorder(root);
        return minDiff;
    }
    
private:
    void inorder(TreeNode* node) {
        if (node == nullptr) return;
        
        inorder(node->left);
        
        if (prev != -1) {
            minDiff = min(minDiff, node->val - prev);
        }
        prev = node->val;
        
        inorder(node->right);
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
    cout << sol.getMinimumDifference(root) << endl;
    
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
    private Integer prev = null;
    private int minDiff = Integer.MAX_VALUE;
    
    public int getMinimumDifference(TreeNode root) {
        // start your solution
        prev = null;
        minDiff = Integer.MAX_VALUE;
        inorder(root);
        return minDiff;
    }
    
    private void inorder(TreeNode node) {
        if (node == null) return;
        
        inorder(node.left);
        
        if (prev != null) {
            minDiff = Math.min(minDiff, node.val - prev);
        }
        prev = node.val;
        
        inorder(node.right);
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
        System.out.println(sol.getMinimumDifference(root));
        
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
    def getMinimumDifference(self, root: TreeNode) -> int:
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
    print(sol.getMinimumDifference(root))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int getMinimumDifference(TreeNode* root) {
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
    cout << sol.getMinimumDifference(root) << endl;
    
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
    public int getMinimumDifference(TreeNode root) {
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
        System.out.println(sol.getMinimumDifference(root));
        
        sc.close();
    }
}
```
