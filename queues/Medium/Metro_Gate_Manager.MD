# Metro Gate Manager

### Problem Statement

At Rajiv Chowk Metro Station in Delhi, the busiest interchange station, gates need to manage passenger flow efficiently. The system uses a circular double-ended queue to track passengers entering from both front and rear gates.

Design a circular deque with fixed capacity that supports insertions and deletions at both ends.

Operations:
- `MyCircularDeque(k)` - Initialize deque with capacity k
- `insertFront(value)` - Add at front, return true if successful
- `insertLast(value)` - Add at rear, return true if successful
- `deleteFront()` - Delete from front, return true if successful
- `deleteLast()` - Delete from rear, return true if successful
- `getFront()` - Get front element, return -1 if empty
- `getRear()` - Get rear element, return -1 if empty
- `isEmpty()` - Check if deque is empty
- `isFull()` - Check if deque is full

### Input Format

- The first line contains the capacity `k`.
- The second line contains the number of operations `n`.
- The next `n` lines each contain an operation.

### Output Format

- For operations returning boolean, print `true` or `false`.
- For `getFront` and `getRear`, print the value or -1.

### Constraints

- `1 <= k <= 1000`
- `0 <= value <= 1000`
- At most 2000 operations

### Test Cases

#### Test Case 1
**Input:**
```
3
8
insertLast 1
insertLast 2
insertFront 3
insertFront 4
getRear
isFull
deleteLast
insertFront 4
getFront
```
**Output:**
```
true
true
true
false
2
true
true
true
4
```
**Explanation:** Capacity 3. Add 1,2 at rear, add 3 at front: [3,1,2]. Add 4 at front fails (full). Rear=2. Delete rear. Add 4 at front: [4,3,1]. Front=4.

---

#### Test Case 2
**Input:**
```
4
6
insertFront 10
insertLast 20
getFront
getRear
deleteFront
getFront
```
**Output:**
```
true
true
10
20
true
20
```
**Explanation:** [10] then [10,20]. Front=10, Rear=20. Delete front, Front now 20.

---

#### Test Case 3
**Input:**
```
2
5
insertFront 1
insertLast 2
isFull
deleteLast
insertFront 3
```
**Output:**
```
true
true
true
true
true
```
**Explanation:** [1,2] full. Delete last. Insert 3 at front: [3,1].

---

#### Test Case 4
**Input:**
```
3
4
isEmpty
getFront
getRear
deleteFront
```
**Output:**
```
true
-1
-1
false
```
**Explanation:** Empty deque operations.

---

#### Test Case 5
**Input:**
```
1
4
insertFront 5
isFull
deleteFront
isEmpty
```
**Output:**
```
true
true
true
true
```
**Explanation:** Capacity 1 deque operations.

---

#### Test Case 6
**Input:**
```
4
8
insertLast 1
insertLast 2
insertFront 0
getFront
getRear
deleteFront
deleteLast
getFront
```
**Output:**
```
true
true
true
0
2
true
true
1
```
**Explanation:** [0,1,2]. Front=0, Rear=2. After deletes: [1]. Front=1.

---

#### Test Case 7
**Input:**
```
3
6
insertLast 10
insertLast 20
insertLast 30
deleteFront
insertLast 40
getRear
```
**Output:**
```
true
true
true
true
true
40
```
**Explanation:** Circular wrap-around. After operations: [20,30,40]. Rear=40.

---

### Solutions

#### Python

```python
class MyCircularDeque:
    def __init__(self, k: int):
        # start your solution
        self.capacity = k
        self.deque = [0] * k
        self.front = 0
        self.rear = 0
        self.size = 0
        # end your solution

    def insertFront(self, value: int) -> bool:
        # start your solution
        if self.isFull():
            return False
        self.front = (self.front - 1 + self.capacity) % self.capacity
        self.deque[self.front] = value
        self.size += 1
        return True
        # end your solution

    def insertLast(self, value: int) -> bool:
        # start your solution
        if self.isFull():
            return False
        self.deque[self.rear] = value
        self.rear = (self.rear + 1) % self.capacity
        self.size += 1
        return True
        # end your solution

    def deleteFront(self) -> bool:
        # start your solution
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return True
        # end your solution

    def deleteLast(self) -> bool:
        # start your solution
        if self.isEmpty():
            return False
        self.rear = (self.rear - 1 + self.capacity) % self.capacity
        self.size -= 1
        return True
        # end your solution

    def getFront(self) -> int:
        # start your solution
        if self.isEmpty():
            return -1
        return self.deque[self.front]
        # end your solution

    def getRear(self) -> int:
        # start your solution
        if self.isEmpty():
            return -1
        return self.deque[(self.rear - 1 + self.capacity) % self.capacity]
        # end your solution

    def isEmpty(self) -> bool:
        # start your solution
        return self.size == 0
        # end your solution

    def isFull(self) -> bool:
        # start your solution
        return self.size == self.capacity
        # end your solution


def main():
    k = int(input())
    n = int(input())
    deque = MyCircularDeque(k)
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "insertFront":
            print("true" if deque.insertFront(int(operation[1])) else "false")
        elif operation[0] == "insertLast":
            print("true" if deque.insertLast(int(operation[1])) else "false")
        elif operation[0] == "deleteFront":
            print("true" if deque.deleteFront() else "false")
        elif operation[0] == "deleteLast":
            print("true" if deque.deleteLast() else "false")
        elif operation[0] == "getFront":
            print(deque.getFront())
        elif operation[0] == "getRear":
            print(deque.getRear())
        elif operation[0] == "isEmpty":
            print("true" if deque.isEmpty() else "false")
        elif operation[0] == "isFull":
            print("true" if deque.isFull() else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class MyCircularDeque {
private:
    vector<int> deque;
    int capacity;
    int frontIdx;
    int rearIdx;
    int count;

public:
    MyCircularDeque(int k) {
        capacity = k;
        deque.resize(k);
        frontIdx = 0;
        rearIdx = 0;
        count = 0;
    }
    
    bool insertFront(int value) {
        if (isFull()) return false;
        frontIdx = (frontIdx - 1 + capacity) % capacity;
        deque[frontIdx] = value;
        count++;
        return true;
    }
    
    bool insertLast(int value) {
        if (isFull()) return false;
        deque[rearIdx] = value;
        rearIdx = (rearIdx + 1) % capacity;
        count++;
        return true;
    }
    
    bool deleteFront() {
        if (isEmpty()) return false;
        frontIdx = (frontIdx + 1) % capacity;
        count--;
        return true;
    }
    
    bool deleteLast() {
        if (isEmpty()) return false;
        rearIdx = (rearIdx - 1 + capacity) % capacity;
        count--;
        return true;
    }
    
    int getFront() {
        if (isEmpty()) return -1;
        return deque[frontIdx];
    }
    
    int getRear() {
        if (isEmpty()) return -1;
        return deque[(rearIdx - 1 + capacity) % capacity];
    }
    
    bool isEmpty() {
        return count == 0;
    }
    
    bool isFull() {
        return count == capacity;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int k, n;
    cin >> k >> n;
    
    MyCircularDeque deque(k);
    
    for (int i = 0; i < n; i++) {
        string op;
        cin >> op;
        
        if (op == "insertFront") {
            int val; cin >> val;
            cout << (deque.insertFront(val) ? "true" : "false") << endl;
        } else if (op == "insertLast") {
            int val; cin >> val;
            cout << (deque.insertLast(val) ? "true" : "false") << endl;
        } else if (op == "deleteFront") {
            cout << (deque.deleteFront() ? "true" : "false") << endl;
        } else if (op == "deleteLast") {
            cout << (deque.deleteLast() ? "true" : "false") << endl;
        } else if (op == "getFront") {
            cout << deque.getFront() << endl;
        } else if (op == "getRear") {
            cout << deque.getRear() << endl;
        } else if (op == "isEmpty") {
            cout << (deque.isEmpty() ? "true" : "false") << endl;
        } else if (op == "isFull") {
            cout << (deque.isFull() ? "true" : "false") << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MyCircularDeque {
    private int[] deque;
    private int capacity;
    private int frontIdx;
    private int rearIdx;
    private int count;
    
    public MyCircularDeque(int k) {
        capacity = k;
        deque = new int[k];
        frontIdx = 0;
        rearIdx = 0;
        count = 0;
    }
    
    public boolean insertFront(int value) {
        if (isFull()) return false;
        frontIdx = (frontIdx - 1 + capacity) % capacity;
        deque[frontIdx] = value;
        count++;
        return true;
    }
    
    public boolean insertLast(int value) {
        if (isFull()) return false;
        deque[rearIdx] = value;
        rearIdx = (rearIdx + 1) % capacity;
        count++;
        return true;
    }
    
    public boolean deleteFront() {
        if (isEmpty()) return false;
        frontIdx = (frontIdx + 1) % capacity;
        count--;
        return true;
    }
    
    public boolean deleteLast() {
        if (isEmpty()) return false;
        rearIdx = (rearIdx - 1 + capacity) % capacity;
        count--;
        return true;
    }
    
    public int getFront() {
        if (isEmpty()) return -1;
        return deque[frontIdx];
    }
    
    public int getRear() {
        if (isEmpty()) return -1;
        return deque[(rearIdx - 1 + capacity) % capacity];
    }
    
    public boolean isEmpty() {
        return count == 0;
    }
    
    public boolean isFull() {
        return count == capacity;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int k = Integer.parseInt(sc.nextLine());
        int n = Integer.parseInt(sc.nextLine());
        
        MyCircularDeque deque = new MyCircularDeque(k);
        
        for (int i = 0; i < n; i++) {
            String[] op = sc.nextLine().split(" ");
            
            if (op[0].equals("insertFront")) {
                System.out.println(deque.insertFront(Integer.parseInt(op[1])) ? "true" : "false");
            } else if (op[0].equals("insertLast")) {
                System.out.println(deque.insertLast(Integer.parseInt(op[1])) ? "true" : "false");
            } else if (op[0].equals("deleteFront")) {
                System.out.println(deque.deleteFront() ? "true" : "false");
            } else if (op[0].equals("deleteLast")) {
                System.out.println(deque.deleteLast() ? "true" : "false");
            } else if (op[0].equals("getFront")) {
                System.out.println(deque.getFront());
            } else if (op[0].equals("getRear")) {
                System.out.println(deque.getRear());
            } else if (op[0].equals("isEmpty")) {
                System.out.println(deque.isEmpty() ? "true" : "false");
            } else if (op[0].equals("isFull")) {
                System.out.println(deque.isFull() ? "true" : "false");
            }
        }
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class MyCircularDeque:
    def __init__(self, k: int):
        # start your solution
        
        # end your solution

    def insertFront(self, value: int) -> bool:
        # start your solution
        
        # end your solution

    def insertLast(self, value: int) -> bool:
        # start your solution
        
        # end your solution

    def deleteFront(self) -> bool:
        # start your solution
        
        # end your solution

    def deleteLast(self) -> bool:
        # start your solution
        
        # end your solution

    def getFront(self) -> int:
        # start your solution
        
        # end your solution

    def getRear(self) -> int:
        # start your solution
        
        # end your solution

    def isEmpty(self) -> bool:
        # start your solution
        
        # end your solution

    def isFull(self) -> bool:
        # start your solution
        
        # end your solution


def main():
    k = int(input())
    n = int(input())
    deque = MyCircularDeque(k)
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "insertFront":
            print("true" if deque.insertFront(int(operation[1])) else "false")
        elif operation[0] == "insertLast":
            print("true" if deque.insertLast(int(operation[1])) else "false")
        elif operation[0] == "deleteFront":
            print("true" if deque.deleteFront() else "false")
        elif operation[0] == "deleteLast":
            print("true" if deque.deleteLast() else "false")
        elif operation[0] == "getFront":
            print(deque.getFront())
        elif operation[0] == "getRear":
            print(deque.getRear())
        elif operation[0] == "isEmpty":
            print("true" if deque.isEmpty() else "false")
        elif operation[0] == "isFull":
            print("true" if deque.isFull() else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class MyCircularDeque {
public:
    MyCircularDeque(int k) {
        // start your solution
        
        // end your solution
    }
    
    bool insertFront(int value) {
        // start your solution
        
        // end your solution
    }
    
    bool insertLast(int value) {
        // start your solution
        
        // end your solution
    }
    
    bool deleteFront() {
        // start your solution
        
        // end your solution
    }
    
    bool deleteLast() {
        // start your solution
        
        // end your solution
    }
    
    int getFront() {
        // start your solution
        
        // end your solution
    }
    
    int getRear() {
        // start your solution
        
        // end your solution
    }
    
    bool isEmpty() {
        // start your solution
        
        // end your solution
    }
    
    bool isFull() {
        // start your solution
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int k, n;
    cin >> k >> n;
    
    MyCircularDeque deque(k);
    
    for (int i = 0; i < n; i++) {
        string op;
        cin >> op;
        
        if (op == "insertFront") {
            int val; cin >> val;
            cout << (deque.insertFront(val) ? "true" : "false") << endl;
        } else if (op == "insertLast") {
            int val; cin >> val;
            cout << (deque.insertLast(val) ? "true" : "false") << endl;
        } else if (op == "deleteFront") {
            cout << (deque.deleteFront() ? "true" : "false") << endl;
        } else if (op == "deleteLast") {
            cout << (deque.deleteLast() ? "true" : "false") << endl;
        } else if (op == "getFront") {
            cout << deque.getFront() << endl;
        } else if (op == "getRear") {
            cout << deque.getRear() << endl;
        } else if (op == "isEmpty") {
            cout << (deque.isEmpty() ? "true" : "false") << endl;
        } else if (op == "isFull") {
            cout << (deque.isFull() ? "true" : "false") << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MyCircularDeque {
    public MyCircularDeque(int k) {
        // start your solution
        
        // end your solution
    }
    
    public boolean insertFront(int value) {
        // start your solution
        
        // end your solution
    }
    
    public boolean insertLast(int value) {
        // start your solution
        
        // end your solution
    }
    
    public boolean deleteFront() {
        // start your solution
        
        // end your solution
    }
    
    public boolean deleteLast() {
        // start your solution
        
        // end your solution
    }
    
    public int getFront() {
        // start your solution
        
        // end your solution
    }
    
    public int getRear() {
        // start your solution
        
        // end your solution
    }
    
    public boolean isEmpty() {
        // start your solution
        
        // end your solution
    }
    
    public boolean isFull() {
        // start your solution
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int k = Integer.parseInt(sc.nextLine());
        int n = Integer.parseInt(sc.nextLine());
        
        MyCircularDeque deque = new MyCircularDeque(k);
        
        for (int i = 0; i < n; i++) {
            String[] op = sc.nextLine().split(" ");
            
            if (op[0].equals("insertFront")) {
                System.out.println(deque.insertFront(Integer.parseInt(op[1])) ? "true" : "false");
            } else if (op[0].equals("insertLast")) {
                System.out.println(deque.insertLast(Integer.parseInt(op[1])) ? "true" : "false");
            } else if (op[0].equals("deleteFront")) {
                System.out.println(deque.deleteFront() ? "true" : "false");
            } else if (op[0].equals("deleteLast")) {
                System.out.println(deque.deleteLast() ? "true" : "false");
            } else if (op[0].equals("getFront")) {
                System.out.println(deque.getFront());
            } else if (op[0].equals("getRear")) {
                System.out.println(deque.getRear());
            } else if (op[0].equals("isEmpty")) {
                System.out.println(deque.isEmpty() ? "true" : "false");
            } else if (op[0].equals("isFull")) {
                System.out.println(deque.isFull() ? "true" : "false");
            }
        }
        
        sc.close();
    }
}
```
