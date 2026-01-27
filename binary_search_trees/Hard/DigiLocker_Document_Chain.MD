# DigiLocker Document Chain

### Problem Statement

DigiLocker, India's digital document storage platform, maintains document IDs in a Binary Search Tree for efficient retrieval. Each node contains a unique document ID, with smaller IDs in the left subtree and larger IDs in the right subtree.

For a new feature that allows sequential document browsing, the system needs to convert the BST into a circular doubly linked list. The conversion should be done in-place, reusing the existing tree nodes. The left pointer of each node should point to its predecessor, and the right pointer should point to its successor. The list should be sorted in ascending order, and the head's left pointer should connect to the tail, while the tail's right pointer should connect to the head, forming a circular structure.

Given the root of a BST, convert it to a sorted circular doubly linked list in-place. Return the pointer to the smallest element of the linked list.

### Input Format

- First line contains the number of nodes `n` in the tree
- Second line contains `n` space-separated values representing the level-order traversal of the BST, where `-1` denotes a null node

### Output Format

- Print the values in the circular doubly linked list traversing forward (using right pointers) starting from the smallest element
- Print all values space-separated
- If tree is empty, print `empty`

### Constraints

- `0 <= n <= 2000`
- `-1000 <= Node.val <= 1000`
- All values are unique

### Test Cases

#### Test Case 1
**Input:**
```
5
4 2 5 1 3
```
**Output:**
```
1 2 3 4 5
```
**Explanation:** BST converted to sorted circular doubly linked list: 1↔2↔3↔4↔5↔(back to 1).

---

#### Test Case 2
**Input:**
```
0

```
**Output:**
```
empty
```
**Explanation:** Empty tree produces empty list.

---

#### Test Case 3
**Input:**
```
1
1
```
**Output:**
```
1
```
**Explanation:** Single node points to itself in both directions.

---

#### Test Case 4
**Input:**
```
3
2 1 3
```
**Output:**
```
1 2 3
```
**Explanation:** Simple three-node BST becomes 1↔2↔3↔(back to 1).

---

#### Test Case 5
**Input:**
```
7
4 2 6 1 3 5 7
```
**Output:**
```
1 2 3 4 5 6 7
```
**Explanation:** Complete BST converted to sorted list.

---

#### Test Case 6
**Input:**
```
4
4 2 -1 1 3
```
**Output:**
```
1 2 3 4
```
**Explanation:** Left-heavy BST converted correctly.

---

#### Test Case 7
**Input:**
```
4
2 -1 4 3 5
```
**Output:**
```
2 3 4 5
```
**Explanation:** Right-heavy BST converted correctly.

---

### Solutions

#### Python
```python
class Node:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def treeToDoublyList(self, root: Node) -> Node:
        # start your solution
        if not root:
            return None
        
        self.first = None
        self.last = None
        
        def inorder(node: Node):
            if not node:
                return
            
            inorder(node.left)
            
            if self.last:
                self.last.right = node
                node.left = self.last
            else:
                self.first = node
            
            self.last = node
            
            inorder(node.right)
        
        inorder(root)
        
        self.last.right = self.first
        self.first.left = self.last
        
        return self.first
        # end your solution


def build_tree(values: list) -> Node:
    if not values or values[0] == -1:
        return None
    
    root = Node(values[0])
    queue = [root]
    i = 1
    
    while queue and i < len(values):
        node = queue.pop(0)
        
        if i < len(values) and values[i] != -1:
            node.left = Node(values[i])
            queue.append(node.left)
        i += 1
        
        if i < len(values) and values[i] != -1:
            node.right = Node(values[i])
            queue.append(node.right)
        i += 1
    
    return root


def main():
    n = int(input())
    if n == 0:
        print("empty")
        return
    
    values = list(map(int, input().split()))
    root = build_tree(values)
    
    sol = Solution()
    head = sol.treeToDoublyList(root)
    
    if not head:
        print("empty")
        return
    
    result = []
    current = head
    while True:
        result.append(current.val)
        current = current.right
        if current == head:
            break
    
    print(" ".join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    Node* first = nullptr;
    Node* last = nullptr;
    
    Node* treeToDoublyList(Node* root) {
        // start your solution
        if (root == nullptr) {
            return nullptr;
        }
        
        first = nullptr;
        last = nullptr;
        
        inorder(root);
        
        last->right = first;
        first->left = last;
        
        return first;
    }
    
private:
    void inorder(Node* node) {
        if (node == nullptr) return;
        
        inorder(node->left);
        
        if (last != nullptr) {
            last->right = node;
            node->left = last;
        } else {
            first = node;
        }
        
        last = node;
        
        inorder(node->right);
        // end your solution
    }
};

Node* buildTree(vector<int>& values) {
    if (values.empty() || values[0] == -1) {
        return nullptr;
    }
    
    Node* root = new Node(values[0]);
    queue<Node*> q;
    q.push(root);
    int i = 1;
    
    while (!q.empty() && i < values.size()) {
        Node* node = q.front();
        q.pop();
        
        if (i < values.size() && values[i] != -1) {
            node->left = new Node(values[i]);
            q.push(node->left);
        }
        i++;
        
        if (i < values.size() && values[i] != -1) {
            node->right = new Node(values[i]);
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
    
    if (n == 0) {
        cout << "empty" << endl;
        return 0;
    }
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    Node* root = buildTree(values);
    
    Solution sol;
    Node* head = sol.treeToDoublyList(root);
    
    if (head == nullptr) {
        cout << "empty" << endl;
        return 0;
    }
    
    vector<int> result;
    Node* current = head;
    do {
        result.push_back(current->val);
        current = current->right;
    } while (current != head);
    
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

class Node {
    int val;
    Node left;
    Node right;
    Node(int val) { this.val = val; }
}

class Solution {
    private Node first = null;
    private Node last = null;
    
    public Node treeToDoublyList(Node root) {
        // start your solution
        if (root == null) {
            return null;
        }
        
        first = null;
        last = null;
        
        inorder(root);
        
        last.right = first;
        first.left = last;
        
        return first;
    }
    
    private void inorder(Node node) {
        if (node == null) return;
        
        inorder(node.left);
        
        if (last != null) {
            last.right = node;
            node.left = last;
        } else {
            first = node;
        }
        
        last = node;
        
        inorder(node.right);
        // end your solution
    }
}

public class Main {
    public static Node buildTree(int[] values) {
        if (values.length == 0 || values[0] == -1) {
            return null;
        }
        
        Node root = new Node(values[0]);
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        int i = 1;
        
        while (!queue.isEmpty() && i < values.length) {
            Node node = queue.poll();
            
            if (i < values.length && values[i] != -1) {
                node.left = new Node(values[i]);
                queue.offer(node.left);
            }
            i++;
            
            if (i < values.length && values[i] != -1) {
                node.right = new Node(values[i]);
                queue.offer(node.right);
            }
            i++;
        }
        
        return root;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        if (n == 0) {
            System.out.println("empty");
            sc.close();
            return;
        }
        
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        
        Node root = buildTree(values);
        
        Solution sol = new Solution();
        Node head = sol.treeToDoublyList(root);
        
        if (head == null) {
            System.out.println("empty");
            sc.close();
            return;
        }
        
        List<Integer> result = new ArrayList<>();
        Node current = head;
        do {
            result.add(current.val);
            current = current.right;
        } while (current != head);
        
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
class Node:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def treeToDoublyList(self, root: Node) -> Node:
        # start your solution
        
        
        
        # end your solution


def build_tree(values: list) -> Node:
    if not values or values[0] == -1:
        return None
    
    root = Node(values[0])
    queue = [root]
    i = 1
    
    while queue and i < len(values):
        node = queue.pop(0)
        
        if i < len(values) and values[i] != -1:
            node.left = Node(values[i])
            queue.append(node.left)
        i += 1
        
        if i < len(values) and values[i] != -1:
            node.right = Node(values[i])
            queue.append(node.right)
        i += 1
    
    return root


def main():
    n = int(input())
    if n == 0:
        print("empty")
        return
    
    values = list(map(int, input().split()))
    root = build_tree(values)
    
    sol = Solution()
    head = sol.treeToDoublyList(root)
    
    if not head:
        print("empty")
        return
    
    result = []
    current = head
    while True:
        result.append(current.val)
        current = current.right
        if current == head:
            break
    
    print(" ".join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    Node* treeToDoublyList(Node* root) {
        // start your solution
        
        
        
        // end your solution
    }
};

Node* buildTree(vector<int>& values) {
    if (values.empty() || values[0] == -1) {
        return nullptr;
    }
    
    Node* root = new Node(values[0]);
    queue<Node*> q;
    q.push(root);
    int i = 1;
    
    while (!q.empty() && i < values.size()) {
        Node* node = q.front();
        q.pop();
        
        if (i < values.size() && values[i] != -1) {
            node->left = new Node(values[i]);
            q.push(node->left);
        }
        i++;
        
        if (i < values.size() && values[i] != -1) {
            node->right = new Node(values[i]);
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
    
    if (n == 0) {
        cout << "empty" << endl;
        return 0;
    }
    
    vector<int> values(n);
    for (int i = 0; i < n; i++) {
        cin >> values[i];
    }
    
    Node* root = buildTree(values);
    
    Solution sol;
    Node* head = sol.treeToDoublyList(root);
    
    if (head == nullptr) {
        cout << "empty" << endl;
        return 0;
    }
    
    vector<int> result;
    Node* current = head;
    do {
        result.push_back(current->val);
        current = current->right;
    } while (current != head);
    
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

class Node {
    int val;
    Node left;
    Node right;
    Node(int val) { this.val = val; }
}

class Solution {
    public Node treeToDoublyList(Node root) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static Node buildTree(int[] values) {
        if (values.length == 0 || values[0] == -1) {
            return null;
        }
        
        Node root = new Node(values[0]);
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        int i = 1;
        
        while (!queue.isEmpty() && i < values.length) {
            Node node = queue.poll();
            
            if (i < values.length && values[i] != -1) {
                node.left = new Node(values[i]);
                queue.offer(node.left);
            }
            i++;
            
            if (i < values.length && values[i] != -1) {
                node.right = new Node(values[i]);
                queue.offer(node.right);
            }
            i++;
        }
        
        return root;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        if (n == 0) {
            System.out.println("empty");
            sc.close();
            return;
        }
        
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        
        Node root = buildTree(values);
        
        Solution sol = new Solution();
        Node head = sol.treeToDoublyList(root);
        
        if (head == null) {
            System.out.println("empty");
            sc.close();
            return;
        }
        
        List<Integer> result = new ArrayList<>();
        Node current = head;
        do {
            result.add(current.val);
            current = current.right;
        } while (current != head);
        
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
