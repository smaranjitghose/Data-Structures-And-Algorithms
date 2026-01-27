# Joint Family Reunion at Ancestral Home

### Problem Statement

The Sharma family from Varanasi is organizing a grand reunion at their ancestral home. The family tree is represented as a binary tree where each node contains a unique family member ID. Two cousins, who live in different cities, want to meet at the home of their nearest common ancestor to minimize travel for both.

The lowest common ancestor (LCA) of two family members `p` and `q` is defined as the closest ancestor node that has both `p` and `q` as descendants (where we allow a node to be a descendant of itself). In other words, it's the first person in the family tree from whom both cousins are descended.

Given the root of a binary tree representing the family structure and two family member nodes `p` and `q`, find and return their lowest common ancestor.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the tree, where `-1` denotes a null node
- Third line contains two space-separated integers `p` and `q` representing the values of the two nodes

### Output Format

- Print the value of the lowest common ancestor node

### Constraints

- `2 <= n <= 10^5`
- `-10^9 <= Node.val <= 10^9`
- All node values are unique
- `p != q`
- `p` and `q` will exist in the tree

### Test Cases

#### Test Case 1
**Input:**
```
7
3 5 1 6 2 0 8
5 1
```
**Output:**
```
3
```
**Explanation:** The LCA of nodes 5 and 1 is the root node 3, as both are in different subtrees.

---

#### Test Case 2
**Input:**
```
7
3 5 1 6 2 0 8
5 4
```
**Output:**
```
5
```
**Explanation:** Node 4 is in the subtree of node 5. Since a node can be ancestor of itself, LCA of 5 and 4 is 5.

---

#### Test Case 3
**Input:**
```
2
1 2
1 2
```
**Output:**
```
1
```
**Explanation:** With only root and one child, the root is the LCA.

---

#### Test Case 4
**Input:**
```
7
3 5 1 6 2 0 8
6 2
```
**Output:**
```
5
```
**Explanation:** Both 6 and 2 are children of 5, so 5 is their LCA.

---

#### Test Case 5
**Input:**
```
7
3 5 1 6 2 0 8
0 8
```
**Output:**
```
1
```
**Explanation:** Nodes 0 and 8 are both children of node 1, so 1 is their LCA.

---

#### Test Case 6
**Input:**
```
7
3 5 1 6 2 0 8
6 8
```
**Output:**
```
3
```
**Explanation:** Node 6 is in left subtree (under 5), node 8 is in right subtree (under 1). Their LCA is root 3.

---

#### Test Case 7
**Input:**
```
5
1 2 3 4 5
4 5
```
**Output:**
```
2
```
**Explanation:** Nodes 4 and 5 are both children of node 2, so 2 is their LCA.

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
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        # start your solution
        if root is None or root == p or root == q:
            return root
        
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        
        if left and right:
            return root
        
        return left if left else right
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


def find_node(root: TreeNode, val: int) -> TreeNode:
    if root is None:
        return None
    if root.val == val:
        return root
    
    left = find_node(root.left, val)
    if left:
        return left
    return find_node(root.right, val)


def main():
    n = int(input())
    values = list(map(int, input().split()))
    p_val, q_val = map(int, input().split())
    
    root = build_tree(values)
    p = find_node(root, p_val)
    q = find_node(root, q_val)
    
    sol = Solution()
    lca = sol.lowestCommonAncestor(root, p, q)
    print(lca.val)


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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // start your solution
        if (root == nullptr || root == p || root == q) {
            return root;
        }
        
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        
        if (left && right) {
            return root;
        }
        
        return left ? left : right;
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

TreeNode* findNode(TreeNode* root, int val) {
    if (root == nullptr) return nullptr;
    if (root->val == val) return root;
    
    TreeNode* left = findNode(root->left, val);
    if (left) return left;
    return findNode(root->right, val);
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
    
    int pVal, qVal;
    cin >> pVal >> qVal;
    
    TreeNode* root = buildTree(values);
    TreeNode* p = findNode(root, pVal);
    TreeNode* q = findNode(root, qVal);
    
    Solution sol;
    TreeNode* lca = sol.lowestCommonAncestor(root, p, q);
    cout << lca->val << endl;
    
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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // start your solution
        if (root == null || root == p || root == q) {
            return root;
        }
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        if (left != null && right != null) {
            return root;
        }
        
        return left != null ? left : right;
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
    
    public static TreeNode findNode(TreeNode root, int val) {
        if (root == null) return null;
        if (root.val == val) return root;
        
        TreeNode left = findNode(root.left, val);
        if (left != null) return left;
        return findNode(root.right, val);
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        
        int pVal = sc.nextInt();
        int qVal = sc.nextInt();
        
        TreeNode root = buildTree(values);
        TreeNode p = findNode(root, pVal);
        TreeNode q = findNode(root, qVal);
        
        Solution sol = new Solution();
        TreeNode lca = sol.lowestCommonAncestor(root, p, q);
        System.out.println(lca.val);
        
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
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
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


def find_node(root: TreeNode, val: int) -> TreeNode:
    if root is None:
        return None
    if root.val == val:
        return root
    
    left = find_node(root.left, val)
    if left:
        return left
    return find_node(root.right, val)


def main():
    n = int(input())
    values = list(map(int, input().split()))
    p_val, q_val = map(int, input().split())
    
    root = build_tree(values)
    p = find_node(root, p_val)
    q = find_node(root, q_val)
    
    sol = Solution()
    lca = sol.lowestCommonAncestor(root, p, q)
    print(lca.val)


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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
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

TreeNode* findNode(TreeNode* root, int val) {
    if (root == nullptr) return nullptr;
    if (root->val == val) return root;
    
    TreeNode* left = findNode(root->left, val);
    if (left) return left;
    return findNode(root->right, val);
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
    
    int pVal, qVal;
    cin >> pVal >> qVal;
    
    TreeNode* root = buildTree(values);
    TreeNode* p = findNode(root, pVal);
    TreeNode* q = findNode(root, qVal);
    
    Solution sol;
    TreeNode* lca = sol.lowestCommonAncestor(root, p, q);
    cout << lca->val << endl;
    
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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
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
    
    public static TreeNode findNode(TreeNode root, int val) {
        if (root == null) return null;
        if (root.val == val) return root;
        
        TreeNode left = findNode(root.left, val);
        if (left != null) return left;
        return findNode(root.right, val);
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        
        int pVal = sc.nextInt();
        int qVal = sc.nextInt();
        
        TreeNode root = buildTree(values);
        TreeNode p = findNode(root, pVal);
        TreeNode q = findNode(root, qVal);
        
        Solution sol = new Solution();
        TreeNode lca = sol.lowestCommonAncestor(root, p, q);
        System.out.println(lca.val);
        
        sc.close();
    }
}
```