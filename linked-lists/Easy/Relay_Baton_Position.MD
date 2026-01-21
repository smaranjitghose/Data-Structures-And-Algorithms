# Relay Baton Position

### Problem Statement

At the Jawaharlal Nehru Stadium in Delhi, a relay race team is practicing. The coach needs to identify the middle runner to hand over the baton during a special training drill. If there are two middle runners (even count), select the second middle one.

Given the head of a singly linked list representing runners' jersey numbers, return the middle node. If there are two middle nodes, return the second middle node.

### Input Format

- A single line containing space-separated integers representing jersey numbers.

### Output Format

- Print the jersey numbers from the middle node to the end, space-separated.

### Constraints

- `1 <= n <= 100` (number of runners)
- `1 <= Node.val <= 100`

### Test Cases

#### Test Case 1
**Input:**
```
1 2 3 4 5
```
**Output:**
```
3 4 5
```
**Explanation:** 5 runners. Middle is at index 2 (0-indexed). Node with value 3 is the middle. Output from middle to end.

---

#### Test Case 2
**Input:**
```
1 2 3 4 5 6
```
**Output:**
```
4 5 6
```
**Explanation:** 6 runners (even). Two middles: 3 and 4. Return second middle (4). Output: 4→5→6.

---

#### Test Case 3
**Input:**
```
7
```
**Output:**
```
7
```
**Explanation:** Single runner is the middle. Output: 7.

---

#### Test Case 4
**Input:**
```
10 20
```
**Output:**
```
20
```
**Explanation:** Two runners. Second middle is 20.

---

#### Test Case 5
**Input:**
```
1 2 3
```
**Output:**
```
2 3
```
**Explanation:** Three runners. Middle is 2. Output: 2→3.

---

#### Test Case 6
**Input:**
```
5 10 15 20 25 30 35
```
**Output:**
```
20 25 30 35
```
**Explanation:** 7 runners. Middle at index 3 (value 20). Output from 20 to end.

---

#### Test Case 7
**Input:**
```
11 22 33 44
```
**Output:**
```
33 44
```
**Explanation:** 4 runners. Two middles: 22 and 33. Return second middle (33). Output: 33→44.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        # start your solution
        slow = head
        fast = head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        
        return slow
        # end your solution


def buildList(arr):
    if not arr:
        return None
    dummy = ListNode(0)
    curr = dummy
    for val in arr:
        curr.next = ListNode(val)
        curr = curr.next
    return dummy.next

def printList(head):
    result = []
    while head:
        result.append(str(head.val))
        head = head.next
    print(' '.join(result))

def main():
    arr = list(map(int, input().split()))
    head = buildList(arr)
    
    sol = Solution()
    result = sol.middleNode(head)
    printList(result)


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
    ListNode* middleNode(ListNode* head) {
        // start your solution
        ListNode* slow = head;
        ListNode* fast = head;
        
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        return slow;
        // end your solution
    }
};

ListNode* buildList(vector<int>& arr) {
    if (arr.empty()) return nullptr;
    ListNode dummy(0);
    ListNode* curr = &dummy;
    for (int val : arr) {
        curr->next = new ListNode(val);
        curr = curr->next;
    }
    return dummy.next;
}

void printList(ListNode* head) {
    while (head) {
        cout << head->val;
        if (head->next) cout << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string line;
    getline(cin, line);
    
    vector<int> arr;
    stringstream ss(line);
    int num;
    while (ss >> num) arr.push_back(num);
    
    ListNode* head = buildList(arr);
    
    Solution sol;
    ListNode* result = sol.middleNode(head);
    printList(result);
    
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
    public ListNode middleNode(ListNode head) {
        // start your solution
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
        // end your solution
    }
}

public class Main {
    public static ListNode buildList(int[] arr) {
        if (arr.length == 0) return null;
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        for (int val : arr) {
            curr.next = new ListNode(val);
            curr = curr.next;
        }
        return dummy.next;
    }
    
    public static void printList(ListNode head) {
        StringBuilder sb = new StringBuilder();
        while (head != null) {
            sb.append(head.val);
            if (head.next != null) sb.append(" ");
            head = head.next;
        }
        System.out.println(sb.toString());
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String[] parts = sc.nextLine().split(" ");
        int[] arr = new int[parts.length];
        for (int i = 0; i < parts.length; i++) {
            arr[i] = Integer.parseInt(parts[i]);
        }
        
        ListNode head = buildList(arr);
        
        Solution sol = new Solution();
        ListNode result = sol.middleNode(head);
        printList(result);
        
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
    def middleNode(self, head: ListNode) -> ListNode:
        # start your solution
        
        
        
        # end your solution


def buildList(arr):
    if not arr:
        return None
    dummy = ListNode(0)
    curr = dummy
    for val in arr:
        curr.next = ListNode(val)
        curr = curr.next
    return dummy.next

def printList(head):
    result = []
    while head:
        result.append(str(head.val))
        head = head.next
    print(' '.join(result))

def main():
    arr = list(map(int, input().split()))
    head = buildList(arr)
    
    sol = Solution()
    result = sol.middleNode(head)
    printList(result)


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
    ListNode* middleNode(ListNode* head) {
        // start your solution
        
        
        
        // end your solution
    }
};

ListNode* buildList(vector<int>& arr) {
    if (arr.empty()) return nullptr;
    ListNode dummy(0);
    ListNode* curr = &dummy;
    for (int val : arr) {
        curr->next = new ListNode(val);
        curr = curr->next;
    }
    return dummy.next;
}

void printList(ListNode* head) {
    while (head) {
        cout << head->val;
        if (head->next) cout << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string line;
    getline(cin, line);
    
    vector<int> arr;
    stringstream ss(line);
    int num;
    while (ss >> num) arr.push_back(num);
    
    ListNode* head = buildList(arr);
    
    Solution sol;
    ListNode* result = sol.middleNode(head);
    printList(result);
    
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
    public ListNode middleNode(ListNode head) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static ListNode buildList(int[] arr) {
        if (arr.length == 0) return null;
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        for (int val : arr) {
            curr.next = new ListNode(val);
            curr = curr.next;
        }
        return dummy.next;
    }
    
    public static void printList(ListNode head) {
        StringBuilder sb = new StringBuilder();
        while (head != null) {
            sb.append(head.val);
            if (head.next != null) sb.append(" ");
            head = head.next;
        }
        System.out.println(sb.toString());
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String[] parts = sc.nextLine().split(" ");
        int[] arr = new int[parts.length];
        for (int i = 0; i < parts.length; i++) {
            arr[i] = Integer.parseInt(parts[i]);
        }
        
        ListNode head = buildList(arr);
        
        Solution sol = new Solution();
        ListNode result = sol.middleNode(head);
        printList(result);
        
        sc.close();
    }
}
```
