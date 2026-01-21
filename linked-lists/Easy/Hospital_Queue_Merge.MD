# Hospital Queue Merge

### Problem Statement

At AIIMS Delhi, two OPD counters maintain separate patient queues sorted by appointment time (in minutes from opening). During lunch break, the staff needs to merge both queues into a single sorted queue for the afternoon session.

Given the heads of two sorted linked lists `queue1` and `queue2`, merge them into one sorted list and return the head of the merged list. The merged list should be made by splicing together the nodes of the input lists.

### Input Format

- The first line contains space-separated integers for queue1, or "empty" for an empty list.
- The second line contains space-separated integers for queue2, or "empty" for an empty list.

### Output Format

- Print the merged sorted list as space-separated integers, or "empty" if both lists are empty.

### Constraints

- `0 <= n, m <= 50` (lengths of both lists)
- `-100 <= Node.val <= 100`
- Both lists are sorted in non-decreasing order

### Test Cases

#### Test Case 1
**Input:**
```
1 2 4
1 3 4
```
**Output:**
```
1 1 2 3 4 4
```
**Explanation:** Compare heads: 1=1, take from queue1. Continue comparing and picking smaller element each time.

---

#### Test Case 2
**Input:**
```
empty
empty
```
**Output:**
```
empty
```
**Explanation:** Both queues empty. Result is empty.

---

#### Test Case 3
**Input:**
```
empty
0
```
**Output:**
```
0
```
**Explanation:** First queue empty. Result is just the second queue.

---

#### Test Case 4
**Input:**
```
5
empty
```
**Output:**
```
5
```
**Explanation:** Second queue empty. Result is just the first queue.

---

#### Test Case 5
**Input:**
```
1 3 5 7
2 4 6 8
```
**Output:**
```
1 2 3 4 5 6 7 8
```
**Explanation:** Alternating merge. Pick from each queue in order.

---

#### Test Case 6
**Input:**
```
1 2 3
4 5 6
```
**Output:**
```
1 2 3 4 5 6
```
**Explanation:** Non-overlapping ranges. First queue exhausted, then append second.

---

#### Test Case 7
**Input:**
```
10 20 30
10 20 30
```
**Output:**
```
10 10 20 20 30 30
```
**Explanation:** Identical queues. Alternate between them for equal values.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeTwoLists(self, queue1: ListNode, queue2: ListNode) -> ListNode:
        # start your solution
        dummy = ListNode(0)
        curr = dummy
        
        while queue1 and queue2:
            if queue1.val <= queue2.val:
                curr.next = queue1
                queue1 = queue1.next
            else:
                curr.next = queue2
                queue2 = queue2.next
            curr = curr.next
        
        curr.next = queue1 if queue1 else queue2
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
    line1 = input().strip()
    line2 = input().strip()
    
    queue1 = None if line1 == "empty" else buildList(list(map(int, line1.split())))
    queue2 = None if line2 == "empty" else buildList(list(map(int, line2.split())))
    
    sol = Solution()
    result = sol.mergeTwoLists(queue1, queue2)
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
    ListNode* mergeTwoLists(ListNode* queue1, ListNode* queue2) {
        // start your solution
        ListNode dummy(0);
        ListNode* curr = &dummy;
        
        while (queue1 && queue2) {
            if (queue1->val <= queue2->val) {
                curr->next = queue1;
                queue1 = queue1->next;
            } else {
                curr->next = queue2;
                queue2 = queue2->next;
            }
            curr = curr->next;
        }
        
        curr->next = queue1 ? queue1 : queue2;
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
    
    string line1, line2;
    getline(cin, line1);
    getline(cin, line2);
    
    ListNode* queue1 = nullptr;
    ListNode* queue2 = nullptr;
    
    if (line1 != "empty") {
        vector<int> arr;
        stringstream ss(line1);
        int num;
        while (ss >> num) arr.push_back(num);
        queue1 = buildList(arr);
    }
    
    if (line2 != "empty") {
        vector<int> arr;
        stringstream ss(line2);
        int num;
        while (ss >> num) arr.push_back(num);
        queue2 = buildList(arr);
    }
    
    Solution sol;
    ListNode* result = sol.mergeTwoLists(queue1, queue2);
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
    public ListNode mergeTwoLists(ListNode queue1, ListNode queue2) {
        // start your solution
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        
        while (queue1 != null && queue2 != null) {
            if (queue1.val <= queue2.val) {
                curr.next = queue1;
                queue1 = queue1.next;
            } else {
                curr.next = queue2;
                queue2 = queue2.next;
            }
            curr = curr.next;
        }
        
        curr.next = (queue1 != null) ? queue1 : queue2;
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
        
        String line1 = sc.nextLine().trim();
        String line2 = sc.nextLine().trim();
        
        ListNode queue1 = null;
        ListNode queue2 = null;
        
        if (!line1.equals("empty")) {
            String[] parts = line1.split(" ");
            int[] arr = new int[parts.length];
            for (int i = 0; i < parts.length; i++) {
                arr[i] = Integer.parseInt(parts[i]);
            }
            queue1 = buildList(arr);
        }
        
        if (!line2.equals("empty")) {
            String[] parts = line2.split(" ");
            int[] arr = new int[parts.length];
            for (int i = 0; i < parts.length; i++) {
                arr[i] = Integer.parseInt(parts[i]);
            }
            queue2 = buildList(arr);
        }
        
        Solution sol = new Solution();
        ListNode result = sol.mergeTwoLists(queue1, queue2);
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
    def mergeTwoLists(self, queue1: ListNode, queue2: ListNode) -> ListNode:
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
    line1 = input().strip()
    line2 = input().strip()
    
    queue1 = None if line1 == "empty" else buildList(list(map(int, line1.split())))
    queue2 = None if line2 == "empty" else buildList(list(map(int, line2.split())))
    
    sol = Solution()
    result = sol.mergeTwoLists(queue1, queue2)
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
    ListNode* mergeTwoLists(ListNode* queue1, ListNode* queue2) {
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
    
    string line1, line2;
    getline(cin, line1);
    getline(cin, line2);
    
    ListNode* queue1 = nullptr;
    ListNode* queue2 = nullptr;
    
    if (line1 != "empty") {
        vector<int> arr;
        stringstream ss(line1);
        int num;
        while (ss >> num) arr.push_back(num);
        queue1 = buildList(arr);
    }
    
    if (line2 != "empty") {
        vector<int> arr;
        stringstream ss(line2);
        int num;
        while (ss >> num) arr.push_back(num);
        queue2 = buildList(arr);
    }
    
    Solution sol;
    ListNode* result = sol.mergeTwoLists(queue1, queue2);
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
    public ListNode mergeTwoLists(ListNode queue1, ListNode queue2) {
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
        
        String line1 = sc.nextLine().trim();
        String line2 = sc.nextLine().trim();
        
        ListNode queue1 = null;
        ListNode queue2 = null;
        
        if (!line1.equals("empty")) {
            String[] parts = line1.split(" ");
            int[] arr = new int[parts.length];
            for (int i = 0; i < parts.length; i++) {
                arr[i] = Integer.parseInt(parts[i]);
            }
            queue1 = buildList(arr);
        }
        
        if (!line2.equals("empty")) {
            String[] parts = line2.split(" ");
            int[] arr = new int[parts.length];
            for (int i = 0; i < parts.length; i++) {
                arr[i] = Integer.parseInt(parts[i]);
            }
            queue2 = buildList(arr);
        }
        
        Solution sol = new Solution();
        ListNode result = sol.mergeTwoLists(queue1, queue2);
        printList(result);
        
        sc.close();
    }
}
```
