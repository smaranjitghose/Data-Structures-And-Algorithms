# Cinema Seat Rearrangement

### Problem Statement

At PVR Cinemas in Mumbai, the manager wants to rearrange the seat booking list for better social distancing. All odd-positioned bookings should come before even-positioned bookings while maintaining their relative order.

Given the head of a singly linked list, group all nodes at odd indices together followed by nodes at even indices, and return the reordered list.

Note: The first node is considered odd (index 1), the second node is even (index 2), and so on.

### Input Format

- A single line containing space-separated integers representing booking IDs, or "empty" for an empty list.

### Output Format

- Print the rearranged list as space-separated integers, or "empty" if the list is empty.

### Constraints

- `0 <= n <= 10^4` (number of bookings)
- `-10^6 <= Node.val <= 10^6`

### Test Cases

#### Test Case 1
**Input:**
```
1 2 3 4 5
```
**Output:**
```
1 3 5 2 4
```
**Explanation:** Odd positions: 1(idx1), 3(idx3), 5(idx5). Even positions: 2(idx2), 4(idx4). Result: 1→3→5→2→4.

---

#### Test Case 2
**Input:**
```
2 1 3 5 6 4 7
```
**Output:**
```
2 3 6 7 1 5 4
```
**Explanation:** Odd indices: 2,3,6,7. Even indices: 1,5,4. Concatenate odd list with even list.

---

#### Test Case 3
**Input:**
```
1
```
**Output:**
```
1
```
**Explanation:** Single node, no rearrangement needed.

---

#### Test Case 4
**Input:**
```
1 2
```
**Output:**
```
1 2
```
**Explanation:** First is odd, second is even. Already in correct order.

---

#### Test Case 5
**Input:**
```
empty
```
**Output:**
```
empty
```
**Explanation:** Empty list remains empty.

---

#### Test Case 6
**Input:**
```
10 20 30 40 50 60
```
**Output:**
```
10 30 50 20 40 60
```
**Explanation:** Odd positions: 10,30,50. Even positions: 20,40,60. Result: 10→30→50→20→40→60.

---

#### Test Case 7
**Input:**
```
5 4 3 2 1
```
**Output:**
```
5 3 1 4 2
```
**Explanation:** Odd positions: 5,3,1. Even positions: 4,2. Result: 5→3→1→4→2.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        # start your solution
        if not head or not head.next:
            return head
        
        odd = head
        even = head.next
        evenHead = even
        
        while even and even.next:
            odd.next = even.next
            odd = odd.next
            even.next = odd.next
            even = even.next
        
        odd.next = evenHead
        return head
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
    result = sol.oddEvenList(head)
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
    ListNode* oddEvenList(ListNode* head) {
        // start your solution
        if (!head || !head->next) return head;
        
        ListNode* odd = head;
        ListNode* even = head->next;
        ListNode* evenHead = even;
        
        while (even && even->next) {
            odd->next = even->next;
            odd = odd->next;
            even->next = odd->next;
            even = even->next;
        }
        
        odd->next = evenHead;
        return head;
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
        while (ss >> num) arr.push_back(num);
        head = buildList(arr);
    }
    
    Solution sol;
    ListNode* result = sol.oddEvenList(head);
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
    public ListNode oddEvenList(ListNode head) {
        // start your solution
        if (head == null || head.next == null) return head;
        
        ListNode odd = head;
        ListNode even = head.next;
        ListNode evenHead = even;
        
        while (even != null && even.next != null) {
            odd.next = even.next;
            odd = odd.next;
            even.next = odd.next;
            even = even.next;
        }
        
        odd.next = evenHead;
        return head;
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
        ListNode result = sol.oddEvenList(head);
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
    def oddEvenList(self, head: ListNode) -> ListNode:
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
    result = sol.oddEvenList(head)
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
    ListNode* oddEvenList(ListNode* head) {
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
        while (ss >> num) arr.push_back(num);
        head = buildList(arr);
    }
    
    Solution sol;
    ListNode* result = sol.oddEvenList(head);
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
    public ListNode oddEvenList(ListNode head) {
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
        ListNode result = sol.oddEvenList(head);
        printList(result);
        
        sc.close();
    }
}
```
