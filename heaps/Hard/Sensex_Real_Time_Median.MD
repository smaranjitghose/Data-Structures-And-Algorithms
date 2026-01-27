# Sensex Real-Time Median Tracker

### Problem Statement

The Bombay Stock Exchange (BSE) needs a system to track the median stock price in real-time as trades happen throughout the day. As each trade comes in with a price, the system should be able to report the current median of all prices seen so far.

The median is the middle value in an ordered list. If the list has an even number of elements, the median is the average of the two middle values.

Implement the `MedianFinder` class:
- `MedianFinder()` - Initializes the MedianFinder object
- `void addNum(int num)` - Adds the integer num from the data stream to the data structure
- `double findMedian()` - Returns the median of all elements so far

### Input Format

- First line contains the number of operations `q`
- Next `q` lines each contain an operation:
  - `add x` - Add number x to the stream
  - `median` - Find the current median

### Output Format

- For each `median` operation, print the median with one decimal place

### Constraints

- `-10^5 <= num <= 10^5`
- There will be at least one element in the data structure before calling `findMedian`
- At most `5 * 10^4` calls will be made to `addNum` and `findMedian`

### Test Cases

#### Test Case 1
**Input:**
```
6
add 1
add 2
median
add 3
median
median
```
**Output:**
```
1.5
2.0
2.0
```
**Explanation:** After [1,2]: median = (1+2)/2 = 1.5. After [1,2,3]: median = 2. No change on third query.

---

#### Test Case 2
**Input:**
```
4
add 5
median
add 3
median
```
**Output:**
```
5.0
4.0
```
**Explanation:** [5] → median=5. [3,5] → median=(3+5)/2=4.

---

#### Test Case 3
**Input:**
```
5
add 1
add 2
add 3
add 4
median
```
**Output:**
```
2.5
```
**Explanation:** [1,2,3,4] → median = (2+3)/2 = 2.5.

---

#### Test Case 4
**Input:**
```
7
add 10
add 20
add 30
median
add 40
add 50
median
```
**Output:**
```
20.0
30.0
```
**Explanation:** [10,20,30] → median=20. [10,20,30,40,50] → median=30.

---

#### Test Case 5
**Input:**
```
5
add -5
add -3
add 0
add 3
median
```
**Output:**
```
-1.5
```
**Explanation:** [-5,-3,0,3] → median = (-3+0)/2 = -1.5.

---

#### Test Case 6
**Input:**
```
3
add 100
add 100
median
```
**Output:**
```
100.0
```
**Explanation:** [100,100] → median = 100.

---

#### Test Case 7
**Input:**
```
9
add 6
add 10
add 2
add 6
add 5
add 0
add 6
add 3
median
```
**Output:**
```
5.5
```
**Explanation:** Sorted: [0,2,3,5,6,6,6,10] → median = (5+6)/2 = 5.5.

---

### Solutions

#### Python
```python
import heapq


class MedianFinder:
    def __init__(self):
        # start your solution
        self.small = []  # max heap (negated)
        self.large = []  # min heap
    
    def addNum(self, num: int) -> None:
        heapq.heappush(self.small, -num)
        
        heapq.heappush(self.large, -heapq.heappop(self.small))
        
        if len(self.large) > len(self.small):
            heapq.heappush(self.small, -heapq.heappop(self.large))
    
    def findMedian(self) -> float:
        if len(self.small) > len(self.large):
            return -self.small[0]
        return (-self.small[0] + self.large[0]) / 2.0
        # end your solution


def main():
    q = int(input())
    mf = MedianFinder()
    
    for _ in range(q):
        line = input().split()
        if line[0] == "add":
            num = int(line[1])
            mf.addNum(num)
        else:
            result = mf.findMedian()
            print(f"{result:.1f}")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <queue>
#include <iomanip>
using namespace std;

class MedianFinder {
private:
    priority_queue<int> small;  // max heap
    priority_queue<int, vector<int>, greater<int>> large;  // min heap
    
public:
    // start your solution
    MedianFinder() {}
    
    void addNum(int num) {
        small.push(num);
        
        large.push(small.top());
        small.pop();
        
        if (large.size() > small.size()) {
            small.push(large.top());
            large.pop();
        }
    }
    
    double findMedian() {
        if (small.size() > large.size()) {
            return small.top();
        }
        return (small.top() + large.top()) / 2.0;
    }
    // end your solution
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int q;
    cin >> q;
    
    MedianFinder mf;
    
    for (int i = 0; i < q; i++) {
        string op;
        cin >> op;
        
        if (op == "add") {
            int num;
            cin >> num;
            mf.addNum(num);
        } else {
            cout << fixed << setprecision(1) << mf.findMedian() << endl;
        }
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class MedianFinder {
    // start your solution
    private PriorityQueue<Integer> small;  // max heap
    private PriorityQueue<Integer> large;  // min heap
    
    public MedianFinder() {
        small = new PriorityQueue<>(Collections.reverseOrder());
        large = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        small.offer(num);
        
        large.offer(small.poll());
        
        if (large.size() > small.size()) {
            small.offer(large.poll());
        }
    }
    
    public double findMedian() {
        if (small.size() > large.size()) {
            return small.peek();
        }
        return (small.peek() + large.peek()) / 2.0;
    }
    // end your solution
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int q = sc.nextInt();
        MedianFinder mf = new MedianFinder();
        
        for (int i = 0; i < q; i++) {
            String op = sc.next();
            
            if (op.equals("add")) {
                int num = sc.nextInt();
                mf.addNum(num);
            } else {
                System.out.printf("%.1f%n", mf.findMedian());
            }
        }
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq


class MedianFinder:
    def __init__(self):
        # start your solution
        
    
    def addNum(self, num: int) -> None:
        
        
    
    def findMedian(self) -> float:
        
        # end your solution


def main():
    q = int(input())
    mf = MedianFinder()
    
    for _ in range(q):
        line = input().split()
        if line[0] == "add":
            num = int(line[1])
            mf.addNum(num)
        else:
            result = mf.findMedian()
            print(f"{result:.1f}")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <queue>
#include <iomanip>
using namespace std;

class MedianFinder {
private:
    
    
public:
    // start your solution
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        
    }
    
    double findMedian() {
        
    }
    // end your solution
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int q;
    cin >> q;
    
    MedianFinder mf;
    
    for (int i = 0; i < q; i++) {
        string op;
        cin >> op;
        
        if (op == "add") {
            int num;
            cin >> num;
            mf.addNum(num);
        } else {
            cout << fixed << setprecision(1) << mf.findMedian() << endl;
        }
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class MedianFinder {
    // start your solution
    
    public MedianFinder() {
        
    }
    
    public void addNum(int num) {
        
    }
    
    public double findMedian() {
        
    }
    // end your solution
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int q = sc.nextInt();
        MedianFinder mf = new MedianFinder();
        
        for (int i = 0; i < q; i++) {
            String op = sc.next();
            
            if (op.equals("add")) {
                int num = sc.nextInt();
                mf.addNum(num);
            } else {
                System.out.printf("%.1f%n", mf.findMedian());
            }
        }
        
        sc.close();
    }
}
```