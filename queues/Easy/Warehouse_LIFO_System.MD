# Warehouse LIFO System

### Problem Statement

At Amazon's fulfillment center in Manesar, the inventory system only supports queue-based (FIFO) storage. However, for certain perishable items, they need last-in-first-out (LIFO) access. Design a stack using only queue operations.

Implement a stack using only two queues. The implemented stack should support all standard stack operations: push, pop, top, and empty.

### Input Format

- The first line contains an integer `n`, the number of operations.
- The next `n` lines each contain an operation:
  - `push x` - Push element x onto stack
  - `pop` - Remove and return the top element
  - `top` - Return the top element without removing
  - `empty` - Return true if stack is empty, false otherwise

### Output Format

- For `pop` and `top`, print the returned value.
- For `empty`, print `true` or `false`.

### Constraints

- `1 <= n <= 100`
- `1 <= x <= 9`
- At most 100 calls will be made to push, pop, top, and empty
- All calls to pop and top are valid (stack is not empty)

### Test Cases

#### Test Case 1
**Input:**
```
6
push 1
push 2
top
pop
empty
pop
```
**Output:**
```
2
2
false
1
```
**Explanation:** Push 1,2. Top is 2. Pop returns 2. Not empty. Pop returns 1.

---

#### Test Case 2
**Input:**
```
4
push 5
push 3
pop
top
```
**Output:**
```
3
5
```
**Explanation:** Push 5,3. Pop returns 3 (last in). Top returns 5.

---

#### Test Case 3
**Input:**
```
3
push 1
empty
pop
```
**Output:**
```
false
1
```
**Explanation:** Stack has one element, not empty. Pop returns 1.

---

#### Test Case 4
**Input:**
```
5
push 1
push 2
push 3
top
pop
```
**Output:**
```
3
3
```
**Explanation:** LIFO order. Top and pop both give 3 (most recent).

---

#### Test Case 5
**Input:**
```
7
push 4
push 5
push 6
pop
pop
pop
empty
```
**Output:**
```
6
5
4
true
```
**Explanation:** Pop all in LIFO order. Stack now empty.

---

#### Test Case 6
**Input:**
```
4
push 7
top
top
pop
```
**Output:**
```
7
7
7
```
**Explanation:** Top doesn't remove element. All operations return 7.

---

#### Test Case 7
**Input:**
```
6
push 1
pop
push 2
push 3
pop
top
```
**Output:**
```
1
3
2
```
**Explanation:** Push 1, pop 1. Push 2,3. Pop 3. Top is 2.

---

### Solutions

#### Python

```python
from collections import deque

class MyStack:
    # start your solution
    def __init__(self):
        self.queue = deque()

    def push(self, x: int) -> None:
        self.queue.append(x)
        for _ in range(len(self.queue) - 1):
            self.queue.append(self.queue.popleft())

    def pop(self) -> int:
        return self.queue.popleft()

    def top(self) -> int:
        return self.queue[0]

    def empty(self) -> bool:
        return len(self.queue) == 0
    # end your solution


def main():
    n = int(input())
    stack = MyStack()
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "push":
            stack.push(int(operation[1]))
        elif operation[0] == "pop":
            print(stack.pop())
        elif operation[0] == "top":
            print(stack.top())
        elif operation[0] == "empty":
            print("true" if stack.empty() else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
#include <queue>
using namespace std;

class MyStack {
    // start your solution
private:
    queue<int> q;

public:
    MyStack() {}

    void push(int x) {
        q.push(x);
        for (int i = 0; i < q.size() - 1; i++) {
            q.push(q.front());
            q.pop();
        }
    }

    int pop() {
        int val = q.front();
        q.pop();
        return val;
    }

    int top() {
        return q.front();
    }

    bool empty() {
        return q.empty();
    }
    // end your solution
};


int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    MyStack stack;
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "push") {
            int x;
            cin >> x;
            stack.push(x);
        } else if (operation == "pop") {
            cout << stack.pop() << endl;
        } else if (operation == "top") {
            cout << stack.top() << endl;
        } else if (operation == "empty") {
            cout << (stack.empty() ? "true" : "false") << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MyStack {
    // start your solution
    private Queue<Integer> queue;

    public MyStack() {
        queue = new LinkedList<>();
    }

    public void push(int x) {
        queue.offer(x);
        for (int i = 0; i < queue.size() - 1; i++) {
            queue.offer(queue.poll());
        }
    }

    public int pop() {
        return queue.poll();
    }

    public int top() {
        return queue.peek();
    }

    public boolean empty() {
        return queue.isEmpty();
    }
    // end your solution
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine());
        MyStack stack = new MyStack();
        
        for (int i = 0; i < n; i++) {
            String[] operation = sc.nextLine().split(" ");
            
            if (operation[0].equals("push")) {
                stack.push(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("pop")) {
                System.out.println(stack.pop());
            } else if (operation[0].equals("top")) {
                System.out.println(stack.top());
            } else if (operation[0].equals("empty")) {
                System.out.println(stack.empty() ? "true" : "false");
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

class MyStack:
    # start your solution
    def __init__(self):
        pass

    def push(self, x: int) -> None:
        pass

    def pop(self) -> int:
        pass

    def top(self) -> int:
        pass

    def empty(self) -> bool:
        pass
    # end your solution

def main():
    n = int(input())
    stack = MyStack()
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "push":
            stack.push(int(operation[1]))
        elif operation[0] == "pop":
            print(stack.pop())
        elif operation[0] == "top":
            print(stack.top())
        elif operation[0] == "empty":
            print("true" if stack.empty() else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <queue>
#include <string>
using namespace std;

class MyStack {
    // start your solution
public:
    MyStack() {}

    void push(int x) {}

    int pop() {}

    int top() {}

    bool empty() {}
    // end your solution
};


int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    MyStack stack;
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "push") {
            int x;
            cin >> x;
            stack.push(x);
        } else if (operation == "pop") {
            cout << stack.pop() << endl;
        } else if (operation == "top") {
            cout << stack.top() << endl;
        } else if (operation == "empty") {
            cout << (stack.empty() ? "true" : "false") << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MyStack {
    // start your solution
    public MyStack() {}

    public void push(int x) {}

    public int pop() {}

    public int top() {}

    public boolean empty() {}
    // end your solution
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine());
        MyStack stack = new MyStack();
        
        for (int i = 0; i < n; i++) {
            String[] operation = sc.nextLine().split(" ");
            
            if (operation[0].equals("push")) {
                stack.push(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("pop")) {
                System.out.println(stack.pop());
            } else if (operation[0].equals("top")) {
                System.out.println(stack.top());
            } else if (operation[0].equals("empty")) {
                System.out.println(stack.empty() ? "true" : "false");
            }
        }
        
        sc.close();
    }
}
```
