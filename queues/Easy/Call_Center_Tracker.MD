# Call Center Tracker

### Problem Statement

At Jio's customer support center in Navi Mumbai, managers need to track the number of calls received in the last 3000 milliseconds (3 seconds) for load balancing purposes.

Implement a `RecentCounter` class that counts recent requests within a certain time frame.

- `RecentCounter()` - Initializes the counter with zero recent requests
- `ping(t)` - Adds a new request at time `t` and returns the number of requests in the past 3000 milliseconds (including the new request). Requests at time `[t - 3000, t]` are counted.

### Input Format

- The first line contains an integer `n`, the number of ping operations.
- The next `n` lines each contain the timestamp for the ping operation.

### Output Format

- For each ping, print the count of requests in the time window.

### Constraints

- `1 <= t <= 10^9`
- Each test case will call ping with strictly increasing values of `t`
- At most `10^4` calls will be made to ping

### Test Cases

#### Test Case 1
**Input:**
```
4
1
100
3001
3002
```
**Output:**
```
1
2
3
3
```
**Explanation:** 
- ping(1): [1] → count=1
- ping(100): [1,100] → count=2
- ping(3001): [1,100,3001] → all within [1,3001] → count=3
- ping(3002): [1,100,3001,3002] → 1 is outside [2,3002] → count=3

---

#### Test Case 2
**Input:**
```
3
1
2
3
```
**Output:**
```
1
2
3
```
**Explanation:** All timestamps within 3000ms of each other.

---

#### Test Case 3
**Input:**
```
5
1000
2000
3000
4000
5000
```
**Output:**
```
1
2
3
4
4
```
**Explanation:** At 5000, window is [2000,5000]. Timestamp 1000 is excluded.

---

#### Test Case 4
**Input:**
```
1
5000
```
**Output:**
```
1
```
**Explanation:** Single call, count is 1.

---

#### Test Case 5
**Input:**
```
6
100
200
300
3100
3200
3300
```
**Output:**
```
1
2
3
4
5
6
```
**Explanation:** All calls within 3000ms sliding window at each point.

---

#### Test Case 6
**Input:**
```
4
1
3001
6001
9001
```
**Output:**
```
1
2
2
2
```
**Explanation:** Each new call pushes the oldest out of the 3000ms window.

---

#### Test Case 7
**Input:**
```
5
10
20
30
3050
6050
```
**Output:**
```
1
2
3
3
1
```
**Explanation:** At 3050: [10,20,30,3050] → [50,3050] valid → count=3. At 6050: only 6050 in window.

---

### Solutions

#### Python

```python
from collections import deque

class RecentCounter:
    # start your solution
    def __init__(self):
        self.requests = deque()

    def ping(self, t: int) -> int:
        self.requests.append(t)

        while self.requests[0] < t - 3000:
            self.requests.popleft()

        return len(self.requests)
    # end your solution



def main():
    n = int(input())
    counter = RecentCounter()
    
    for _ in range(n):
        t = int(input())
        print(counter.ping(t))


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <queue>
using namespace std;

class RecentCounter {
    // start your solution
private:
    queue<int> requests;

public:
    RecentCounter() {}

    int ping(int t) {
        requests.push(t);

        while (requests.front() < t - 3000) {
            requests.pop();
        }

        return requests.size();
    }
    // end your solution
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    RecentCounter counter;
    
    for (int i = 0; i < n; i++) {
        int t;
        cin >> t;
        cout << counter.ping(t) << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class RecentCounter {
    // start your solution
    private Queue<Integer> requests;

    public RecentCounter() {
        requests = new LinkedList<>();
    }

    public int ping(int t) {
        requests.offer(t);

        while (requests.peek() < t - 3000) {
            requests.poll();
        }

        return requests.size();
    }
    // end your solution
}


public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        RecentCounter counter = new RecentCounter();
        
        for (int i = 0; i < n; i++) {
            int t = sc.nextInt();
            System.out.println(counter.ping(t));
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

class RecentCounter:
    # start your solution
    def __init__(self):
        pass

    def ping(self, t: int) -> int:
        pass
    # end your solution



def main():
    n = int(input())
    counter = RecentCounter()
    
    for _ in range(n):
        t = int(input())
        print(counter.ping(t))


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <queue>
using namespace std;

class RecentCounter {
    // start your solution
public:
    RecentCounter() {}

    int ping(int t) {}
    // end your solution
};


int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    RecentCounter counter;
    
    for (int i = 0; i < n; i++) {
        int t;
        cin >> t;
        cout << counter.ping(t) << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class RecentCounter {
    // start your solution
    public RecentCounter() {}

    public int ping(int t) {}
    // end your solution
}


public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        RecentCounter counter = new RecentCounter();
        
        for (int i = 0; i < n; i++) {
            int t = sc.nextInt();
            System.out.println(counter.ping(t));
        }
        
        sc.close();
    }
}
```
