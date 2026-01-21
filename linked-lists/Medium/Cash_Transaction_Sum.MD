# Cash Transaction Sum

### Problem Statement

Two money exchange agents in Chandni Chowk, Delhi are calculating the total of two large cash amounts. Each amount is represented as a linked list where digits are stored in reverse order (least significant digit first).

Given two non-empty linked lists `amount1` and `amount2` representing two non-negative integers, add the two numbers and return the sum as a linked list in the same reverse-digit format.

### Input Format

- The first line contains space-separated digits of the first amount (reverse order).
- The second line contains space-separated digits of the second amount (reverse order).

### Output Format

- Print the sum as space-separated digits (reverse order).

### Constraints

- `1 <= length of each list <= 100`
- `0 <= Node.val <= 9`
- Numbers do not contain leading zeros except the number 0 itself

### Test Cases

#### Test Case 1
**Input:**
```
2 4 3
5 6 4
```
**Output:**
```
7 0 8
```
**Explanation:** 342 + 465 = 807. Reverse: 2→4→3 represents 342, 5→6→4 represents 465. Sum 807 as 7→0→8.

---

#### Test Case 2
**Input:**
```
0
0
```
**Output:**
```
0
```
**Explanation:** 0 + 0 = 0.

---

#### Test Case 3
**Input:**
```
9 9 9 9 9 9 9
9 9 9 9
```
**Output:**
```
8 9 9 9 0 0 0 1
```
**Explanation:** 9999999 + 9999 = 10009998. Result in reverse: 8→9→9→9→0→0→0→1.

---

#### Test Case 4
**Input:**
```
1
9 9 9
```
**Output:**
```
0 0 0 1
```
**Explanation:** 1 + 999 = 1000. Reverse representation: 0→0→0→1.

---

#### Test Case 5
**Input:**
```
5
5
```
**Output:**
```
0 1
```
**Explanation:** 5 + 5 = 10. Reverse: 0→1.

---

#### Test Case 6
**Input:**
```
1 2 3 4 5
6 7 8
```
**Output:**
```
7 9 1 5 5
```
**Explanation:** 54321 + 876 = 55197. Reverse: 7→9→1→5→5.

---

#### Test Case 7
**Input:**
```
9
1
```
**Output:**
```
0 1
```
**Explanation:** 9 + 1 = 10. Carry propagates. Result: 0→1.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def addTwoNumbers(self, amount1: ListNode, amount2: ListNode) -> ListNode:
        # start your solution
        dummy = ListNode(0)
        curr = dummy
        carry = 0
        
        while amount1 or amount2 or carry:
            val1 = amount1.val if amount1 else 0
            val2 = amount2.val if amount2 else 0
            
            total = val1 + val2 + carry
            carry = total // 10
            curr.next = ListNode(total % 10)
            curr = curr.next
            
            if amount1:
                amount1 = amount1.next
            if amount2:
                amount2 = amount2.next
        
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
    arr1 = list(map(int, input().split()))
    arr2 = list(map(int, input().split()))
    
    amount1 = buildList(arr1)
    amount2 = buildList(arr2)
    
    sol = Solution()
    result = sol.addTwoNumbers(amount1, amount2)
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
    ListNode* addTwoNumbers(ListNode* amount1, ListNode* amount2) {
        // start your solution
        ListNode dummy(0);
        ListNode* curr = &dummy;
        int carry = 0;
        
        while (amount1 || amount2 || carry) {
            int val1 = amount1 ? amount1->val : 0;
            int val2 = amount2 ? amount2->val : 0;
            
            int total = val1 + val2 + carry;
            carry = total / 10;
            curr->next = new ListNode(total % 10);
            curr = curr->next;
            
            if (amount1) amount1 = amount1->next;
            if (amount2) amount2 = amount2->next;
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
    
    string line1, line2;
    getline(cin, line1);
    getline(cin, line2);
    
    vector<int> arr1, arr2;
    stringstream ss1(line1), ss2(line2);
    int num;
    while (ss1 >> num) arr1.push_back(num);
    while (ss2 >> num) arr2.push_back(num);
    
    ListNode* amount1 = buildList(arr1);
    ListNode* amount2 = buildList(arr2);
    
    Solution sol;
    ListNode* result = sol.addTwoNumbers(amount1, amount2);
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
    public ListNode addTwoNumbers(ListNode amount1, ListNode amount2) {
        // start your solution
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        int carry = 0;
        
        while (amount1 != null || amount2 != null || carry != 0) {
            int val1 = (amount1 != null) ? amount1.val : 0;
            int val2 = (amount2 != null) ? amount2.val : 0;
            
            int total = val1 + val2 + carry;
            carry = total / 10;
            curr.next = new ListNode(total % 10);
            curr = curr.next;
            
            if (amount1 != null) amount1 = amount1.next;
            if (amount2 != null) amount2 = amount2.next;
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
        
        String[] parts1 = sc.nextLine().split(" ");
        String[] parts2 = sc.nextLine().split(" ");
        
        int[] arr1 = new int[parts1.length];
        int[] arr2 = new int[parts2.length];
        
        for (int i = 0; i < parts1.length; i++) arr1[i] = Integer.parseInt(parts1[i]);
        for (int i = 0; i < parts2.length; i++) arr2[i] = Integer.parseInt(parts2[i]);
        
        ListNode amount1 = buildList(arr1);
        ListNode amount2 = buildList(arr2);
        
        Solution sol = new Solution();
        ListNode result = sol.addTwoNumbers(amount1, amount2);
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
    def addTwoNumbers(self, amount1: ListNode, amount2: ListNode) -> ListNode:
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
    arr1 = list(map(int, input().split()))
    arr2 = list(map(int, input().split()))
    
    amount1 = buildList(arr1)
    amount2 = buildList(arr2)
    
    sol = Solution()
    result = sol.addTwoNumbers(amount1, amount2)
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
    ListNode* addTwoNumbers(ListNode* amount1, ListNode* amount2) {
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
    
    string line1, line2;
    getline(cin, line1);
    getline(cin, line2);
    
    vector<int> arr1, arr2;
    stringstream ss1(line1), ss2(line2);
    int num;
    while (ss1 >> num) arr1.push_back(num);
    while (ss2 >> num) arr2.push_back(num);
    
    ListNode* amount1 = buildList(arr1);
    ListNode* amount2 = buildList(arr2);
    
    Solution sol;
    ListNode* result = sol.addTwoNumbers(amount1, amount2);
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
    public ListNode addTwoNumbers(ListNode amount1, ListNode amount2) {
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
        
        String[] parts1 = sc.nextLine().split(" ");
        String[] parts2 = sc.nextLine().split(" ");
        
        int[] arr1 = new int[parts1.length];
        int[] arr2 = new int[parts2.length];
        
        for (int i = 0; i < parts1.length; i++) arr1[i] = Integer.parseInt(parts1[i]);
        for (int i = 0; i < parts2.length; i++) arr2[i] = Integer.parseInt(parts2[i]);
        
        ListNode amount1 = buildList(arr1);
        ListNode amount2 = buildList(arr2);
        
        Solution sol = new Solution();
        ListNode result = sol.addTwoNumbers(amount1, amount2);
        printList(result);
        
        sc.close();
    }
}
```
