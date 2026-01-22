# NEET Rank Finder

### Problem Statement

The National Testing Agency (NTA) maintains NEET examination scores in a Binary Search Tree for efficient rank calculations. Each node contains a unique score, with lower scores in the left subtree and higher scores in the right subtree.

After the results are declared, students often want to know which score corresponds to a particular rank. Given that an inorder traversal of a BST gives values in sorted order, the kth smallest score represents the student ranked kth from the bottom.

Given the root of a BST containing NEET scores and an integer `k`, return the kth smallest score in the tree. The answer is guaranteed to exist.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node
- Third line contains the integer `k`

### Output Format

- A single integer representing the kth smallest value in the BST

### Constraints

- `1 <= k <= n <= 10^4`
- `0 <= Node.val <= 10^4`

### Test Cases

#### Test Case 1
**Input:**
```
4
3 1 4 -1 2
1
```
**Output:**
```
1
```
**Explanation:** Inorder traversal gives [1, 2, 3, 4]. The 1st smallest is 1.

---

#### Test Case 2
**Input:**
```
6
5 3 6 2 4 -1 -1 1
3
```
**Output:**
```
3
```
**Explanation:** Inorder gives [1, 2, 3, 4, 5, 6]. The 3rd smallest is 3.

---

#### Test Case 3
**Input:**
```
1
42
1
```
**Output:**
```
42
```
**Explanation:** Single node, k=1 returns that node's value.

---

#### Test Case 4
**Input:**
```
7
50 30 70 20 40 60 80
4
```
**Output:**
```
50
```
**Explanation:** Inorder gives [20, 30, 40, 50, 60, 70, 80]. The 4th smallest is 50.

---

#### Test Case 5
**Input:**
```
7
50 30 70 20 40 60 80
1
```
**Output:**
```
20
```
**Explanation:** The 1st smallest (minimum) is 20.

---

#### Test Case 6
**Input:**
```
7
50 30 70 20 40 60 80
7
```
**Output:**
```
80
```
**Explanation:** The 7th smallest (maximum in a 7-node tree) is 80.

---

#### Test Case 7
**Input:**
```
5
4 2 6 1 3
2
```
**Output:**
```
2
```
**Explanation:** Inorder gives [1, 2, 3, 4, 6]. The 2nd smallest is 2.

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
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        # start your solution
        self.count = 0
        self.result = 0
        
        def inorder(node: TreeNode):
            if not node or self.count >= k:
                return
            
            inorder(node.left)
            
            self.count += 1
            if self.count == k:
                self.result = node.val
                return
            
            inorder(node.right)
        
        inorder(root)
        return self.result
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
    k = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    print(sol.kthSmallest(root, k))


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
    int count = 0;
    int result = 0;
    
    int kthSmallest(TreeNode* root, int k) {
        // start your solution
        count = 0;
        result = 0;
        inorder(root, k);
        return result;
    }
    
private:
    void inorder(TreeNode* node, int k) {
        if (node == nullptr || count >= k) {
            return;
        }
        
        inorder(node->left, k);
        
        count++;
        if (count == k) {
            result = node->val;
            return;
        }
        
        inorder(node->right, k);
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
    
    int k;
    cin >> k;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    cout << sol.kthSmallest(root, k) << endl;
    
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
    private int count = 0;
    private int result = 0;
    
    public int kthSmallest(TreeNode root, int k) {
        // start your solution
        count = 0;
        result = 0;
        inorder(root, k);
        return result;
    }
    
    private void inorder(TreeNode node, int k) {
        if (node == null || count >= k) {
            return;
        }
        
        inorder(node.left, k);
        
        count++;
        if (count == k) {
            result = node.val;
            return;
        }
        
        inorder(node.right, k);
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
        int k = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        System.out.println(sol.kthSmallest(root, k));
        
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
    def kthSmallest(self, root: TreeNode, k: int) -> int:
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
    k = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    print(sol.kthSmallest(root, k))


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
    int kthSmallest(TreeNode* root, int k) {
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
    
    int k;
    cin >> k;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    cout << sol.kthSmallest(root, k) << endl;
    
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
    public int kthSmallest(TreeNode root, int k) {
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
        int k = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        System.out.println(sol.kthSmallest(root, k));
        
        sc.close();
    }
}
```
