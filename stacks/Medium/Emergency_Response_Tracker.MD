# Emergency Response Tracker

### Problem Statement

The National Disaster Management Authority (NDMA) in New Delhi needs a system to track emergency severity levels. The system must support adding new emergencies, removing the most recent one, viewing the most recent one, and instantly retrieving the minimum (most critical) severity level at any time.

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

### Input Format

- The first line contains an integer `n`, the number of operations.
- The next `n` lines each contain an operation:
  - `push x` - Push element x onto stack
  - `pop` - Remove the top element
  - `top` - Get the top element
  - `getMin` - Retrieve the minimum element in the stack

### Output Format

- For `top` and `getMin`, print the returned value.

### Constraints

- `-2^31 <= val <= 2^31 - 1`
- Methods `pop`, `top` and `getMin` will always be called on non-empty stacks
- At most `3 * 10^4` calls will be made to push, pop, top, and getMin

### Test Cases

#### Test Case 1
**Input:**
```
7
push -2
push 0
push -3
getMin
pop
top
getMin
```
**Output:**
```
-3
0
-2
```
**Explanation:** Push -2,0,-3. Min is -3. Pop -3. Top is 0. Min now -2.

---

#### Test Case 2
**Input:**
```
5
push 1
push 2
push 3
getMin
top
```
**Output:**
```
1
3
```
**Explanation:** Push 1,2,3. Min is 1. Top is 3.

---

#### Test Case 3
**Input:**
```
6
push 5
push 3
push 7
getMin
pop
getMin
```
**Output:**
```
3
3
```
**Explanation:** Min is 3. After popping 7, min is still 3.

---

#### Test Case 4
**Input:**
```
4
push 10
getMin
top
pop
```
**Output:**
```
10
10
```
**Explanation:** Single element. Both min and top are 10.

---

#### Test Case 5
**Input:**
```
8
push 2
push 2
push 1
push 1
getMin
pop
getMin
pop
```
**Output:**
```
1
1
```
**Explanation:** Duplicate minimums handled correctly. After first pop, min still 1.

---

#### Test Case 6
**Input:**
```
6
push -1
push -2
push -3
pop
pop
getMin
```
**Output:**
```
-1
```
**Explanation:** Pop -3, pop -2. Only -1 remains. Min is -1.

---

#### Test Case 7
**Input:**
```
9
push 3
push 1
push 2
getMin
pop
getMin
pop
getMin
top
```
**Output:**
```
1
1
3
3
```
**Explanation:** Track minimum through multiple pops. Min updates when 1 is popped.

---

### Solutions

#### Python

```python
class MinStack:
    def __init__(self):
        # start your solution
        self.stack = []
        self.minStack = []
        # end your solution

    def push(self, val: int) -> None:
        # start your solution
        self.stack.append(val)
        if not self.minStack or val <= self.minStack[-1]:
            self.minStack.append(val)
        # end your solution

    def pop(self) -> None:
        # start your solution
        if self.stack[-1] == self.minStack[-1]:
            self.minStack.pop()
        self.stack.pop()
        # end your solution

    def top(self) -> int:
        # start your solution
        return self.stack[-1]
        # end your solution

    def getMin(self) -> int:
        # start your solution
        return self.minStack[-1]
        # end your solution


def main():
    n = int(input())
    minStack = MinStack()
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "push":
            minStack.push(int(operation[1]))
        elif operation[0] == "pop":
            minStack.pop()
        elif operation[0] == "top":
            print(minStack.top())
        elif operation[0] == "getMin":
            print(minStack.getMin())


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

class MinStack {
private:
    stack<int> mainStack;
    stack<int> minStack;

public:
    MinStack() {
        // start your solution
        // end your solution
    }
    
    void push(int val) {
        // start your solution
        mainStack.push(val);
        if (minStack.empty() || val <= minStack.top()) {
            minStack.push(val);
        }
        // end your solution
    }
    
    void pop() {
        // start your solution
        if (mainStack.top() == minStack.top()) {
            minStack.pop();
        }
        mainStack.pop();
        // end your solution
    }
    
    int top() {
        // start your solution
        return mainStack.top();
        // end your solution
    }
    
    int getMin() {
        // start your solution
        return minStack.top();
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    MinStack minStack;
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "push") {
            int val;
            cin >> val;
            minStack.push(val);
        } else if (operation == "pop") {
            minStack.pop();
        } else if (operation == "top") {
            cout << minStack.top() << endl;
        } else if (operation == "getMin") {
            cout << minStack.getMin() << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MinStack {
    private Stack<Integer> mainStack;
    private Stack<Integer> minStack;
    
    public MinStack() {
        // start your solution
        mainStack = new Stack<>();
        minStack = new Stack<>();
        // end your solution
    }
    
    public void push(int val) {
        // start your solution
        mainStack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
        // end your solution
    }
    
    public void pop() {
        // start your solution
        if (mainStack.peek().equals(minStack.peek())) {
            minStack.pop();
        }
        mainStack.pop();
        // end your solution
    }
    
    public int top() {
        // start your solution
        return mainStack.peek();
        // end your solution
    }
    
    public int getMin() {
        // start your solution
        return minStack.peek();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine());
        MinStack minStack = new MinStack();
        
        for (int i = 0; i < n; i++) {
            String[] operation = sc.nextLine().split(" ");
            
            if (operation[0].equals("push")) {
                minStack.push(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("pop")) {
                minStack.pop();
            } else if (operation[0].equals("top")) {
                System.out.println(minStack.top());
            } else if (operation[0].equals("getMin")) {
                System.out.println(minStack.getMin());
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
class MinStack:
    def __init__(self):
        # start your solution
        
        # end your solution

    def push(self, val: int) -> None:
        # start your solution
        
        # end your solution

    def pop(self) -> None:
        # start your solution
        
        # end your solution

    def top(self) -> int:
        # start your solution
        
        # end your solution

    def getMin(self) -> int:
        # start your solution
        
        # end your solution


def main():
    n = int(input())
    minStack = MinStack()
    
    for _ in range(n):
        operation = input().split()
        
        if operation[0] == "push":
            minStack.push(int(operation[1]))
        elif operation[0] == "pop":
            minStack.pop()
        elif operation[0] == "top":
            print(minStack.top())
        elif operation[0] == "getMin":
            print(minStack.getMin())


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

class MinStack {
public:
    MinStack() {
        // start your solution
        
        // end your solution
    }
    
    void push(int val) {
        // start your solution
        
        // end your solution
    }
    
    void pop() {
        // start your solution
        
        // end your solution
    }
    
    int top() {
        // start your solution
        
        // end your solution
    }
    
    int getMin() {
        // start your solution
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    MinStack minStack;
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "push") {
            int val;
            cin >> val;
            minStack.push(val);
        } else if (operation == "pop") {
            minStack.pop();
        } else if (operation == "top") {
            cout << minStack.top() << endl;
        } else if (operation == "getMin") {
            cout << minStack.getMin() << endl;
        }
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MinStack {
    public MinStack() {
        // start your solution
        
        // end your solution
    }
    
    public void push(int val) {
        // start your solution
        
        // end your solution
    }
    
    public void pop() {
        // start your solution
        
        // end your solution
    }
    
    public int top() {
        // start your solution
        
        // end your solution
    }
    
    public int getMin() {
        // start your solution
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine());
        MinStack minStack = new MinStack();
        
        for (int i = 0; i < n; i++) {
            String[] operation = sc.nextLine().split(" ");
            
            if (operation[0].equals("push")) {
                minStack.push(Integer.parseInt(operation[1]));
            } else if (operation[0].equals("pop")) {
                minStack.pop();
            } else if (operation[0].equals("top")) {
                System.out.println(minStack.top());
            } else if (operation[0].equals("getMin")) {
                System.out.println(minStack.getMin());
            }
        }
        
        sc.close();
    }
}
```
