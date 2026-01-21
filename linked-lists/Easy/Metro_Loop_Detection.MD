# Metro Loop Detection

### Problem Statement

The Bangalore Metro Rail Corporation (BMRC) is debugging their route mapping system. Some routes have been incorrectly configured to loop back to a previous station, causing trains to run indefinitely in a cycle.

Given the head of a linked list representing metro stations, determine if the route contains a cycle. A cycle exists if some station can be reached again by continuously following the next pointer.

Return `true` if there is a cycle, otherwise return `false`.

### Input Format

- The first line contains space-separated integers representing station IDs.
- The second line contains an integer `pos` (-1 if no cycle, otherwise the 0-indexed position where the tail connects back).

### Output Format

- Print `true` if cycle exists, otherwise `false`.

### Constraints

- `0 <= n <= 10^4` (number of stations)
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
true
```
**Explanation:** Tail (-4) connects back to station at index 1 (value 2). Cycle: 2→0→-4→2...

---

#### Test Case 2
**Input:**
```
1 2
0
```
**Output:**
```
true
```
**Explanation:** Tail (2) connects back to head (1). Cycle: 1→2→1...

---

#### Test Case 3
**Input:**
```
1
-1
```
**Output:**
```
false
```
**Explanation:** Single station with no cycle. Tail points to null.

---

#### Test Case 4
**Input:**
```
1 2 3 4 5
-1
```
**Output:**
```
false
```
**Explanation:** Linear route with no cycle. Last station points to null.

---

#### Test Case 5
**Input:**
```
1 2 3 4 5
4
```
**Output:**
```
true
```
**Explanation:** Tail (5) connects back to itself (index 4). Single-node cycle at end.

---

#### Test Case 6
**Input:**
```
10 20 30 40 50
2
```
**Output:**
```
true
```
**Explanation:** Tail (50) connects to station at index 2 (value 30). Cycle: 30→40→50→30...

---

#### Test Case 7
**Input:**
```
empty
-1
```
**Output:**
```
false
```
**Explanation:** Empty route has no cycle.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        # start your solution
        if not head or not head.next:
            return False
        
        slow = head
        fast = head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            if slow == fast:
                return True
        
        return False
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
    result = sol.hasCycle(head)
    print("true" if result else "false")


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
    bool hasCycle(ListNode* head) {
        // start your solution
        if (!head || !head->next) return false;
        
        ListNode* slow = head;
        ListNode* fast = head;
        
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            
            if (slow == fast) return true;
        }
        
        return false;
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
    cout << (sol.hasCycle(head) ? "true" : "false") << endl;
    
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
    public boolean hasCycle(ListNode head) {
        // start your solution
        if (head == null || head.next == null) return false;
        
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            
            if (slow == fast) return true;
        }
        
        return false;
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
        System.out.println(sol.hasCycle(head) ? "true" : "false");
        
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
    def hasCycle(self, head: ListNode) -> bool:
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
    result = sol.hasCycle(head)
    print("true" if result else "false")


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
    bool hasCycle(ListNode* head) {
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
    cout << (sol.hasCycle(head) ? "true" : "false") << endl;
    
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
    public boolean hasCycle(ListNode head) {
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
        System.out.println(sol.hasCycle(head) ? "true" : "false");
        
        sc.close();
    }
}
```
