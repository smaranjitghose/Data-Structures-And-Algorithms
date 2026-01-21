# Train Coach Rearrangement

### Problem Statement

At the New Delhi Railway Station, the Rajdhani Express needs coach rearrangement before departure. The station master must reverse coaches in groups of `k` for maintenance inspection. If the remaining coaches are fewer than `k`, they stay in their original order.

Given the head of a linked list representing coach numbers, reverse the nodes in groups of `k` and return the modified list. Only the nodes themselves may be changed, not their values.

### Input Format

- The first line contains space-separated integers representing coach numbers.
- The second line contains an integer `k`, the group size.

### Output Format

- Print the rearranged coach numbers as space-separated integers.

### Constraints

- `1 <= n <= 5000` (number of coaches)
- `1 <= k <= n`
- `0 <= Node.val <= 1000`

### Test Cases

#### Test Case 1
**Input:**
```
1 2 3 4 5
2
```
**Output:**
```
2 1 4 3 5
```
**Explanation:** Reverse in groups of 2. [1,2] becomes [2,1], [3,4] becomes [4,3], [5] remains as is (less than k).

---

#### Test Case 2
**Input:**
```
1 2 3 4 5
3
```
**Output:**
```
3 2 1 4 5
```
**Explanation:** Reverse in groups of 3. [1,2,3] becomes [3,2,1], [4,5] stays same (only 2 nodes, less than k=3).

---

#### Test Case 3
**Input:**
```
1 2 3 4
2
```
**Output:**
```
2 1 4 3
```
**Explanation:** Exactly 2 groups of 2. Both reversed completely.

---

#### Test Case 4
**Input:**
```
1
1
```
**Output:**
```
1
```
**Explanation:** Single coach, k=1. No change needed.

---

#### Test Case 5
**Input:**
```
1 2 3 4 5 6
3
```
**Output:**
```
3 2 1 6 5 4
```
**Explanation:** Two complete groups of 3. [1,2,3]→[3,2,1], [4,5,6]→[6,5,4].

---

#### Test Case 6
**Input:**
```
1 2 3 4 5 6 7
4
```
**Output:**
```
4 3 2 1 5 6 7
```
**Explanation:** First 4 coaches reversed. Remaining 3 coaches (less than k=4) stay in order.

---

#### Test Case 7
**Input:**
```
10 20 30 40 50 60 70 80
2
```
**Output:**
```
20 10 40 30 60 50 80 70
```
**Explanation:** Four groups of 2, all reversed. [10,20]→[20,10], [30,40]→[40,30], etc.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        # start your solution
        # Count total nodes
        count = 0
        curr = head
        while curr:
            count += 1
            curr = curr.next
        
        dummy = ListNode(0)
        dummy.next = head
        prevGroupEnd = dummy
        
        while count >= k:
            # Reverse k nodes
            prev = None
            curr = prevGroupEnd.next
            groupStart = curr
            
            for _ in range(k):
                nextNode = curr.next
                curr.next = prev
                prev = curr
                curr = nextNode
            
            # Connect with previous group
            prevGroupEnd.next = prev
            groupStart.next = curr
            prevGroupEnd = groupStart
            
            count -= k
        
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
    result = []
    while head:
        result.append(str(head.val))
        head = head.next
    print(' '.join(result))

def main():
    arr = list(map(int, input().split()))
    k = int(input())
    
    head = buildList(arr)
    
    sol = Solution()
    result = sol.reverseKGroup(head, k)
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
    ListNode* reverseKGroup(ListNode* head, int k) {
        // start your solution
        // Count total nodes
        int count = 0;
        ListNode* curr = head;
        while (curr) {
            count++;
            curr = curr->next;
        }
        
        ListNode dummy(0);
        dummy.next = head;
        ListNode* prevGroupEnd = &dummy;
        
        while (count >= k) {
            // Reverse k nodes
            ListNode* prev = nullptr;
            curr = prevGroupEnd->next;
            ListNode* groupStart = curr;
            
            for (int i = 0; i < k; i++) {
                ListNode* nextNode = curr->next;
                curr->next = prev;
                prev = curr;
                curr = nextNode;
            }
            
            // Connect with previous group
            prevGroupEnd->next = prev;
            groupStart->next = curr;
            prevGroupEnd = groupStart;
            
            count -= k;
        }
        
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
    while (ss >> num) {
        arr.push_back(num);
    }
    
    int k;
    cin >> k;
    
    ListNode* head = buildList(arr);
    
    Solution sol;
    ListNode* result = sol.reverseKGroup(head, k);
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
    public ListNode reverseKGroup(ListNode head, int k) {
        // start your solution
        // Count total nodes
        int count = 0;
        ListNode curr = head;
        while (curr != null) {
            count++;
            curr = curr.next;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prevGroupEnd = dummy;
        
        while (count >= k) {
            // Reverse k nodes
            ListNode prev = null;
            curr = prevGroupEnd.next;
            ListNode groupStart = curr;
            
            for (int i = 0; i < k; i++) {
                ListNode nextNode = curr.next;
                curr.next = prev;
                prev = curr;
                curr = nextNode;
            }
            
            // Connect with previous group
            prevGroupEnd.next = prev;
            groupStart.next = curr;
            prevGroupEnd = groupStart;
            
            count -= k;
        }
        
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
        
        int k = Integer.parseInt(sc.nextLine().trim());
        
        ListNode head = buildList(arr);
        
        Solution sol = new Solution();
        ListNode result = sol.reverseKGroup(head, k);
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
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
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
    k = int(input())
    
    head = buildList(arr)
    
    sol = Solution()
    result = sol.reverseKGroup(head, k)
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
    ListNode* reverseKGroup(ListNode* head, int k) {
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
    while (ss >> num) {
        arr.push_back(num);
    }
    
    int k;
    cin >> k;
    
    ListNode* head = buildList(arr);
    
    Solution sol;
    ListNode* result = sol.reverseKGroup(head, k);
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
    public ListNode reverseKGroup(ListNode head, int k) {
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
        
        int k = Integer.parseInt(sc.nextLine().trim());
        
        ListNode head = buildList(arr);
        
        Solution sol = new Solution();
        ListNode result = sol.reverseKGroup(head, k);
        printList(result);
        
        sc.close();
    }
}
```
