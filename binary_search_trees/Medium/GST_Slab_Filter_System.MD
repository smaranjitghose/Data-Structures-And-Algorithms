# GST Slab Filter System

### Problem Statement

The Goods and Services Tax Network (GSTN) maintains product HSN codes in a Binary Search Tree for efficient tax calculation. Each node contains a unique HSN code number, with smaller codes in the left subtree and larger codes in the right subtree.

For a specialized tax report, the finance ministry needs to extract only the HSN codes that fall within a specific range [low, high]. All codes outside this range should be removed from the tree, while maintaining the BST structure for the remaining nodes.

Given the root of a BST and two boundary values `low` and `high`, trim the tree so that all its elements lie in the range [low, high]. Trimming should maintain the relative structure of the remaining elements (a node's descendant in the original tree should remain its descendant if not removed).

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node
- Third line contains two space-separated integers `low` and `high`

### Output Format

- Print the level-order traversal of the trimmed BST
- Trim trailing `-1` values
- If tree becomes empty, print `empty`

### Constraints

- `1 <= n <= 10^4`
- `0 <= Node.val <= 10^4`
- `0 <= low <= high <= 10^4`

### Test Cases

#### Test Case 1
**Input:**
```
3
1 0 2
1 2
```
**Output:**
```
1 -1 2
```
**Explanation:** Node 0 is less than low (1), so it's removed. Nodes 1 and 2 are within range.

---

#### Test Case 2
**Input:**
```
7
3 0 4 -1 2 -1 -1 1
1 3
```
**Output:**
```
3 2 -1 1
```
**Explanation:** Nodes 0 and 4 are outside [1,3]. Nodes 1, 2, 3 remain.

---

#### Test Case 3
**Input:**
```
1
1
1 1
```
**Output:**
```
1
```
**Explanation:** Single node equals both low and high, so it remains.

---

#### Test Case 4
**Input:**
```
7
5 3 7 2 4 6 8
3 6
```
**Output:**
```
5 3 6 -1 4
```
**Explanation:** Nodes 2, 7, 8 are outside range [3,6].

---

#### Test Case 5
**Input:**
```
5
10 5 15 3 7
5 10
```
**Output:**
```
10 5 -1 -1 7
```
**Explanation:** Nodes 3 and 15 are outside range [5,10].

---

#### Test Case 6
**Input:**
```
3
2 1 3
3 4
```
**Output:**
```
3
```
**Explanation:** Only node 3 is within range [3,4].

---

#### Test Case 7
**Input:**
```
3
2 1 3
5 10
```
**Output:**
```
empty
```
**Explanation:** All nodes are below the range [5,10].

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
    def trimBST(self, root: TreeNode, low: int, high: int) -> TreeNode:
        # start your solution
        if not root:
            return None
        
        if root.val < low:
            return self.trimBST(root.right, low, high)
        
        if root.val > high:
            return self.trimBST(root.left, low, high)
        
        root.left = self.trimBST(root.left, low, high)
        root.right = self.trimBST(root.right, low, high)
        
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
    values = list(map(int, input().split()))
    low, high = map(int, input().split())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.trimBST(root, low, high)
    
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
    TreeNode* trimBST(TreeNode* root, int low, int high) {
        // start your solution
        if (root == nullptr) {
            return nullptr;
        }
        
        if (root->val < low) {
            return trimBST(root->right, low, high);
        }
        
        if (root->val > high) {
            return trimBST(root->left, low, high);
        }
        
        root->left = trimBST(root->left, low, high);
        root->right = trimBST(root->right, low, high);
        
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
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    int low, high;
    cin >> low >> high;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    TreeNode* result = sol.trimBST(root, low, high);
    
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
    public TreeNode trimBST(TreeNode root, int low, int high) {
        // start your solution
        if (root == null) {
            return null;
        }
        
        if (root.val < low) {
            return trimBST(root.right, low, high);
        }
        
        if (root.val > high) {
            return trimBST(root.left, low, high);
        }
        
        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        
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
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        int low = sc.nextInt();
        int high = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        TreeNode result = sol.trimBST(root, low, high);
        
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
    def trimBST(self, root: TreeNode, low: int, high: int) -> TreeNode:
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
    low, high = map(int, input().split())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.trimBST(root, low, high)
    
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
    TreeNode* trimBST(TreeNode* root, int low, int high) {
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
    
    int low, high;
    cin >> low >> high;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    TreeNode* result = sol.trimBST(root, low, high);
    
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
    public TreeNode trimBST(TreeNode root, int low, int high) {
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
        int low = sc.nextInt();
        int high = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        TreeNode result = sol.trimBST(root, low, high);
        
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
