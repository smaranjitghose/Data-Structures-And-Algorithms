# JEE Main Cutoff Neighbors

### Problem Statement

The National Testing Agency (NTA) stores JEE Main cutoff scores for various engineering colleges in a Binary Search Tree. Each node contains a unique cutoff score, with lower scores in the left subtree and higher scores in the right subtree.

A student with a specific score wants to find the `k` colleges whose cutoff scores are closest to their score. This helps them understand which colleges they're most likely to get admission to, considering both colleges where they just qualify and those where they're slightly below the cutoff.

Given the root of a BST, a target score, and an integer `k`, return the `k` values in the BST that are closest to the target. The answer can be returned in any order.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node
- Third line contains the target value (can be a decimal)
- Fourth line contains the integer `k`

### Output Format

- Print `k` space-separated integers representing the closest values to target
- Values can be in any order

### Constraints

- `1 <= k <= n <= 10^4`
- `0 <= Node.val <= 10^9`

### Test Cases

#### Test Case 1
**Input:**
```
5
4 2 5 1 3
3.7
2
```
**Output:**
```
4 3
```
**Explanation:** Values closest to 3.7 are 4 (distance 0.3) and 3 (distance 0.7).

---

#### Test Case 2
**Input:**
```
1
1
0.0
1
```
**Output:**
```
1
```
**Explanation:** Only one node, so it's the closest.

---

#### Test Case 3
**Input:**
```
7
50 30 70 20 40 60 80
45.0
3
```
**Output:**
```
40 50 30
```
**Explanation:** Distances: 40→5, 50→5, 30→15, 60→15, 20→25, 70→25, 80→35. Top 3 closest: 40, 50, 30.

---

#### Test Case 4
**Input:**
```
5
4 2 5 1 3
3.0
2
```
**Output:**
```
3 2
```
**Explanation:** Value 3 has distance 0, value 2 has distance 1.

---

#### Test Case 5
**Input:**
```
7
100 50 150 25 75 125 175
100.0
4
```
**Output:**
```
100 75 125 50
```
**Explanation:** 100 is exact match, then 75 and 125 (distance 25), then 50 (distance 50).

---

#### Test Case 6
**Input:**
```
3
2 1 3
2.5
3
```
**Output:**
```
2 3 1
```
**Explanation:** All 3 values returned. Distances: 2→0.5, 3→0.5, 1→1.5.

---

#### Test Case 7
**Input:**
```
7
8 4 12 2 6 10 14
7.0
3
```
**Output:**
```
8 6 4
```
**Explanation:** Distances: 6→1, 8→1, 4→3, 10→3, 12→5, 2→5, 14→7.

---

### Solutions

#### Python
```python
import heapq


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def closestKValues(self, root: TreeNode, target: float, k: int) -> list[int]:
        # start your solution
        heap = []
        
        def inorder(node: TreeNode):
            if not node:
                return
            
            inorder(node.left)
            
            diff = abs(node.val - target)
            if len(heap) < k:
                heapq.heappush(heap, (-diff, node.val))
            elif diff < -heap[0][0]:
                heapq.heappop(heap)
                heapq.heappush(heap, (-diff, node.val))
            
            inorder(node.right)
        
        inorder(root)
        return [val for _, val in heap]
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
    target = float(input())
    k = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.closestKValues(root, target, k)
    
    print(" ".join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <cmath>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    vector<int> closestKValues(TreeNode* root, double target, int k) {
        // start your solution
        priority_queue<pair<double, int>> maxHeap;
        inorder(root, target, k, maxHeap);
        
        vector<int> result;
        while (!maxHeap.empty()) {
            result.push_back(maxHeap.top().second);
            maxHeap.pop();
        }
        return result;
    }
    
private:
    void inorder(TreeNode* node, double target, int k, priority_queue<pair<double, int>>& maxHeap) {
        if (node == nullptr) return;
        
        inorder(node->left, target, k, maxHeap);
        
        double diff = abs(node->val - target);
        if (maxHeap.size() < k) {
            maxHeap.push({diff, node->val});
        } else if (diff < maxHeap.top().first) {
            maxHeap.pop();
            maxHeap.push({diff, node->val});
        }
        
        inorder(node->right, target, k, maxHeap);
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
    
    double target;
    cin >> target;
    
    int k;
    cin >> k;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    vector<int> result = sol.closestKValues(root, target, k);
    
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
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        // start your solution
        PriorityQueue<double[]> maxHeap = new PriorityQueue<>((a, b) -> Double.compare(b[0], a[0]));
        inorder(root, target, k, maxHeap);
        
        List<Integer> result = new ArrayList<>();
        while (!maxHeap.isEmpty()) {
            result.add((int) maxHeap.poll()[1]);
        }
        return result;
    }
    
    private void inorder(TreeNode node, double target, int k, PriorityQueue<double[]> maxHeap) {
        if (node == null) return;
        
        inorder(node.left, target, k, maxHeap);
        
        double diff = Math.abs(node.val - target);
        if (maxHeap.size() < k) {
            maxHeap.offer(new double[]{diff, node.val});
        } else if (diff < maxHeap.peek()[0]) {
            maxHeap.poll();
            maxHeap.offer(new double[]{diff, node.val});
        }
        
        inorder(node.right, target, k, maxHeap);
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
        double target = sc.nextDouble();
        int k = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        List<Integer> result = sol.closestKValues(root, target, k);
        
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
import heapq


class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def closestKValues(self, root: TreeNode, target: float, k: int) -> list[int]:
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
    target = float(input())
    k = int(input())
    
    root = build_tree(values)
    
    sol = Solution()
    result = sol.closestKValues(root, target, k)
    
    print(" ".join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <cmath>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    vector<int> closestKValues(TreeNode* root, double target, int k) {
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
    
    double target;
    cin >> target;
    
    int k;
    cin >> k;
    
    TreeNode* root = buildTree(values);
    
    Solution sol;
    vector<int> result = sol.closestKValues(root, target, k);
    
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
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
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
        double target = sc.nextDouble();
        int k = sc.nextInt();
        
        TreeNode root = buildTree(values);
        
        Solution sol = new Solution();
        List<Integer> result = sol.closestKValues(root, target, k);
        
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
