# Indian Railways Zone Hierarchy

### Problem Statement

The Indian Railways network is organized hierarchically as a Binary Search Tree, where each node represents a railway zone or division identified by a unique code number. Smaller codes are in the left subtree and larger codes are in the right subtree. This structure helps in efficient administrative lookups.

Two railway officials from different zones need to coordinate for a joint project. They want to find the lowest level administrative unit (node) that oversees both their zones. In BST terms, this is the Lowest Common Ancestor (LCA) — the deepest node that has both zones in its subtree.

Given the root of the BST representing the railway hierarchy and two zone codes `p` and `q`, find their lowest common ancestor. The LCA is the deepest node that has both p and q as descendants (a node can be a descendant of itself).

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node
- Third line contains two space-separated integers `p` and `q`

### Output Format

- Print the value of the lowest common ancestor node

### Constraints

- `2 <= n <= 10^5`
- `-10^9 <= Node.val <= 10^9`
- All node values are unique
- `p != q`
- `p` and `q` exist in the BST

### Test Cases

#### Test Case 1
**Input:**
```
9
6 2 8 0 4 7 9 -1 -1 3 5
2 8
```
**Output:**
```
6
```
**Explanation:** Nodes 2 and 8 are in different subtrees of root 6. So 6 is their LCA.

---

#### Test Case 2
**Input:**
```
9
6 2 8 0 4 7 9 -1 -1 3 5
2 4
```
**Output:**
```
2
```
**Explanation:** Node 4 is in the subtree of node 2. Since a node can be its own ancestor, LCA is 2.

---

#### Test Case 3
**Input:**
```
2
2 1
2 1
```
**Output:**
```
2
```
**Explanation:** Node 1 is child of node 2. LCA is 2.

---

#### Test Case 4
**Input:**
```
9
6 2 8 0 4 7 9 -1 -1 3 5
3 5
```
**Output:**
```
4
```
**Explanation:** Both 3 and 5 are children of node 4.

---

#### Test Case 5
**Input:**
```
9
6 2 8 0 4 7 9 -1 -1 3 5
0 5
```
**Output:**
```
2
```
**Explanation:** Node 0 is left child of 2, node 5 is in right subtree of 2. LCA is 2.

---

#### Test Case 6
**Input:**
```
9
6 2 8 0 4 7 9 -1 -1 3 5
7 9
```
**Output:**
```
8
```
**Explanation:** Both 7 and 9 are children of node 8.

---

#### Test Case 7
**Input:**
```
9
6 2 8 0 4 7 9 -1 -1 3 5
0 9
```
**Output:**
```
6
```
**Explanation:** Nodes 0 and 9 are on opposite sides of the tree. Root 6 is their LCA.

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
        while root:
            if p.val < root.val and q.val < root.val:
                root = root.left
            elif p.val > root.val and q.val > root.val:
                root = root.right
            else:
                return root
        return None
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
    while root:
        if val == root.val:
            return root
        elif val < root.val:
            root = root.left
        else:
            root = root.right
    return None


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
        while (root) {
            if (p->val < root->val && q->val < root->val) {
                root = root->left;
            } else if (p->val > root->val && q->val > root->val) {
                root = root->right;
            } else {
                return root;
            }
        }
        return nullptr;
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
    while (root) {
        if (val == root->val) return root;
        else if (val < root->val) root = root->left;
        else root = root->right;
    }
    return nullptr;
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
        while (root != null) {
            if (p.val < root.val && q.val < root.val) {
                root = root.left;
            } else if (p.val > root.val && q.val > root.val) {
                root = root.right;
            } else {
                return root;
            }
        }
        return null;
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
        while (root != null) {
            if (val == root.val) return root;
            else if (val < root.val) root = root.left;
            else root = root.right;
        }
        return null;
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
    while root:
        if val == root.val:
            return root
        elif val < root.val:
            root = root.left
        else:
            root = root.right
    return None


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
    while (root) {
        if (val == root->val) return root;
        else if (val < root->val) root = root->left;
        else root = root->right;
    }
    return nullptr;
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
        while (root != null) {
            if (val == root.val) return root;
            else if (val < root.val) root = root.left;
            else root = root.right;
        }
        return null;
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
