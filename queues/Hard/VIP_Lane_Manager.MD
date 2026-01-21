# VIP Lane Manager

### Problem Statement

At the Taj Mahal entry in Agra, the tourism department manages a special VIP queue that allows visitors to join at the front, middle, or back, and leave from the front, middle, or back positions.

Design a queue that supports push and pop operations at front, middle, and back positions.

Operations:
- `pushFront(val)` - Add val to the front
- `pushMiddle(val)` - Add val to the middle (if odd length, middle is (size/2) position)
- `pushBack(val)` - Add val to the back
- `popFront()` - Remove and return front element (-1 if empty)
- `popMiddle()` - Remove and return middle element (-1 if empty)
- `popBack()` - Remove and return back element (-1 if empty)

### Input Format

- The first line contains an integer `n`, the number of operations.
- The next `n` lines each contain an operation and optionally a value.

### Output Format

- For pop operations, print the returned value.

### Constraints

- `1 <= val <= 10^9`
- At most `1000` calls will be made to each method
- Pop operations on empty queue return -1

### Test Cases

#### Test Case 1
**Input:**
```
10
pushFront 1
pushBack 2
pushMiddle 3
pushMiddle 4
popFront
popMiddle
popMiddle
popBack
popFront
popFront
```
**Output:**
```
1
3
4
2
-1
-1
```
**Explanation:** 
- pushFront(1): [1]
- pushBack(2): [1,2]
- pushMiddle(3): [1,3,2]
- pushMiddle(4): [1,4,3,2]
- popFront: return 1, queue [4,3,2]
- popMiddle: return 3, queue [4,2]
- popMiddle: return 4, queue [2]
- popBack: return 2, queue []
- popFront: return -1 (empty)
- popFront: return -1 (empty)

---

#### Test Case 2
**Input:**
```
5
pushBack 10
pushBack 20
pushBack 30
popMiddle
popMiddle
```
**Output:**
```
20
10
```
**Explanation:** [10,20,30] → pop middle (20) → [10,30] → pop middle (10) → [30]

---

#### Test Case 3
**Input:**
```
4
popFront
popMiddle
popBack
pushFront 5
```
**Output:**
```
-1
-1
-1
```
**Explanation:** All pops on empty queue return -1.

---

#### Test Case 4
**Input:**
```
6
pushFront 1
pushFront 2
pushFront 3
popBack
popBack
popBack
```
**Output:**
```
1
2
3
```
**Explanation:** [3,2,1] → pop from back successively.

---

#### Test Case 5
**Input:**
```
5
pushMiddle 1
pushMiddle 2
pushMiddle 3
popFront
popBack
```
**Output:**
```
3
1
```
**Explanation:** [1] → [2,1] → [3,2,1] → popFront=3 → [2,1] → popBack=1

---

#### Test Case 6
**Input:**
```
7
pushBack 1
pushBack 2
pushBack 3
pushBack 4
pushBack 5
popMiddle
popMiddle
```
**Output:**
```
3
2
```
**Explanation:** [1,2,3,4,5] middle=3. After pop: [1,2,4,5] middle=2.

---

#### Test Case 7
**Input:**
```
4
pushFront 100
popMiddle
pushBack 200
popMiddle
```
**Output:**
```
100
200
```
**Explanation:** Single element is always middle.

---

### Solutions

#### Python

```python
from collections import deque

class FrontMiddleBackQueue:
    # start your solution
    def __init__(self):
        self.front = deque()
        self.back = deque()

    def _balance(self):
        if len(self.front) > len(self.back):
            self.back.appendleft(self.front.pop())
        elif len(self.back) > len(self.front) + 1:
            self.front.append(self.back.popleft())

    def pushFront(self, val: int) -> None:
        self.front.appendleft(val)
        self._balance()

    def pushMiddle(self, val: int) -> None:
        if len(self.front) < len(self.back):
            self.front.append(val)
        else:
            self.back.appendleft(val)

    def pushBack(self, val: int) -> None:
        self.back.append(val)
        self._balance()

    def popFront(self) -> int:
        if not self.front and not self.back:
            return -1
        if self.front:
            val = self.front.popleft()
        else:
            val = self.back.popleft()
        self._balance()
        return val

    def popMiddle(self) -> int:
        if not self.front and not self.back:
            return -1
        if len(self.front) == len(self.back):
            return self.front.pop()
        return self.back.popleft()

    def popBack(self) -> int:
        if not self.front and not self.back:
            return -1
        val = self.back.pop()
        self._balance()
        return val
    # end your solution



def main():
    n = int(input())
    queue = FrontMiddleBackQueue()
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "pushFront":
            queue.pushFront(int(operation[1]))
        elif operation[0] == "pushMiddle":
            queue.pushMiddle(int(operation[1]))
        elif operation[0] == "pushBack":
            queue.pushBack(int(operation[1]))
        elif operation[0] == "popFront":
            print(queue.popFront())
        elif operation[0] == "popMiddle":
            print(queue.popMiddle())
        elif operation[0] == "popBack":
            print(queue.popBack())


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <deque>
#include <string>
using namespace std;

class FrontMiddleBackQueue {
    // start your solution
private:
    deque<int> front;
    deque<int> back;

    void balance() {
        if (front.size() > back.size()) {
            back.push_front(front.back());
            front.pop_back();
        } else if (back.size() > front.size() + 1) {
            front.push_back(back.front());
            back.pop_front();
        }
    }

public:
    FrontMiddleBackQueue() {}

    void pushFront(int val) {
        front.push_front(val);
        balance();
    }

    void pushMiddle(int val) {
        if (front.size() < back.size()) {
            front.push_back(val);
        } else {
            back.push_front(val);
        }
    }

    void pushBack(int val) {
        back.push_back(val);
        balance();
    }

    int popFront() {
        if (front.empty() && back.empty()) return -1;
        int val;
        if (!front.empty()) {
            val = front.front();
            front.pop_front();
        } else {
            val = back.front();
            back.pop_front();
        }
        balance();
        return val;
    }

    int popMiddle() {
        if (front.empty() && back.empty()) return -1;
        if (front.size() == back.size()) {
            int val = front.back();
            front.pop_back();
            return val;
        }
        int val = back.front();
        back.pop_front();
        return val;
    }

    int popBack() {
        if (front.empty() && back.empty()) return -1;
        int val = back.back();
        back.pop_back();
        balance();
        return val;
    }
    // end your solution
};


int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    FrontMiddleBackQueue queue;
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "pushFront") {
            int val; cin >> val;
            queue.pushFront(val);
        } else if (operation == "pushMiddle") {
            int val; cin >> val;
            queue.pushMiddle(val);
        } else if (operation == "pushBack") {
            int val; cin >> val;
            queue.pushBack(val);
        } else if (operation == "popFront") {
            cout << queue.popFront() << endl;
        } else if (operation == "popMiddle") {
            cout << queue.popMiddle() << endl;
        } else if (operation == "popBack") {
            cout << queue.popBack() << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class FrontMiddleBackQueue {
    // start your solution
    private Deque<Integer> front;
    private Deque<Integer> back;

    public FrontMiddleBackQueue() {
        front = new ArrayDeque<>();
        back = new ArrayDeque<>();
    }

    private void balance() {
        if (front.size() > back.size()) {
            back.offerFirst(front.pollLast());
        } else if (back.size() > front.size() + 1) {
            front.offerLast(back.pollFirst());
        }
    }

    public void pushFront(int val) {
        front.offerFirst(val);
        balance();
    }

    public void pushMiddle(int val) {
        if (front.size() < back.size()) {
            front.offerLast(val);
        } else {
            back.offerFirst(val);
        }
    }

    public void pushBack(int val) {
        back.offerLast(val);
        balance();
    }

    public int popFront() {
        if (front.isEmpty() && back.isEmpty()) return -1;
        int val = !front.isEmpty() ? front.pollFirst() : back.pollFirst();
        balance();
        return val;
    }

    public int popMiddle() {
        if (front.isEmpty() && back.isEmpty()) return -1;
        if (front.size() == back.size()) {
            return front.pollLast();
        }
        return back.pollFirst();
    }

    public int popBack() {
        if (front.isEmpty() && back.isEmpty()) return -1;
        int val = back.pollLast();
        balance();
        return val;
    }
    // end your solution
}


public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine());
        FrontMiddleBackQueue queue = new FrontMiddleBackQueue();
        
        for (int i = 0; i < n; i++) {
            String[] operation = sc.nextLine().split(" ");
            
            if (operation[0].equals("pushFront")) {
                queue.pushFront(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("pushMiddle")) {
                queue.pushMiddle(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("pushBack")) {
                queue.pushBack(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("popFront")) {
                System.out.println(queue.popFront());
            } else if (operation[0].equals("popMiddle")) {
                System.out.println(queue.popMiddle());
            } else if (operation[0].equals("popBack")) {
                System.out.println(queue.popBack());
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
from collections import deque

class FrontMiddleBackQueue:
    # start your solution
    def __init__(self):
        pass

    def pushFront(self, val: int) -> None:
        pass

    def pushMiddle(self, val: int) -> None:
        pass

    def pushBack(self, val: int) -> None:
        pass

    def popFront(self) -> int:
        pass

    def popMiddle(self) -> int:
        pass

    def popBack(self) -> int:
        pass
    # end your solution



def main():
    n = int(input())
    queue = FrontMiddleBackQueue()
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "pushFront":
            queue.pushFront(int(operation[1]))
        elif operation[0] == "pushMiddle":
            queue.pushMiddle(int(operation[1]))
        elif operation[0] == "pushBack":
            queue.pushBack(int(operation[1]))
        elif operation[0] == "popFront":
            print(queue.popFront())
        elif operation[0] == "popMiddle":
            print(queue.popMiddle())
        elif operation[0] == "popBack":
            print(queue.popBack())


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <deque>
#include <string>
using namespace std;

class FrontMiddleBackQueue {
    // start your solution
public:
    FrontMiddleBackQueue() {}

    void pushFront(int val) {}

    void pushMiddle(int val) {}

    void pushBack(int val) {}

    int popFront() {}

    int popMiddle() {}

    int popBack() {}
    // end your solution
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    FrontMiddleBackQueue queue;
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "pushFront") {
            int val; cin >> val;
            queue.pushFront(val);
        } else if (operation == "pushMiddle") {
            int val; cin >> val;
            queue.pushMiddle(val);
        } else if (operation == "pushBack") {
            int val; cin >> val;
            queue.pushBack(val);
        } else if (operation == "popFront") {
            cout << queue.popFront() << endl;
        } else if (operation == "popMiddle") {
            cout << queue.popMiddle() << endl;
        } else if (operation == "popBack") {
            cout << queue.popBack() << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class FrontMiddleBackQueue {
    // start your solution
    public FrontMiddleBackQueue() {}

    public void pushFront(int val) {}

    public void pushMiddle(int val) {}

    public void pushBack(int val) {}

    public int popFront() {}

    public int popMiddle() {}

    public int popBack() {}
    // end your solution
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine());
        FrontMiddleBackQueue queue = new FrontMiddleBackQueue();
        
        for (int i = 0; i < n; i++) {
            String[] operation = sc.nextLine().split(" ");
            
            if (operation[0].equals("pushFront")) {
                queue.pushFront(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("pushMiddle")) {
                queue.pushMiddle(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("pushBack")) {
                queue.pushBack(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("popFront")) {
                System.out.println(queue.popFront());
            } else if (operation[0].equals("popMiddle")) {
                System.out.println(queue.popMiddle());
            } else if (operation[0].equals("popBack")) {
                System.out.println(queue.popBack());
            }
        }
        
        sc.close();
    }
}
```
