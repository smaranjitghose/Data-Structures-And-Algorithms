# Reconstructing ISRO Satellite Network

### Problem Statement

The Indian Space Research Organisation (ISRO) maintains a satellite communication network structured as a binary tree. Due to a system malfunction, the original tree structure was lost, but engineers managed to recover two traversal logs from backup systems: the preorder traversal log (recording satellites as they were activated from root) and the inorder traversal log (recording satellites in a left-root-right pattern).

Your task is to help ISRO engineers reconstruct the original satellite network tree from these two traversal sequences. Each satellite has a unique identifier, and no two satellites share the same ID.

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal and `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

### Input Format

- First line contains the number of nodes `n`
- Second line contains `n` space-separated integers representing the preorder traversal
- Third line contains `n` space-separated integers representing the inorder traversal

### Output Format

- Print the level-order traversal of the constructed tree as space-separated values
- Use `-1` for null nodes only when needed to show structure
- Trim trailing `-1` values

### Constraints

- `1 <= n <= 3000`
- `-3000 <= preorder[i], inorder[i] <= 3000`
- `preorder` and `inorder` consist of unique values
- Each value of `inorder` also appears in `preorder`
- `preorder` is guaranteed to be the preorder traversal of the tree
- `inorder` is guaranteed to be the inorder traversal of the tree

### Test Cases

#### Test Case 1
**Input:**
```
5
3 9 20 15 7
9 3 15 20 7
```
**Output:**
```
3 9 20 -1 -1 15 7
```
**Explanation:** Preorder [3,9,20,15,7] with root 3. Inorder [9,3,15,20,7] shows 9 is left of 3, and [15,20,7] is right subtree.

---

#### Test Case 2
**Input:**
```
1
-1
-1
```
**Output:**
```
-1
```
**Explanation:** Single node with value -1.

---

#### Test Case 3
**Input:**
```
3
1 2 3
2 1 3
```
**Output:**
```
1 2 3
```
**Explanation:** Root is 1, left child is 2, right child is 3.

---

#### Test Case 4
**Input:**
```
5
1 2 4 5 3
4 2 5 1 3
```
**Output:**
```
1 2 3 4 5
```
**Explanation:** Root 1, left subtree has root 2 with children 4 and 5, right child is 3.

---

#### Test Case 5
**Input:**
```
4
1 2 3 4
4 3 2 1
```
**Output:**
```
1 2 -1 3 -1 4
```
**Explanation:** Right-skewed tree going left at each level: 1 → 2 → 3 → 4.

---

#### Test Case 6
**Input:**
```
4
1 2 3 4
1 2 3 4
```
**Output:**
```
1 -1 2 -1 3 -1 4
```
**Explanation:** Left-skewed tree: 1 → 2 → 3 → 4 all going right.

---

#### Test Case 7
**Input:**
```
7
1 2 4 5 3 6 7
4 2 5 1 6 3 7
```
**Output:**
```
1 2 3 4 5 6 7
```
**Explanation:** Complete binary tree with 3 levels.

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
    def buildTree(self, preorder: list[int], inorder: list[int]) -> TreeNode:
        # start your solution
        if not preorder or not inorder:
            return None
        
        inorder_map = {val: idx for idx, val in enumerate(inorder)}
        self.preorder_idx = 0
        
        def helper(left: int, right: int) -> TreeNode:
            if left > right:
                return None
            
            root_val = preorder[self.preorder_idx]
            self.preorder_idx += 1
            
            root = TreeNode(root_val)
            inorder_idx = inorder_map[root_val]
            
            root.left = helper(left, inorder_idx - 1)
            root.right = helper(inorder_idx + 1, right)
            
            return root
        
        return helper(0, len(inorder) - 1)
        # end your solution


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
    preorder = list(map(int, input().split()))
    inorder = list(map(int, input().split()))
    
    sol = Solution()
    root = sol.buildTree(preorder, inorder)
    
    result = tree_to_list(root)
    print(" ".join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int preorderIdx;
    unordered_map<int, int> inorderMap;
    
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        // start your solution
        preorderIdx = 0;
        for (int i = 0; i < inorder.size(); i++) {
            inorderMap[inorder[i]] = i;
        }
        return helper(preorder, 0, inorder.size() - 1);
    }
    
private:
    TreeNode* helper(vector<int>& preorder, int left, int right) {
        if (left > right) {
            return nullptr;
        }
        
        int rootVal = preorder[preorderIdx++];
        TreeNode* root = new TreeNode(rootVal);
        int inorderIdx = inorderMap[rootVal];
        
        root->left = helper(preorder, left, inorderIdx - 1);
        root->right = helper(preorder, inorderIdx + 1, right);
        
        return root;
        // end your solution
    }
};

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
    
    vector<int> preorder(n), inorder(n);
    for (int i = 0; i < n; i++) {
        cin >> preorder[i];
    }
    for (int i = 0; i < n; i++) {
        cin >> inorder[i];
    }
    
    Solution sol;
    TreeNode* root = sol.buildTree(preorder, inorder);
    
    vector<int> result = treeToList(root);
    for (int i = 0; i < result.size(); i++) {
        if (i > 0) cout << " ";
        cout << result[i];
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
    private int preorderIdx;
    private Map<Integer, Integer> inorderMap;
    
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // start your solution
        preorderIdx = 0;
        inorderMap = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        return helper(preorder, 0, inorder.length - 1);
    }
    
    private TreeNode helper(int[] preorder, int left, int right) {
        if (left > right) {
            return null;
        }
        
        int rootVal = preorder[preorderIdx++];
        TreeNode root = new TreeNode(rootVal);
        int inorderIdx = inorderMap.get(rootVal);
        
        root.left = helper(preorder, left, inorderIdx - 1);
        root.right = helper(preorder, inorderIdx + 1, right);
        
        return root;
        // end your solution
    }
}

public class Main {
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
        int[] preorder = new int[n];
        int[] inorder = new int[n];
        
        for (int i = 0; i < n; i++) {
            preorder[i] = sc.nextInt();
        }
        for (int i = 0; i < n; i++) {
            inorder[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        TreeNode root = sol.buildTree(preorder, inorder);
        
        List<Integer> result = treeToList(root);
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.size(); i++) {
            if (i > 0) sb.append(" ");
            sb.append(result.get(i));
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
    def buildTree(self, preorder: list[int], inorder: list[int]) -> TreeNode:
        # start your solution
        
        
        
        # end your solution


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
    preorder = list(map(int, input().split()))
    inorder = list(map(int, input().split()))
    
    sol = Solution()
    root = sol.buildTree(preorder, inorder)
    
    result = tree_to_list(root)
    print(" ".join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        // start your solution
        
        
        
        // end your solution
    }
};

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
    
    vector<int> preorder(n), inorder(n);
    for (int i = 0; i < n; i++) {
        cin >> preorder[i];
    }
    for (int i = 0; i < n; i++) {
        cin >> inorder[i];
    }
    
    Solution sol;
    TreeNode* root = sol.buildTree(preorder, inorder);
    
    vector<int> result = treeToList(root);
    for (int i = 0; i < result.size(); i++) {
        if (i > 0) cout << " ";
        cout << result[i];
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
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
        int[] preorder = new int[n];
        int[] inorder = new int[n];
        
        for (int i = 0; i < n; i++) {
            preorder[i] = sc.nextInt();
        }
        for (int i = 0; i < n; i++) {
            inorder[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        TreeNode root = sol.buildTree(preorder, inorder);
        
        List<Integer> result = treeToList(root);
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.size(); i++) {
            if (i > 0) sb.append(" ");
            sb.append(result.get(i));
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```