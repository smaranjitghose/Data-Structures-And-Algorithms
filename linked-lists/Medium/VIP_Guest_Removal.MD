# VIP Guest Removal

### Problem Statement

At a state banquet in Rashtrapati Bhavan, New Delhi, the protocol officer maintains a guest list as a linked list. Due to a last-minute security concern, the nth guest from the end of the list must be removed.

Given the head of a linked list representing guest IDs, remove the nth node from the end of the list and return the updated list.

### Input Format

- The first line contains space-separated integers representing guest IDs.
- The second line contains an integer `n`, the position from the end to remove.

### Output Format

- Print the updated guest list as space-separated integers, or "empty" if the list becomes empty.

### Constraints

- `1 <= size of list <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= size of list`

### Test Cases

#### Test Case 1
**Input:**
```
1 2 3 4 5
2
```
**Output:**
```
1 2 3 5
```
**Explanation:** Remove 2nd from end (value 4). List becomes 1→2→3→5.

---

#### Test Case 2
**Input:**
```
1
1
```
**Output:**
```
empty
```
**Explanation:** Single guest, remove 1st from end. List becomes empty.

---

#### Test Case 3
**Input:**
```
1 2
1
```
**Output:**
```
1
```
**Explanation:** Remove 1st from end (value 2). List becomes 1.

---

#### Test Case 4
**Input:**
```
1 2
2
```
**Output:**
```
2
```
**Explanation:** Remove 2nd from end (value 1, the head). List becomes 2.

---

#### Test Case 5
**Input:**
```
10 20 30 40 50
5
```
**Output:**
```
20 30 40 50
```
**Explanation:** Remove 5th from end (the head, value 10). List becomes 20→30→40→50.

---

#### Test Case 6
**Input:**
```
1 2 3 4 5 6 7
3
```
**Output:**
```
1 2 3 4 6 7
```
**Explanation:** Remove 3rd from end (value 5). List becomes 1→2→3→4→6→7.

---

#### Test Case 7
**Input:**
```
100 200 300
1
```
**Output:**
```
100 200
```
**Explanation:** Remove 1st from end (value 300, the tail). List becomes 100→200.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        # start your solution
        dummy = ListNode(0)
        dummy.next = head
        
        fast = dummy
        slow = dummy
        
        # Move fast pointer n+1 steps ahead
        for _ in range(n + 1):
            fast = fast.next
        
        # Move both until fast reaches end
        while fast:
            fast = fast.next
            slow = slow.next
        
        # Remove the nth node
        slow.next = slow.next.next
        
        return dummy.next
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
    if not head:
        print("empty")
        return
    result = []
    while head:
        result.append(str(head.val))
        head = head.next
    print(' '.join(result))

def main():
    arr = list(map(int, input().split()))
    n = int(input())
    
    head = buildList(arr)
    
    sol = Solution()
    result = sol.removeNthFromEnd(head, n)
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        // start your solution
        ListNode dummy(0);
        dummy.next = head;
        
        ListNode* fast = &dummy;
        ListNode* slow = &dummy;
        
        // Move fast pointer n+1 steps ahead
        for (int i = 0; i <= n; i++) {
            fast = fast->next;
        }
        
        // Move both until fast reaches end
        while (fast) {
            fast = fast->next;
            slow = slow->next;
        }
        
        // Remove the nth node
        ListNode* toDelete = slow->next;
        slow->next = slow->next->next;
        delete toDelete;
        
        return dummy.next;
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
    if (!head) {
        cout << "empty" << endl;
        return;
    }
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
    
    int n;
    cin >> n;
    
    ListNode* head = buildList(arr);
    
    Solution sol;
    ListNode* result = sol.removeNthFromEnd(head, n);
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // start your solution
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode fast = dummy;
        ListNode slow = dummy;
        
        // Move fast pointer n+1 steps ahead
        for (int i = 0; i <= n; i++) {
            fast = fast.next;
        }
        
        // Move both until fast reaches end
        while (fast != null) {
            fast = fast.next;
            slow = slow.next;
        }
        
        // Remove the nth node
        slow.next = slow.next.next;
        
        return dummy.next;
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
        if (head == null) {
            System.out.println("empty");
            return;
        }
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
        
        int n = Integer.parseInt(sc.nextLine().trim());
        
        ListNode head = buildList(arr);
        
        Solution sol = new Solution();
        ListNode result = sol.removeNthFromEnd(head, n);
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
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
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
    if not head:
        print("empty")
        return
    result = []
    while head:
        result.append(str(head.val))
        head = head.next
    print(' '.join(result))

def main():
    arr = list(map(int, input().split()))
    n = int(input())
    
    head = buildList(arr)
    
    sol = Solution()
    result = sol.removeNthFromEnd(head, n)
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
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
    if (!head) {
        cout << "empty" << endl;
        return;
    }
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
    
    int n;
    cin >> n;
    
    ListNode* head = buildList(arr);
    
    Solution sol;
    ListNode* result = sol.removeNthFromEnd(head, n);
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
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
        if (head == null) {
            System.out.println("empty");
            return;
        }
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
        
        int n = Integer.parseInt(sc.nextLine().trim());
        
        ListNode head = buildList(arr);
        
        Solution sol = new Solution();
        ListNode result = sol.removeNthFromEnd(head, n);
        printList(result);
        
        sc.close();
    }
}
```
