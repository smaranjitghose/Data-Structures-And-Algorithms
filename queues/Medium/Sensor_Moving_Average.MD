# Sensor Moving Average

### Problem Statement

At Tata Steel's plant in Jamshedpur, engineers monitor temperature sensors on blast furnaces. They need to compute the moving average of the last `k` readings to detect anomalies.

Design a class that calculates the moving average of all integers in a sliding window of fixed size.

Operations:
- `MovingAverage(size)` - Initialize with window size
- `next(val)` - Add new value and return current moving average

### Input Format

- The first line contains the window size `k`.
- The second line contains the number of operations `n`.
- The next `n` lines each contain a sensor reading value.

### Output Format

- For each `next` operation, print the moving average with 5 decimal places.

### Constraints

- `1 <= size <= 1000`
- `-10^5 <= val <= 10^5`
- At most `10^4` calls to `next`

### Test Cases

#### Test Case 1
**Input:**
```
3
4
1
10
3
5
```
**Output:**
```
1.00000
5.50000
4.66667
6.00000
```
**Explanation:** 
- next(1): window [1], avg = 1/1 = 1.0
- next(10): window [1,10], avg = 11/2 = 5.5
- next(3): window [1,10,3], avg = 14/3 = 4.66667
- next(5): window [10,3,5], avg = 18/3 = 6.0 (1 dropped)

---

#### Test Case 2
**Input:**
```
1
3
5
10
15
```
**Output:**
```
5.00000
10.00000
15.00000
```
**Explanation:** Window size 1. Each value replaces previous. Average is always the current value.

---

#### Test Case 3
**Input:**
```
5
3
2
4
6
```
**Output:**
```
2.00000
3.00000
4.00000
```
**Explanation:** Window not full yet. Average of all values so far.

---

#### Test Case 4
**Input:**
```
2
5
10
20
30
40
50
```
**Output:**
```
10.00000
15.00000
25.00000
35.00000
45.00000
```
**Explanation:** After first two, window slides: [10,20]→[20,30]→[30,40]→[40,50].

---

#### Test Case 5
**Input:**
```
4
4
100
200
300
400
```
**Output:**
```
100.00000
150.00000
200.00000
250.00000
```
**Explanation:** Window fills exactly. Final avg = (100+200+300+400)/4 = 250.

---

#### Test Case 6
**Input:**
```
3
5
-10
20
-30
40
-50
```
**Output:**
```
-10.00000
5.00000
-6.66667
10.00000
-13.33333
```
**Explanation:** Handles negative values. Window slides with mix of positives and negatives.

---

#### Test Case 7
**Input:**
```
2
3
0
0
0
```
**Output:**
```
0.00000
0.00000
0.00000
```
**Explanation:** All zeros. Average remains 0.

---

### Solutions

#### Python

```python
from collections import deque

class MovingAverage:
    def __init__(self, size: int):
        # start your solution
        self.size = size
        self.queue = deque()
        self.total = 0
        # end your solution

    def next(self, val: int) -> float:
        # start your solution
        self.queue.append(val)
        self.total += val
        
        if len(self.queue) > self.size:
            self.total -= self.queue.popleft()
        
        return self.total / len(self.queue)
        # end your solution


def main():
    k = int(input())
    n = int(input())
    
    ma = MovingAverage(k)
    
    for _ in range(n):
        val = int(input())
        result = ma.next(val)
        print(f"{result:.5f}")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <queue>
#include <iomanip>
using namespace std;

class MovingAverage {
private:
    int size;
    queue<int> q;
    double total;

public:
    MovingAverage(int size) {
        // start your solution
        this->size = size;
        this->total = 0;
        // end your solution
    }
    
    double next(int val) {
        // start your solution
        q.push(val);
        total += val;
        
        if (q.size() > size) {
            total -= q.front();
            q.pop();
        }
        
        return total / q.size();
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int k, n;
    cin >> k >> n;
    
    MovingAverage ma(k);
    
    cout << fixed << setprecision(5);
    for (int i = 0; i < n; i++) {
        int val;
        cin >> val;
        cout << ma.next(val) << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MovingAverage {
    private int size;
    private Queue<Integer> queue;
    private double total;
    
    public MovingAverage(int size) {
        // start your solution
        this.size = size;
        this.queue = new LinkedList<>();
        this.total = 0;
        // end your solution
    }
    
    public double next(int val) {
        // start your solution
        queue.offer(val);
        total += val;
        
        if (queue.size() > size) {
            total -= queue.poll();
        }
        
        return total / queue.size();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int k = sc.nextInt();
        int n = sc.nextInt();
        
        MovingAverage ma = new MovingAverage(k);
        
        for (int i = 0; i < n; i++) {
            int val = sc.nextInt();
            System.out.printf("%.5f%n", ma.next(val));
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

class MovingAverage:
    def __init__(self, size: int):
        # start your solution
        
        # end your solution

    def next(self, val: int) -> float:
        # start your solution
        
        
        
        # end your solution


def main():
    k = int(input())
    n = int(input())
    
    ma = MovingAverage(k)
    
    for _ in range(n):
        val = int(input())
        result = ma.next(val)
        print(f"{result:.5f}")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <queue>
#include <iomanip>
using namespace std;

class MovingAverage {
public:
    MovingAverage(int size) {
        // start your solution
        
        // end your solution
    }
    
    double next(int val) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int k, n;
    cin >> k >> n;
    
    MovingAverage ma(k);
    
    cout << fixed << setprecision(5);
    for (int i = 0; i < n; i++) {
        int val;
        cin >> val;
        cout << ma.next(val) << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class MovingAverage {
    public MovingAverage(int size) {
        // start your solution
        
        // end your solution
    }
    
    public double next(int val) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int k = sc.nextInt();
        int n = sc.nextInt();
        
        MovingAverage ma = new MovingAverage(k);
        
        for (int i = 0; i < n; i++) {
            int val = sc.nextInt();
            System.out.printf("%.5f%n", ma.next(val));
        }
        
        sc.close();
    }
}
```
