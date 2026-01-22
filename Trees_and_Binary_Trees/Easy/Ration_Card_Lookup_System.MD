# Ration Card Lookup System

### Problem Statement

The Public Distribution System (PDS) in Kerala maintains a digital registry of ration card holders organized as a Binary Search Tree. Each node contains a unique ration card number, with smaller numbers in the left subtree and larger numbers in the right subtree. This organization allows for efficient lookup of card holder records.

A Taluk Supply Officer needs to search for a specific ration card number in the system. If found, the system should return the subtree rooted at that node (representing the card holder and all dependent records). If the card number doesn't exist, the system should indicate that no record was found.

Given the root of the BST representing the ration card registry and a target card number `val`, find the node with that value and return the subtree rooted at that node. If the card number does not exist, return null.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node
- Third line contains the target value `val` to search for

### Output Format

- Print the level-order traversal of the subtree rooted at the found node
- If the node is not found, print `null`
- Trim trailing `-1` values from output

### Constraints

- `1 <= n <= 5000`
- `1 <= Node.val <= 10^7`
- `1 <= val <= 10^7`
- All node values are unique
- The tree is a valid Binary Search Tree

### Test Cases

#### Test Case 1
**Input:**
```
7
4 2 7 1 3 -1 -1
2
```
**Output:**
```
2 1 3
```
**Explanation:** Found node with value 2. Its subtree contains nodes 2, 1, and 3.

---

#### Test Case 2
**Input:**
```
7
4 2 7 1 3 -1 -1
5
```
**Output:**
```
null
```
**Explanation:** Value 5 does not exist in the BST.

---

#### Test Case 3
**Input:**
```
1
1
1
```
**Output:**
```
1
```
**Explanation:** Single node tree, searching for root value returns the root.

---

#### Test Case 4
**Input:**
```
7
4 2 7 1 3 -1 -1
4
```
**Output:**
```
4 2 7 1 3
```
**Explanation:** Searching for root returns the entire tree.

---

#### Test Case 5
**Input:**
```
7
4 2 7 1 3 -1 -1
1
```
**Output:**
```
1
```
**Explanation:** Found leaf node with value 1. Subtree contains only that node.

---

#### Test Case 6
**Input:**
```
7
4 2 7 1 3 -1 -1
7
```
**Output:**
```
7
```
**Explanation:** Found node 7 which has no children.

---

#### Test Case 7
**Input:**
```
15
8 4 12 2 6 10 14 1 3 5 7 9 11 13 15
6
```
**Output:**
```
6 5 7
```
**Explanation:** Found node 6 in a larger BST. Its subtree has children 5 and 7.

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
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        # start your solution
        if not root or root.val == val:
            return root
        
        if val < root.val:
            return self.searchBST(root.left, val)
        else:
            return self.searchBST(root.right, val)
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


def tree_to_list(root: TreeNode) -> list:
    if not root:
        return []
    
    result = []
    queue = [root]
    
    while queue:
        node = queue.pop(0)
        if node:
            result.append(node.val)
            queue.append(node.left)
            queue.append(node.right)
        else:
            result.append(-1)
    
    while result and result[-1] == -1:
        result.pop()
    
    return result


def main():
    n = int(input())
    values = list(map(int, input().split()))
    val = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.searchBST(root, val)
    
    if result:
        output = tree_to_list(result)
        print(" ".join(map(str, output)))
    else:
        print("null")


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
    TreeNode* searchBST(TreeNode* root, int val) {
        // start your solution
        if (root == nullptr || root->val == val) {
            return root;
        }
        
        if (val < root->val) {
            return searchBST(root->left, val);
        } else {
            return searchBST(root->right, val);
        }
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

vector<int> treeToList(TreeNode* root) {
    vector<int> result;
    if (root == nullptr) {
        return result;
    }
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (node) {
            result.push_back(node->val);
            q.push(node->left);
            q.push(node->right);
        } else {
            result.push_back(-1);
        }
    }
    
    while (!result.empty() && result.back() == -1) {
        result.pop_back();
    }
    
    return result;
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
    
    int val;
    cin >> val;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    TreeNode* result = sol.searchBST(root, val);
    
    if (result) {
        vector<int> output = treeToList(result);
        for (int i = 0; i < output.size(); i++) {
            if (i > 0) cout << " ";
            cout << output[i];
        }
        cout << endl;
    } else {
        cout << "null" << endl;
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
    public TreeNode searchBST(TreeNode root, int val) {
        // start your solution
        if (root == null || root.val == val) {
            return root;
        }
        
        if (val < root.val) {
            return searchBST(root.left, val);
        } else {
            return searchBST(root.right, val);
        }
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
    
    public static List<Integer> treeToList(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            
            if (node != null) {
                result.add(node.val);
                queue.offer(node.left);
                queue.offer(node.right);
            } else {
                result.add(-1);
            }
        }
        
        while (!result.isEmpty() && result.get(result.size() - 1) == -1) {
            result.remove(result.size() - 1);
        }
        
        return result;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        int val = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        TreeNode result = sol.searchBST(root, val);
        
        if (result != null) {
            List<Integer> output = treeToList(result);
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < output.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(output.get(i));
            }
            System.out.println(sb.toString());
        } else {
            System.out.println("null");
        }
        
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
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
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


def tree_to_list(root: TreeNode) -> list:
    if not root:
        return []
    
    result = []
    queue = [root]
    
    while queue:
        node = queue.pop(0)
        if node:
            result.append(node.val)
            queue.append(node.left)
            queue.append(node.right)
        else:
            result.append(-1)
    
    while result and result[-1] == -1:
        result.pop()
    
    return result


def main():
    n = int(input())
    values = list(map(int, input().split()))
    val = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.searchBST(root, val)
    
    if result:
        output = tree_to_list(result)
        print(" ".join(map(str, output)))
    else:
        print("null")


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
    TreeNode* searchBST(TreeNode* root, int val) {
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

vector<int> treeToList(TreeNode* root) {
    vector<int> result;
    if (root == nullptr) {
        return result;
    }
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (node) {
            result.push_back(node->val);
            q.push(node->left);
            q.push(node->right);
        } else {
            result.push_back(-1);
        }
    }
    
    while (!result.empty() && result.back() == -1) {
        result.pop_back();
    }
    
    return result;
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
    
    int val;
    cin >> val;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    TreeNode* result = sol.searchBST(root, val);
    
    if (result) {
        vector<int> output = treeToList(result);
        for (int i = 0; i < output.size(); i++) {
            if (i > 0) cout << " ";
            cout << output[i];
        }
        cout << endl;
    } else {
        cout << "null" << endl;
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
    public TreeNode searchBST(TreeNode root, int val) {
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
    
    public static List<Integer> treeToList(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            
            if (node != null) {
                result.add(node.val);
                queue.offer(node.left);
                queue.offer(node.right);
            } else {
                result.add(-1);
            }
        }
        
        while (!result.isEmpty() && result.get(result.size() - 1) == -1) {
            result.remove(result.size() - 1);
        }
        
        return result;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        int val = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        TreeNode result = sol.searchBST(root, val);
        
        if (result != null) {
            List<Integer> output = treeToList(result);
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < output.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(output.get(i));
            }
            System.out.println(sb.toString());
        } else {
            System.out.println("null");
        }
        
        sc.close();
    }
}
```
