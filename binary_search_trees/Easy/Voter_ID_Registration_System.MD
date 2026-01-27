# Voter ID Registration System

### Problem Statement

The Election Commission of India maintains a digital voter registry for a constituency in Gujarat, organized as a Binary Search Tree. Each node contains a unique voter ID number, with smaller IDs in the left subtree and larger IDs in the right subtree. This structure allows efficient lookup during elections.

When a new citizen becomes eligible to vote, their voter ID must be added to the registry. The new ID should be inserted at the appropriate position to maintain the BST property. Since all voter IDs are unique, there's guaranteed to be a valid position for any new ID.

Given the root of the BST representing the voter registry and a new voter ID `val` to insert, add the new node to the tree and return the root of the modified BST. The insertion should maintain the BST property.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node
- Third line contains the value `val` to insert

### Output Format

- Print the level-order traversal of the BST after insertion
- Trim trailing `-1` values from output

### Constraints

- `0 <= n <= 10^4`
- `-10^8 <= Node.val <= 10^8`
- All values in the tree are unique
- `-10^8 <= val <= 10^8`
- `val` does not exist in the original BST

### Test Cases

#### Test Case 1
**Input:**
```
5
4 2 7 1 3
5
```
**Output:**
```
4 2 7 1 3 5
```
**Explanation:** Value 5 is inserted as the left child of node 7 (since 5 < 7 and 5 > 4).

---

#### Test Case 2
**Input:**
```
5
40 20 60 10 30
25
```
**Output:**
```
40 20 60 10 30 -1 -1 -1 -1 25
```
**Explanation:** Value 25 is inserted as the left child of node 30.

---

#### Test Case 3
**Input:**
```
0

5
```
**Output:**
```
5
```
**Explanation:** Empty tree, inserted value becomes the root.

---

#### Test Case 4
**Input:**
```
1
10
5
```
**Output:**
```
10 5
```
**Explanation:** Value 5 is less than 10, so it becomes the left child.

---

#### Test Case 5
**Input:**
```
1
10
15
```
**Output:**
```
10 -1 15
```
**Explanation:** Value 15 is greater than 10, so it becomes the right child.

---

#### Test Case 6
**Input:**
```
7
50 30 70 20 40 60 80
25
```
**Output:**
```
50 30 70 20 40 60 80 -1 25
```
**Explanation:** Value 25 goes right of 20 in the left subtree.

---

#### Test Case 7
**Input:**
```
7
50 30 70 20 40 60 80
75
```
**Output:**
```
50 30 70 20 40 60 80 -1 -1 -1 -1 -1 -1 75
```
**Explanation:** Value 75 is inserted as left child of 80.

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
    def insertIntoBST(self, root: TreeNode, val: int) -> TreeNode:
        # start your solution
        if not root:
            return TreeNode(val)
        
        if val < root.val:
            root.left = self.insertIntoBST(root.left, val)
        else:
            root.right = self.insertIntoBST(root.right, val)
        
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
        input()  # consume empty line
        val = int(input())
        print(val)
        return
    
    values = list(map(int, input().split()))
    val = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.insertIntoBST(root, val)
    
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
#include <string>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        // start your solution
        if (root == nullptr) {
            return new TreeNode(val);
        }
        
        if (val < root->val) {
            root->left = insertIntoBST(root->left, val);
        } else {
            root->right = insertIntoBST(root->right, val);
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
        int val;
        cin >> val;
        cout << val << endl;
        return 0;
    }
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    int val;
    cin >> val;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    TreeNode* result = sol.insertIntoBST(root, val);
    
    vector<int> output = treeToList(result);
    for (int i = 0; i < output.size(); i++) {
        if (i > 0) cout << " ";
        cout << output[i];
    }
    cout << endl;
    
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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        // start your solution
        if (root == null) {
            return new TreeNode(val);
        }
        
        if (val < root.val) {
            root.left = insertIntoBST(root.left, val);
        } else {
            root.right = insertIntoBST(root.right, val);
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
            int val = sc.nextInt();
            System.out.println(val);
            sc.close();
            return;
        }
        
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        int val = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        TreeNode result = sol.insertIntoBST(root, val);
        
        List<Integer> output = treeToList(result);
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < output.size(); i++) {
            if (i > 0) sb.append(" ");
            sb.append(output.get(i));
        }
        System.out.println(sb.toString());
        
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
    def insertIntoBST(self, root: TreeNode, val: int) -> TreeNode:
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
        input()  # consume empty line
        val = int(input())
        print(val)
        return
    
    values = list(map(int, input().split()))
    val = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.insertIntoBST(root, val)
    
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
#include <string>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
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
        int val;
        cin >> val;
        cout << val << endl;
        return 0;
    }
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    int val;
    cin >> val;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    TreeNode* result = sol.insertIntoBST(root, val);
    
    vector<int> output = treeToList(result);
    for (int i = 0; i < output.size(); i++) {
        if (i > 0) cout << " ";
        cout << output[i];
    }
    cout << endl;
    
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
    public TreeNode insertIntoBST(TreeNode root, int val) {
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
            int val = sc.nextInt();
            System.out.println(val);
            sc.close();
            return;
        }
        
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        int val = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        TreeNode result = sol.insertIntoBST(root, val);
        
        List<Integer> output = treeToList(result);
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < output.size(); i++) {
            if (i > 0) sb.append(" ");
            sb.append(output.get(i));
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```
