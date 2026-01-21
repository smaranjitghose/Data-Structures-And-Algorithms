# Pipeline Leak Finder

### Problem Statement

The Jal Board in Hyderabad is debugging a water pipeline network. Some pipelines have been incorrectly connected, creating loops that cause pressure imbalance. They need to find exactly where the loop begins.

Given the head of a linked list representing pipeline segments, return the node where the cycle begins. If there is no cycle, return null.

### Input Format

- The first line contains space-separated integers representing segment IDs.
- The second line contains an integer `pos` (-1 if no cycle, otherwise the 0-indexed position where the tail connects back).

### Output Format

- Print the value of the node where the cycle begins, or "no cycle" if there is no cycle.

### Constraints

- `0 <= n <= 10^4` (number of segments)
- `-10^5 <= Node.val <= 10^5`
- `pos` is -1 or a valid index in the list

### Test Cases

#### Test Case 1
**Input:**
```
3 2 0 -4
1
```
**Output:**
```
2
```
**Explanation:** Tail (-4) connects to node at index 1 (value 2). Cycle starts at node with value 2.

---

#### Test Case 2
**Input:**
```
1 2
0
```
**Output:**
```
1
```
**Explanation:** Tail (2) connects back to head (1). Cycle starts at head, value 1.

---

#### Test Case 3
**Input:**
```
1
-1
```
**Output:**
```
no cycle
```
**Explanation:** Single segment with no cycle.

---

#### Test Case 4
**Input:**
```
1 2 3 4 5
-1
```
**Output:**
```
no cycle
```
**Explanation:** Linear pipeline, no loop exists.

---

#### Test Case 5
**Input:**
```
1 2 3 4 5
2
```
**Output:**
```
3
```
**Explanation:** Tail (5) connects to node at index 2 (value 3). Cycle starts at 3.

---

#### Test Case 6
**Input:**
```
10 20 30 40
3
```
**Output:**
```
40
```
**Explanation:** Tail (40) connects to itself (index 3). Single-node cycle at value 40.

---

#### Test Case 7
**Input:**
```
5 10 15 20 25 30
0
```
**Output:**
```
5
```
**Explanation:** Tail (30) connects back to head (5). Entire list is a cycle starting at head.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        # start your solution
        if not head or not head.next:
            return None
        
        # Phase 1: Detect cycle using Floyd's algorithm
        slow = head
        fast = head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            if slow == fast:
                # Phase 2: Find cycle start
                slow = head
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
        
        return None
        # end your solution


def buildListWithCycle(arr, pos):
    if not arr:
        return None
    
    nodes = []
    for val in arr:
        nodes.append(ListNode(val))
    
    for i in range(len(nodes) - 1):
        nodes[i].next = nodes[i + 1]
    
    if pos >= 0:
        nodes[-1].next = nodes[pos]
    
    return nodes[0]

def main():
    line = input().strip()
    pos = int(input())
    
    if line == "empty":
        head = None
    else:
        arr = list(map(int, line.split()))
        head = buildListWithCycle(arr, pos)
    
    sol = Solution()
    result = sol.detectCycle(head)
    
    if result:
        print(result.val)
    else:
        print("no cycle")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <sstream>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
public:
    ListNode* detectCycle(ListNode* head) {
        // start your solution
        if (!head || !head->next) return nullptr;
        
        // Phase 1: Detect cycle
        ListNode* slow = head;
        ListNode* fast = head;
        
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            
            if (slow == fast) {
                // Phase 2: Find cycle start
                slow = head;
                while (slow != fast) {
                    slow = slow->next;
                    fast = fast->next;
                }
                return slow;
            }
        }
        
        return nullptr;
        // end your solution
    }
};

ListNode* buildListWithCycle(vector<int>& arr, int pos) {
    if (arr.empty()) return nullptr;
    
    vector<ListNode*> nodes;
    for (int val : arr) {
        nodes.push_back(new ListNode(val));
    }
    
    for (int i = 0; i < nodes.size() - 1; i++) {
        nodes[i]->next = nodes[i + 1];
    }
    
    if (pos >= 0) {
        nodes.back()->next = nodes[pos];
    }
    
    return nodes[0];
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string line;
    getline(cin, line);
    int pos;
    cin >> pos;
    
    ListNode* head = nullptr;
    if (line != "empty") {
        vector<int> arr;
        stringstream ss(line);
        int num;
        while (ss >> num) arr.push_back(num);
        head = buildListWithCycle(arr, pos);
    }
    
    Solution sol;
    ListNode* result = sol.detectCycle(head);
    
    if (result) {
        cout << result->val << endl;
    } else {
        cout << "no cycle" << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    public ListNode detectCycle(ListNode head) {
        // start your solution
        if (head == null || head.next == null) return null;
        
        // Phase 1: Detect cycle
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            
            if (slow == fast) {
                // Phase 2: Find cycle start
                slow = head;
                while (slow != fast) {
                    slow = slow.next;
                    fast = fast.next;
                }
                return slow;
            }
        }
        
        return null;
        // end your solution
    }
}

public class Main {
    public static ListNode buildListWithCycle(int[] arr, int pos) {
        if (arr.length == 0) return null;
        
        ListNode[] nodes = new ListNode[arr.length];
        for (int i = 0; i < arr.length; i++) {
            nodes[i] = new ListNode(arr[i]);
        }
        
        for (int i = 0; i < nodes.length - 1; i++) {
            nodes[i].next = nodes[i + 1];
        }
        
        if (pos >= 0) {
            nodes[nodes.length - 1].next = nodes[pos];
        }
        
        return nodes[0];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String line = sc.nextLine().trim();
        int pos = Integer.parseInt(sc.nextLine().trim());
        
        ListNode head = null;
        if (!line.equals("empty")) {
            String[] parts = line.split(" ");
            int[] arr = new int[parts.length];
            for (int i = 0; i < parts.length; i++) {
                arr[i] = Integer.parseInt(parts[i]);
            }
            head = buildListWithCycle(arr, pos);
        }
        
        Solution sol = new Solution();
        ListNode result = sol.detectCycle(head);
        
        if (result != null) {
            System.out.println(result.val);
        } else {
            System.out.println("no cycle");
        }
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        # start your solution
        
        
        
        # end your solution


def buildListWithCycle(arr, pos):
    if not arr:
        return None
    
    nodes = []
    for val in arr:
        nodes.append(ListNode(val))
    
    for i in range(len(nodes) - 1):
        nodes[i].next = nodes[i + 1]
    
    if pos >= 0:
        nodes[-1].next = nodes[pos]
    
    return nodes[0]

def main():
    line = input().strip()
    pos = int(input())
    
    if line == "empty":
        head = None
    else:
        arr = list(map(int, line.split()))
        head = buildListWithCycle(arr, pos)
    
    sol = Solution()
    result = sol.detectCycle(head)
    
    if result:
        print(result.val)
    else:
        print("no cycle")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <sstream>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
public:
    ListNode* detectCycle(ListNode* head) {
        // start your solution
        
        
        
        // end your solution
    }
};

ListNode* buildListWithCycle(vector<int>& arr, int pos) {
    if (arr.empty()) return nullptr;
    
    vector<ListNode*> nodes;
    for (int val : arr) {
        nodes.push_back(new ListNode(val));
    }
    
    for (int i = 0; i < nodes.size() - 1; i++) {
        nodes[i]->next = nodes[i + 1];
    }
    
    if (pos >= 0) {
        nodes.back()->next = nodes[pos];
    }
    
    return nodes[0];
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string line;
    getline(cin, line);
    int pos;
    cin >> pos;
    
    ListNode* head = nullptr;
    if (line != "empty") {
        vector<int> arr;
        stringstream ss(line);
        int num;
        while (ss >> num) arr.push_back(num);
        head = buildListWithCycle(arr, pos);
    }
    
    Solution sol;
    ListNode* result = sol.detectCycle(head);
    
    if (result) {
        cout << result->val << endl;
    } else {
        cout << "no cycle" << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    public ListNode detectCycle(ListNode head) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static ListNode buildListWithCycle(int[] arr, int pos) {
        if (arr.length == 0) return null;
        
        ListNode[] nodes = new ListNode[arr.length];
        for (int i = 0; i < arr.length; i++) {
            nodes[i] = new ListNode(arr[i]);
        }
        
        for (int i = 0; i < nodes.length - 1; i++) {
            nodes[i].next = nodes[i + 1];
        }
        
        if (pos >= 0) {
            nodes[nodes.length - 1].next = nodes[pos];
        }
        
        return nodes[0];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String line = sc.nextLine().trim();
        int pos = Integer.parseInt(sc.nextLine().trim());
        
        ListNode head = null;
        if (!line.equals("empty")) {
            String[] parts = line.split(" ");
            int[] arr = new int[parts.length];
            for (int i = 0; i < parts.length; i++) {
                arr[i] = Integer.parseInt(parts[i]);
            }
            head = buildListWithCycle(arr, pos);
        }
        
        Solution sol = new Solution();
        ListNode result = sol.detectCycle(head);
        
        if (result != null) {
            System.out.println(result.val);
        } else {
            System.out.println("no cycle");
        }
        
        sc.close();
    }
}
```
