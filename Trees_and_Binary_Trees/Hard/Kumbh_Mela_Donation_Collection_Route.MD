# Kumbh Mela Donation Collection Route

### Problem Statement

During the Kumbh Mela in Prayagraj, charitable organizations have set up donation collection points across the mela grounds. The layout of these collection points forms a binary tree structure, where each node represents a collection point with a certain amount of donations (which can be positive or negative if expenses exceed collections at that point).

A volunteer can walk along any path in the tree to collect donations. A path is defined as any sequence of nodes where each pair of adjacent nodes has a direct connection. The path must contain at least one node and does not need to pass through the root. The volunteer wants to find the route that maximizes the total donations collected.

Given the root of the binary tree representing the donation collection points, return the maximum path sum. A path sum is the sum of the node values in the path.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the tree, where `-1001` denotes a null node (since valid values are -1000 to 1000)

### Output Format

- A single integer representing the maximum path sum

### Constraints

- `1 <= n <= 3 * 10^4`
- `-1000 <= Node.val <= 1000`

### Test Cases

#### Test Case 1
**Input:**
```
3
1 2 3
```
**Output:**
```
6
```
**Explanation:** The optimal path is 2 → 1 → 3 with sum 2 + 1 + 3 = 6.

---

#### Test Case 2
**Input:**
```
5
-10 9 20 -1001 -1001 15 7
```
**Output:**
```
42
```
**Explanation:** The optimal path is 15 → 20 → 7 with sum 15 + 20 + 7 = 42.

---

#### Test Case 3
**Input:**
```
1
-3
```
**Output:**
```
-3
```
**Explanation:** Single negative node - we must include at least one node.

---

#### Test Case 4
**Input:**
```
3
2 -1 -2
```
**Output:**
```
2
```
**Explanation:** Best path is just the root node with value 2.

---

#### Test Case 5
**Input:**
```
7
1 2 3 4 5 6 7
```
**Output:**
```
18
```
**Explanation:** The optimal path is 4 → 2 → 1 → 3 → 7 or similar with maximum sum.

---

#### Test Case 6
**Input:**
```
5
5 4 8 11 -1001 13 4
```
**Output:**
```
48
```
**Explanation:** Path 11 → 4 → 5 → 8 → 13 gives sum 48.

---

#### Test Case 7
**Input:**
```
7
-1 -2 -3 -4 -5 -6 -7
```
**Output:**
```
-1
```
**Explanation:** All negative values. The maximum is the root alone with value -1.

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
    def maxPathSum(self, root: TreeNode) -> int:
        # start your solution
        self.max_sum = float('-inf')
        
        def max_gain(node: TreeNode) -> int:
            if not node:
                return 0
            
            left_gain = max(max_gain(node.left), 0)
            right_gain = max(max_gain(node.right), 0)
            
            path_sum = node.val + left_gain + right_gain
            self.max_sum = max(self.max_sum, path_sum)
            
            return node.val + max(left_gain, right_gain)
        
        max_gain(root)
        return self.max_sum
        # end your solution


def build_tree(values: list) -> TreeNode:
    if not values or values[0] == -1001:
        return None
    
    root = TreeNode(values[0])
    queue = [root]
    i = 1
    
    while queue and i < len(values):
        node = queue.pop(0)
        
        if i < len(values) and values[i] != -1001:
            node.left = TreeNode(values[i])
            queue.append(node.left)
        i += 1
        
        if i < len(values) and values[i] != -1001:
            node.right = TreeNode(values[i])
            queue.append(node.right)
        i += 1
    
    return root


def main():
    n = int(input())
    values = list(map(int, input().split()))
    root = build_tree(values)
    
    sol = Solution()
    print(sol.maxPathSum(root))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
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
    int maxSum;
    
    int maxPathSum(TreeNode* root) {
        // start your solution
        maxSum = INT_MIN;
        maxGain(root);
        return maxSum;
    }
    
private:
    int maxGain(TreeNode* node) {
        if (node == nullptr) {
            return 0;
        }
        
        int leftGain = max(maxGain(node->left), 0);
        int rightGain = max(maxGain(node->right), 0);
        
        int pathSum = node->val + leftGain + rightGain;
        maxSum = max(maxSum, pathSum);
        
        return node->val + max(leftGain, rightGain);
        // end your solution
    }
};

TreeNode* buildTree(vector<int>& values) {
    if (values.empty() || values[0] == -1001) {
        return nullptr;
    }
    
    TreeNode* root = new TreeNode(values[0]);
    queue<TreeNode*> q;
    q.push(root);
    int i = 1;
    
    while (!q.empty() && i < values.size()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (i < values.size() && values[i] != -1001) {
            node->left = new TreeNode(values[i]);
            q.push(node->left);
        }
        i++;
        
        if (i < values.size() && values[i] != -1001) {
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
    cout << sol.maxPathSum(root) << endl;
    
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
    private int maxSum;
    
    public int maxPathSum(TreeNode root) {
        // start your solution
        maxSum = Integer.MIN_VALUE;
        maxGain(root);
        return maxSum;
    }
    
    private int maxGain(TreeNode node) {
        if (node == null) {
            return 0;
        }
        
        int leftGain = Math.max(maxGain(node.left), 0);
        int rightGain = Math.max(maxGain(node.right), 0);
        
        int pathSum = node.val + leftGain + rightGain;
        maxSum = Math.max(maxSum, pathSum);
        
        return node.val + Math.max(leftGain, rightGain);
        // end your solution
    }
}

public class Main {
    public static TreeNode buildTree(int[] values) {
        if (values.length == 0 || values[0] == -1001) {
            return null;
        }
        
        TreeNode root = new TreeNode(values[0]);
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int i = 1;
        
        while (!queue.isEmpty() && i < values.length) {
            TreeNode node = queue.poll();
            
            if (i < values.length && values[i] != -1001) {
                node.left = new TreeNode(values[i]);
                queue.offer(node.left);
            }
            i++;
            
            if (i < values.length && values[i] != -1001) {
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
        System.out.println(sol.maxPathSum(root));
        
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
    def maxPathSum(self, root: TreeNode) -> int:
        # start your solution
        
        
        
        # end your solution


def build_tree(values: list) -> TreeNode:
    if not values or values[0] == -1001:
        return None
    
    root = TreeNode(values[0])
    queue = [root]
    i = 1
    
    while queue and i < len(values):
        node = queue.pop(0)
        
        if i < len(values) and values[i] != -1001:
            node.left = TreeNode(values[i])
            queue.append(node.left)
        i += 1
        
        if i < len(values) and values[i] != -1001:
            node.right = TreeNode(values[i])
            queue.append(node.right)
        i += 1
    
    return root


def main():
    n = int(input())
    values = list(map(int, input().split()))
    root = build_tree(values)
    
    sol = Solution()
    print(sol.maxPathSum(root))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
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
    int maxPathSum(TreeNode* root) {
        // start your solution
        
        
        
        // end your solution
    }
};

TreeNode* buildTree(vector<int>& values) {
    if (values.empty() || values[0] == -1001) {
        return nullptr;
    }
    
    TreeNode* root = new TreeNode(values[0]);
    queue<TreeNode*> q;
    q.push(root);
    int i = 1;
    
    while (!q.empty() && i < values.size()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (i < values.size() && values[i] != -1001) {
            node->left = new TreeNode(values[i]);
            q.push(node->left);
        }
        i++;
        
        if (i < values.size() && values[i] != -1001) {
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
    cout << sol.maxPathSum(root) << endl;
    
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
    public int maxPathSum(TreeNode root) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static TreeNode buildTree(int[] values) {
        if (values.length == 0 || values[0] == -1001) {
            return null;
        }
        
        TreeNode root = new TreeNode(values[0]);
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int i = 1;
        
        while (!queue.isEmpty() && i < values.length) {
            TreeNode node = queue.poll();
            
            if (i < values.length && values[i] != -1001) {
                node.left = new TreeNode(values[i]);
                queue.offer(node.left);
            }
            i++;
            
            if (i < values.length && values[i] != -1001) {
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
        System.out.println(sol.maxPathSum(root));
        
        sc.close();
    }
}
```
