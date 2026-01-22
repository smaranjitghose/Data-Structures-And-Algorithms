# Aadhaar Deactivation System

### Problem Statement

The Unique Identification Authority of India (UIDAI) maintains active Aadhaar numbers in a Binary Search Tree for efficient verification. Each node contains a unique 12-digit Aadhaar number (represented as an integer for simplicity), with smaller numbers in the left subtree and larger numbers in the right subtree.

When a citizen passes away or requests voluntary deactivation, their Aadhaar number must be removed from the active registry while maintaining the BST structure. The deletion must handle three cases: deleting a leaf node, deleting a node with one child, and deleting a node with two children.

Given the root of a BST and a key value to delete, remove the node with the given key from the BST and return the root of the modified tree. If the key doesn't exist, return the tree unchanged.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node
- Third line contains the key value to delete

### Output Format

- Print the level-order traversal of the BST after deletion
- Trim trailing `-1` values
- If tree becomes empty, print `empty`

### Constraints

- `0 <= n <= 10^4`
- `-10^5 <= Node.val <= 10^5`
- All node values are unique
- The tree is a valid BST

### Test Cases

#### Test Case 1
**Input:**
```
7
5 3 6 2 4 -1 7
3
```
**Output:**
```
5 4 6 2 -1 -1 7
```
**Explanation:** Delete node 3. It has two children, so replace with inorder successor (4).

---

#### Test Case 2
**Input:**
```
7
5 3 6 2 4 -1 7
0
```
**Output:**
```
5 3 6 2 4 -1 7
```
**Explanation:** Key 0 doesn't exist, tree remains unchanged.

---

#### Test Case 3
**Input:**
```
1
5
5
```
**Output:**
```
empty
```
**Explanation:** Only node is deleted, tree becomes empty.

---

#### Test Case 4
**Input:**
```
7
5 3 6 2 4 -1 7
7
```
**Output:**
```
5 3 6 2 4
```
**Explanation:** Delete leaf node 7.

---

#### Test Case 5
**Input:**
```
7
5 3 6 2 4 -1 7
6
```
**Output:**
```
5 3 7 2 4
```
**Explanation:** Delete node 6 which has one child (7). Replace 6 with 7.

---

#### Test Case 6
**Input:**
```
7
5 3 6 2 4 -1 7
5
```
**Output:**
```
6 3 7 2 4
```
**Explanation:** Delete root 5. Replace with inorder successor (6).

---

#### Test Case 7
**Input:**
```
5
50 30 70 20 40
30
```
**Output:**
```
50 40 70 20
```
**Explanation:** Delete node 30, replace with its inorder successor 40.

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
    def deleteNode(self, root: TreeNode, key: int) -> TreeNode:
        # start your solution
        if not root:
            return None
        
        if key < root.val:
            root.left = self.deleteNode(root.left, key)
        elif key > root.val:
            root.right = self.deleteNode(root.right, key)
        else:
            if not root.left:
                return root.right
            elif not root.right:
                return root.left
            
            successor = root.right
            while successor.left:
                successor = successor.left
            
            root.val = successor.val
            root.right = self.deleteNode(root.right, successor.val)
        
        return root
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
    if n == 0:
        input()
        key = int(input())
        print("empty")
        return
    
    values = list(map(int, input().split()))
    key = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.deleteNode(root, key)
    
    if not result:
        print("empty")
    else:
        output = tree_to_list(result)
        print(" ".join(map(str, output)))


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
    TreeNode* deleteNode(TreeNode* root, int key) {
        // start your solution
        if (root == nullptr) {
            return nullptr;
        }
        
        if (key < root->val) {
            root->left = deleteNode(root->left, key);
        } else if (key > root->val) {
            root->right = deleteNode(root->right, key);
        } else {
            if (root->left == nullptr) {
                return root->right;
            } else if (root->right == nullptr) {
                return root->left;
            }
            
            TreeNode* successor = root->right;
            while (successor->left != nullptr) {
                successor = successor->left;
            }
            
            root->val = successor->val;
            root->right = deleteNode(root->right, successor->val);
        }
        
        return root;
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
    
    if (n == 0) {
        int key;
        cin >> key;
        cout << "empty" << endl;
        return 0;
    }
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    int key;
    cin >> key;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    TreeNode* result = sol.deleteNode(root, key);
    
    if (result == nullptr) {
        cout << "empty" << endl;
    } else {
        vector<int> output = treeToList(result);
        for (int i = 0; i < output.size(); i++) {
            if (i > 0) cout << " ";
            cout << output[i];
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
    public TreeNode deleteNode(TreeNode root, int key) {
        // start your solution
        if (root == null) {
            return null;
        }
        
        if (key < root.val) {
            root.left = deleteNode(root.left, key);
        } else if (key > root.val) {
            root.right = deleteNode(root.right, key);
        } else {
            if (root.left == null) {
                return root.right;
            } else if (root.right == null) {
                return root.left;
            }
            
            TreeNode successor = root.right;
            while (successor.left != null) {
                successor = successor.left;
            }
            
            root.val = successor.val;
            root.right = deleteNode(root.right, successor.val);
        }
        
        return root;
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
        
        if (n == 0) {
            int key = sc.nextInt();
            System.out.println("empty");
            sc.close();
            return;
        }
        
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        int key = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        TreeNode result = sol.deleteNode(root, key);
        
        if (result == null) {
            System.out.println("empty");
        } else {
            List<Integer> output = treeToList(result);
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < output.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(output.get(i));
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
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def deleteNode(self, root: TreeNode, key: int) -> TreeNode:
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
    if n == 0:
        input()
        key = int(input())
        print("empty")
        return
    
    values = list(map(int, input().split()))
    key = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.deleteNode(root, key)
    
    if not result:
        print("empty")
    else:
        output = tree_to_list(result)
        print(" ".join(map(str, output)))


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
    TreeNode* deleteNode(TreeNode* root, int key) {
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
    
    if (n == 0) {
        int key;
        cin >> key;
        cout << "empty" << endl;
        return 0;
    }
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    int key;
    cin >> key;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    TreeNode* result = sol.deleteNode(root, key);
    
    if (result == nullptr) {
        cout << "empty" << endl;
    } else {
        vector<int> output = treeToList(result);
        for (int i = 0; i < output.size(); i++) {
            if (i > 0) cout << " ";
            cout << output[i];
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
    public TreeNode deleteNode(TreeNode root, int key) {
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
        
        if (n == 0) {
            int key = sc.nextInt();
            System.out.println("empty");
            sc.close();
            return;
        }
        
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        int key = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        TreeNode result = sol.deleteNode(root, key);
        
        if (result == null) {
            System.out.println("empty");
        } else {
            List<Integer> output = treeToList(result);
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < output.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(output.get(i));
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```
