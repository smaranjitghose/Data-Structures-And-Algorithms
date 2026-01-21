# Warehouse Inventory Merge

### Problem Statement

Flipkart operates multiple warehouses across India. Each warehouse maintains its inventory as a sorted linked list of product IDs. During the Big Billion Days sale, the central system in Bengaluru needs to merge all warehouse inventories into a single sorted list for unified stock management.

Given an array of `k` linked lists, where each linked list is sorted in ascending order, merge all lists into one sorted linked list and return it.

### Input Format

- The first line contains an integer `k`, the number of warehouses.
- The next `k` lines each contain space-separated integers representing sorted product IDs for that warehouse. Use -1 to indicate an empty list.

### Output Format

- Print the merged sorted linked list as space-separated integers, or "empty" if result is empty.

### Constraints

- `k == lists.length`
- `0 <= k <= 10^4`
- `0 <= lists[i].length <= 500`
- `-10^4 <= lists[i][j] <= 10^4`
- `lists[i]` is sorted in ascending order
- Sum of all `lists[i].length` <= 10^4

### Test Cases

#### Test Case 1
**Input:**
```
3
1 4 5
1 3 4
2 6
```
**Output:**
```
1 1 2 3 4 4 5 6
```
**Explanation:** Merge three sorted lists: [1,4,5], [1,3,4], [2,6]. Compare heads, pick smallest, advance pointer. Result: [1,1,2,3,4,4,5,6].

---

#### Test Case 2
**Input:**
```
1
-1
```
**Output:**
```
empty
```
**Explanation:** Single empty warehouse list. Result is empty.

---

#### Test Case 3
**Input:**
```
0
```
**Output:**
```
empty
```
**Explanation:** No warehouses. Result is empty.

---

#### Test Case 4
**Input:**
```
2
1 2 3
4 5 6
```
**Output:**
```
1 2 3 4 5 6
```
**Explanation:** Non-overlapping ranges. First list exhausted, then second appended.

---

#### Test Case 5
**Input:**
```
3
1
2
3
```
**Output:**
```
1 2 3
```
**Explanation:** Single element lists. Merge in order.

---

#### Test Case 6
**Input:**
```
4
1 5 9
2 6 10
3 7 11
4 8 12
```
**Output:**
```
1 2 3 4 5 6 7 8 9 10 11 12
```
**Explanation:** Four interleaved lists merge into sequential order.

---

#### Test Case 7
**Input:**
```
2
-5 -3 -1
-4 -2 0
```
**Output:**
```
-5 -4 -3 -2 -1 0
```
**Explanation:** Negative product IDs (returns/credits). Merge maintains sorted order.

---

### Solutions

#### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeKLists(self, lists: list) -> ListNode:
        # start your solution
        if not lists:
            return None
        
        while len(lists) > 1:
            merged = []
            for i in range(0, len(lists), 2):
                l1 = lists[i]
                l2 = lists[i + 1] if i + 1 < len(lists) else None
                merged.append(self.mergeTwoLists(l1, l2))
            lists = merged
        
        return lists[0]
    
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode(0)
        curr = dummy
        
        while l1 and l2:
            if l1.val <= l2.val:
                curr.next = l1
                l1 = l1.next
            else:
                curr.next = l2
                l2 = l2.next
            curr = curr.next
        
        curr.next = l1 if l1 else l2
        return dummy.next
        # end your solution


def buildList(arr):
    if not arr or arr[0] == -1:
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
    k = int(input())
    lists = []
    for _ in range(k):
        line = input().strip()
        if line:
            arr = list(map(int, line.split()))
            lists.append(buildList(arr))
        else:
            lists.append(None)
    
    sol = Solution()
    result = sol.mergeKLists(lists)
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        // start your solution
        if (lists.empty()) return nullptr;
        
        while (lists.size() > 1) {
            vector<ListNode*> merged;
            for (int i = 0; i < lists.size(); i += 2) {
                ListNode* l1 = lists[i];
                ListNode* l2 = (i + 1 < lists.size()) ? lists[i + 1] : nullptr;
                merged.push_back(mergeTwoLists(l1, l2));
            }
            lists = merged;
        }
        
        return lists[0];
        // end your solution
    }
    
private:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode dummy(0);
        ListNode* curr = &dummy;
        
        while (l1 && l2) {
            if (l1->val <= l2->val) {
                curr->next = l1;
                l1 = l1->next;
            } else {
                curr->next = l2;
                l2 = l2->next;
            }
            curr = curr->next;
        }
        
        curr->next = l1 ? l1 : l2;
        return dummy.next;
    }
};

ListNode* buildList(vector<int>& arr) {
    if (arr.empty() || arr[0] == -1) return nullptr;
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
    
    int k;
    cin >> k;
    cin.ignore();
    
    vector<ListNode*> lists;
    for (int i = 0; i < k; i++) {
        string line;
        getline(cin, line);
        vector<int> arr;
        stringstream ss(line);
        int num;
        while (ss >> num) {
            arr.push_back(num);
        }
        lists.push_back(buildList(arr));
    }
    
    Solution sol;
    ListNode* result = sol.mergeKLists(lists);
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
    public ListNode mergeKLists(ListNode[] lists) {
        // start your solution
        if (lists == null || lists.length == 0) return null;
        
        List<ListNode> listArray = new ArrayList<>(Arrays.asList(lists));
        
        while (listArray.size() > 1) {
            List<ListNode> merged = new ArrayList<>();
            for (int i = 0; i < listArray.size(); i += 2) {
                ListNode l1 = listArray.get(i);
                ListNode l2 = (i + 1 < listArray.size()) ? listArray.get(i + 1) : null;
                merged.add(mergeTwoLists(l1, l2));
            }
            listArray = merged;
        }
        
        return listArray.get(0);
        // end your solution
    }
    
    private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                curr.next = l1;
                l1 = l1.next;
            } else {
                curr.next = l2;
                l2 = l2.next;
            }
            curr = curr.next;
        }
        
        curr.next = (l1 != null) ? l1 : l2;
        return dummy.next;
    }
}

public class Main {
    public static ListNode buildList(int[] arr) {
        if (arr.length == 0 || arr[0] == -1) return null;
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
        
        int k = Integer.parseInt(sc.nextLine().trim());
        ListNode[] lists = new ListNode[k];
        
        for (int i = 0; i < k; i++) {
            String line = sc.nextLine().trim();
            if (line.isEmpty()) {
                lists[i] = null;
            } else {
                String[] parts = line.split(" ");
                int[] arr = new int[parts.length];
                for (int j = 0; j < parts.length; j++) {
                    arr[j] = Integer.parseInt(parts[j]);
                }
                lists[i] = buildList(arr);
            }
        }
        
        Solution sol = new Solution();
        ListNode result = sol.mergeKLists(lists);
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
    def mergeKLists(self, lists: list) -> ListNode:
        # start your solution
        
        
        
        # end your solution


def buildList(arr):
    if not arr or arr[0] == -1:
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
    k = int(input())
    lists = []
    for _ in range(k):
        line = input().strip()
        if line:
            arr = list(map(int, line.split()))
            lists.append(buildList(arr))
        else:
            lists.append(None)
    
    sol = Solution()
    result = sol.mergeKLists(lists)
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        // start your solution
        
        
        
        // end your solution
    }
};

ListNode* buildList(vector<int>& arr) {
    if (arr.empty() || arr[0] == -1) return nullptr;
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
    
    int k;
    cin >> k;
    cin.ignore();
    
    vector<ListNode*> lists;
    for (int i = 0; i < k; i++) {
        string line;
        getline(cin, line);
        vector<int> arr;
        stringstream ss(line);
        int num;
        while (ss >> num) {
            arr.push_back(num);
        }
        lists.push_back(buildList(arr));
    }
    
    Solution sol;
    ListNode* result = sol.mergeKLists(lists);
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
    public ListNode mergeKLists(ListNode[] lists) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static ListNode buildList(int[] arr) {
        if (arr.length == 0 || arr[0] == -1) return null;
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
        
        int k = Integer.parseInt(sc.nextLine().trim());
        ListNode[] lists = new ListNode[k];
        
        for (int i = 0; i < k; i++) {
            String line = sc.nextLine().trim();
            if (line.isEmpty()) {
                lists[i] = null;
            } else {
                String[] parts = line.split(" ");
                int[] arr = new int[parts.length];
                for (int j = 0; j < parts.length; j++) {
                    arr[j] = Integer.parseInt(parts[j]);
                }
                lists[i] = buildList(arr);
            }
        }
        
        Solution sol = new Solution();
        ListNode result = sol.mergeKLists(lists);
        printList(result);
        
        sc.close();
    }
}
```
