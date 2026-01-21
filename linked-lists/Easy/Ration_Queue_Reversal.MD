# Ration Queue Reversal

### Problem Statement

At a Fair Price Shop in Kolkata, the queue for ration distribution got recorded in the wrong order. The shop manager needs to reverse the queue list so that the first person who arrived is served first.

Given the head of a singly linked list representing people's token numbers in the queue, reverse the list and return the new head.

### Input Format

- A single line containing space-separated integers representing token numbers, or "empty" for an empty list.

### Output Format

- Print the reversed list as space-separated integers, or "empty" if the list is empty.

### Constraints

- `0 <= n <= 5000` (number of people)
- `-5000 <= Node.val <= 5000`

### Test Cases

#### Test Case 1
**Input:**
```
1 2 3 4 5
```
**Output:**
```
5 4 3 2 1
```
**Explanation:** Reverse pointers: 5→4→3→2→1. Original first (1) becomes last, original last (5) becomes first.

---

#### Test Case 2
**Input:**
```
1 2
```
**Output:**
```
2 1
```
**Explanation:** Two nodes. Simply swap their order.

---

#### Test Case 3
**Input:**
```
empty
```
**Output:**
```
empty
```
**Explanation:** Empty queue remains empty.

---

#### Test Case 4
**Input:**
```
100
```
**Output:**
```
100
```
**Explanation:** Single person queue. Reversal gives same result.

---

#### Test Case 5
**Input:**
```
10 20 30 40 50 60
```
**Output:**
```
60 50 40 30 20 10
```
**Explanation:** Six tokens reversed. Each node's next pointer redirected to previous node.

---

#### Test Case 6
**Input:**
```
-5 0 5 10
```
**Output:**
```
10 5 0 -5
```
**Explanation:** Works with negative values. Order completely reversed.

---

#### Test Case 7
**Input:**
```
1 1 1 1
```
**Output:**
```
1 1 1 1
```
**Explanation:** Duplicate values. Structure reversed even though values look same.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # start your solution
        prev = None
        curr = head
        
        while curr:
            nextNode = curr.next
            curr.next = prev
            prev = curr
            curr = nextNode
        
        return prev
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
    line = input().strip()
    if line == "empty":
        head = None
    else:
        arr = list(map(int, line.split()))
        head = buildList(arr)
    
    sol = Solution()
    result = sol.reverseList(head)
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
    ListNode* reverseList(ListNode* head) {
        // start your solution
        ListNode* prev = nullptr;
        ListNode* curr = head;
        
        while (curr) {
            ListNode* nextNode = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextNode;
        }
        
        return prev;
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
    
    ListNode* head = nullptr;
    if (line != "empty") {
        vector<int> arr;
        stringstream ss(line);
        int num;
        while (ss >> num) {
            arr.push_back(num);
        }
        head = buildList(arr);
    }
    
    Solution sol;
    ListNode* result = sol.reverseList(head);
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
    public ListNode reverseList(ListNode head) {
        // start your solution
        ListNode prev = null;
        ListNode curr = head;
        
        while (curr != null) {
            ListNode nextNode = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextNode;
        }
        
        return prev;
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
        
        String line = sc.nextLine().trim();
        ListNode head = null;
        
        if (!line.equals("empty")) {
            String[] parts = line.split(" ");
            int[] arr = new int[parts.length];
            for (int i = 0; i < parts.length; i++) {
                arr[i] = Integer.parseInt(parts[i]);
            }
            head = buildList(arr);
        }
        
        Solution sol = new Solution();
        ListNode result = sol.reverseList(head);
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
    def reverseList(self, head: ListNode) -> ListNode:
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
    line = input().strip()
    if line == "empty":
        head = None
    else:
        arr = list(map(int, line.split()))
        head = buildList(arr)
    
    sol = Solution()
    result = sol.reverseList(head)
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
    ListNode* reverseList(ListNode* head) {
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
    
    ListNode* head = nullptr;
    if (line != "empty") {
        vector<int> arr;
        stringstream ss(line);
        int num;
        while (ss >> num) {
            arr.push_back(num);
        }
        head = buildList(arr);
    }
    
    Solution sol;
    ListNode* result = sol.reverseList(head);
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
    public ListNode reverseList(ListNode head) {
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
        
        String line = sc.nextLine().trim();
        ListNode head = null;
        
        if (!line.equals("empty")) {
            String[] parts = line.split(" ");
            int[] arr = new int[parts.length];
            for (int i = 0; i < parts.length; i++) {
                arr[i] = Integer.parseInt(parts[i]);
            }
            head = buildList(arr);
        }
        
        Solution sol = new Solution();
        ListNode result = sol.reverseList(head);
        printList(result);
        
        sc.close();
    }
}
```
