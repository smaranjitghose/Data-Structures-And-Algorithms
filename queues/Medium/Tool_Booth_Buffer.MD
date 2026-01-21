# Toll Booth Buffer

### Problem Statement

The National Highways Authority of India (NHAI) operates electronic toll booths on the Mumbai-Pune Expressway. The toll system uses a circular buffer to store recent vehicle entries for auditing. When the buffer is full, new entries can only be added after removing old ones.

Design a circular queue implementation with a fixed capacity.

Operations:
- `MyCircularQueue(k)` - Initialize queue with capacity k
- `enQueue(value)` - Insert element, return true if successful
- `deQueue()` - Delete front element, return true if successful
- `Front()` - Get front element, return -1 if empty
- `Rear()` - Get rear element, return -1 if empty
- `isEmpty()` - Check if queue is empty
- `isFull()` - Check if queue is full

### Input Format

- The first line contains the capacity `k`.
- The second line contains the number of operations `n`.
- The next `n` lines each contain an operation.

### Output Format

- For operations returning boolean, print `true` or `false`.
- For `Front` and `Rear`, print the value or -1.

### Constraints

- `1 <= k <= 1000`
- `0 <= value <= 1000`
- At most 3000 operations

### Test Cases

#### Test Case 1
**Input:**
```
3
10
enQueue 1
enQueue 2
enQueue 3
enQueue 4
Rear
isFull
deQueue
enQueue 4
Rear
Front
```
**Output:**
```
true
true
true
false
3
true
true
true
4
2
```
**Explanation:** Capacity 3. Add 1,2,3 (success). Add 4 fails (full). Rear=3. Full=true. Remove front. Add 4 succeeds. Rear=4. Front=2.

---

#### Test Case 2
**Input:**
```
2
6
enQueue 10
enQueue 20
Front
Rear
deQueue
Rear
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
**Explanation:** Queue [10,20]. Front=10, Rear=20. After deQueue, only 20 remains.

---

#### Test Case 3
**Input:**
```
1
5
isEmpty
enQueue 5
isEmpty
isFull
deQueue
```
**Output:**
```
true
true
false
true
true
```
**Explanation:** Capacity 1. Initially empty. Add 5, now full. Remove succeeds.

---

#### Test Case 4
**Input:**
```
3
4
Front
Rear
deQueue
isEmpty
```
**Output:**
```
-1
-1
false
true
```
**Explanation:** Empty queue. Front/Rear return -1. deQueue fails.

---

#### Test Case 5
**Input:**
```
5
8
enQueue 1
enQueue 2
enQueue 3
deQueue
deQueue
enQueue 4
enQueue 5
Front
```
**Output:**
```
true
true
true
true
true
true
true
3
```
**Explanation:** Add 1,2,3. Remove 1,2. Add 4,5. Queue is [3,4,5]. Front=3.

---

#### Test Case 6
**Input:**
```
4
7
enQueue 10
enQueue 20
enQueue 30
enQueue 40
isFull
Front
Rear
```
**Output:**
```
true
true
true
true
true
10
40
```
**Explanation:** Full queue of 4 elements. Front=10, Rear=40.

---

#### Test Case 7
**Input:**
```
3
9
enQueue 1
deQueue
enQueue 2
deQueue
enQueue 3
deQueue
isEmpty
enQueue 4
Front
```
**Output:**
```
true
true
true
true
true
true
true
true
4
```
**Explanation:** Circular behavior - add, remove, repeat. Indices wrap around.

---

### Solutions

#### Python

```python
class MyCircularQueue:
    # start your solution
    def __init__(self, k: int):
        self.capacity = k
        self.queue = [0] * k
        self.front = 0
        self.rear = -1
        self.size = 0

    def enQueue(self, value: int) -> bool:
        if self.isFull():
            return False
        self.rear = (self.rear + 1) % self.capacity
        self.queue[self.rear] = value
        self.size += 1
        return True

    def deQueue(self) -> bool:
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return True

    def Front(self) -> int:
        if self.isEmpty():
            return -1
        return self.queue[self.front]

    def Rear(self) -> int:
        if self.isEmpty():
            return -1
        return self.queue[self.rear]

    def isEmpty(self) -> bool:
        return self.size == 0

    def isFull(self) -> bool:
        return self.size == self.capacity
    # end your solution



def main():
    k = int(input())
    n = int(input())
    queue = MyCircularQueue(k)
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "enQueue":
            print("true" if queue.enQueue(int(operation[1])) else "false")
        elif operation[0] == "deQueue":
            print("true" if queue.deQueue() else "false")
        elif operation[0] == "Front":
            print(queue.Front())
        elif operation[0] == "Rear":
            print(queue.Rear())
        elif operation[0] == "isEmpty":
            print("true" if queue.isEmpty() else "false")
        elif operation[0] == "isFull":
            print("true" if queue.isFull() else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class MyCircularQueue {
    // start your solution
private:
    vector<int> queue;
    int capacity;
    int frontIdx;
    int rearIdx;
    int count;

public:
    MyCircularQueue(int k) {
        capacity = k;
        queue.resize(k);
        frontIdx = 0;
        rearIdx = -1;
        count = 0;
    }

    bool enQueue(int value) {
        if (isFull()) return false;
        rearIdx = (rearIdx + 1) % capacity;
        queue[rearIdx] = value;
        count++;
        return true;
    }

    bool deQueue() {
        if (isEmpty()) return false;
        frontIdx = (frontIdx + 1) % capacity;
        count--;
        return true;
    }

    int Front() {
        if (isEmpty()) return -1;
        return queue[frontIdx];
    }

    int Rear() {
        if (isEmpty()) return -1;
        return queue[rearIdx];
    }

    bool isEmpty() {
        return count == 0;
    }

    bool isFull() {
        return count == capacity;
    }
    // end your solution
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int k, n;
    cin >> k >> n;
    
    MyCircularQueue queue(k);
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "enQueue") {
            int val; cin >> val;
            cout << (queue.enQueue(val) ? "true" : "false") << endl;
        } else if (operation == "deQueue") {
            cout << (queue.deQueue() ? "true" : "false") << endl;
        } else if (operation == "Front") {
            cout << queue.Front() << endl;
        } else if (operation == "Rear") {
            cout << queue.Rear() << endl;
        } else if (operation == "isEmpty") {
            cout << (queue.isEmpty() ? "true" : "false") << endl;
        } else if (operation == "isFull") {
            cout << (queue.isFull() ? "true" : "false") << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MyCircularQueue {
    // start your solution
    private int[] queue;
    private int capacity;
    private int frontIdx;
    private int rearIdx;
    private int count;

    public MyCircularQueue(int k) {
        capacity = k;
        queue = new int[k];
        frontIdx = 0;
        rearIdx = -1;
        count = 0;
    }

    public boolean enQueue(int value) {
        if (isFull()) return false;
        rearIdx = (rearIdx + 1) % capacity;
        queue[rearIdx] = value;
        count++;
        return true;
    }

    public boolean deQueue() {
        if (isEmpty()) return false;
        frontIdx = (frontIdx + 1) % capacity;
        count--;
        return true;
    }

    public int Front() {
        if (isEmpty()) return -1;
        return queue[frontIdx];
    }

    public int Rear() {
        if (isEmpty()) return -1;
        return queue[rearIdx];
    }

    public boolean isEmpty() {
        return count == 0;
    }

    public boolean isFull() {
        return count == capacity;
    }
    // end your solution
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int k = Integer.parseInt(sc.nextLine());
        int n = Integer.parseInt(sc.nextLine());
        
        MyCircularQueue queue = new MyCircularQueue(k);
        
        for (int i = 0; i < n; i++) {
            String[] operation = sc.nextLine().split(" ");
            
            if (operation[0].equals("enQueue")) {
                System.out.println(queue.enQueue(Integer.parseInt(operation[1])) ? "true" : "false");
            } else if (operation[0].equals("deQueue")) {
                System.out.println(queue.deQueue() ? "true" : "false");
            } else if (operation[0].equals("Front")) {
                System.out.println(queue.Front());
            } else if (operation[0].equals("Rear")) {
                System.out.println(queue.Rear());
            } else if (operation[0].equals("isEmpty")) {
                System.out.println(queue.isEmpty() ? "true" : "false");
            } else if (operation[0].equals("isFull")) {
                System.out.println(queue.isFull() ? "true" : "false");
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
class MyCircularQueue:
    # start your solution
    def __init__(self, k: int):
        pass

    def enQueue(self, value: int) -> bool:
        pass

    def deQueue(self) -> bool:
        pass

    def Front(self) -> int:
        pass

    def Rear(self) -> int:
        pass

    def isEmpty(self) -> bool:
        pass

    def isFull(self) -> bool:
        pass
    # end your solution



def main():
    k = int(input())
    n = int(input())
    queue = MyCircularQueue(k)
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "enQueue":
            print("true" if queue.enQueue(int(operation[1])) else "false")
        elif operation[0] == "deQueue":
            print("true" if queue.deQueue() else "false")
        elif operation[0] == "Front":
            print(queue.Front())
        elif operation[0] == "Rear":
            print(queue.Rear())
        elif operation[0] == "isEmpty":
            print("true" if queue.isEmpty() else "false")
        elif operation[0] == "isFull":
            print("true" if queue.isFull() else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;
class MyCircularQueue {
    // start your solution
public:
    MyCircularQueue(int k) {}

    bool enQueue(int value) {}

    bool deQueue() {}

    int Front() {}

    int Rear() {}

    bool isEmpty() {}

    bool isFull() {}
    // end your solution
};


int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int k, n;
    cin >> k >> n;
    
    MyCircularQueue queue(k);
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "enQueue") {
            int val; cin >> val;
            cout << (queue.enQueue(val) ? "true" : "false") << endl;
        } else if (operation == "deQueue") {
            cout << (queue.deQueue() ? "true" : "false") << endl;
        } else if (operation == "Front") {
            cout << queue.Front() << endl;
        } else if (operation == "Rear") {
            cout << queue.Rear() << endl;
        } else if (operation == "isEmpty") {
            cout << (queue.isEmpty() ? "true" : "false") << endl;
        } else if (operation == "isFull") {
            cout << (queue.isFull() ? "true" : "false") << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MyCircularQueue {
    // start your solution
    public MyCircularQueue(int k) {}

    public boolean enQueue(int value) {}

    public boolean deQueue() {}

    public int Front() {}

    public int Rear() {}

    public boolean isEmpty() {}

    public boolean isFull() {}
    // end your solution
}


public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int k = Integer.parseInt(sc.nextLine());
        int n = Integer.parseInt(sc.nextLine());
        
        MyCircularQueue queue = new MyCircularQueue(k);
        
        for (int i = 0; i < n; i++) {
            String[] operation = sc.nextLine().split(" ");
            
            if (operation[0].equals("enQueue")) {
                System.out.println(queue.enQueue(Integer.parseInt(operation[1])) ? "true" : "false");
            } else if (operation[0].equals("deQueue")) {
                System.out.println(queue.deQueue() ? "true" : "false");
            } else if (operation[0].equals("Front")) {
                System.out.println(queue.Front());
            } else if (operation[0].equals("Rear")) {
                System.out.println(queue.Rear());
            } else if (operation[0].equals("isEmpty")) {
                System.out.println(queue.isEmpty() ? "true" : "false");
            } else if (operation[0].equals("isFull")) {
                System.out.println(queue.isFull() ? "true" : "false");
            }
        }
        
        sc.close();
    }
}
```
