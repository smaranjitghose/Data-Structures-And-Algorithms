# Air Quality Monitor

### Problem Statement

The Central Pollution Control Board (CPCB) in Delhi monitors Air Quality Index (AQI) readings throughout the day. For public alerts, they need to report the maximum AQI within every k-hour sliding window.

Given an array `readings` representing hourly AQI values and an integer `k` representing the window size, return an array of maximum values for each sliding window.

### Input Format

- The first line contains two integers `n` and `k`, the number of readings and window size.
- The second line contains `n` space-separated integers representing AQI readings.

### Output Format

- Print the maximum values for each window as space-separated integers.

### Constraints

- `1 <= n <= 10^5`
- `1 <= k <= n`
- `-10^4 <= readings[i] <= 10^4`

### Test Cases

#### Test Case 1
**Input:**
```
8 3
1 3 -1 -3 5 3 6 7
```
**Output:**
```
3 3 5 5 6 7
```
**Explanation:** Window positions and maximums:
- [1 3 -1] -3 5 3 6 7 → max=3
- 1 [3 -1 -3] 5 3 6 7 → max=3
- 1 3 [-1 -3 5] 3 6 7 → max=5
- 1 3 -1 [-3 5 3] 6 7 → max=5
- 1 3 -1 -3 [5 3 6] 7 → max=6
- 1 3 -1 -3 5 [3 6 7] → max=7

---

#### Test Case 2
**Input:**
```
1 1
1
```
**Output:**
```
1
```
**Explanation:** Single element, single window. Maximum is 1.

---

#### Test Case 3
**Input:**
```
5 5
5 4 3 2 1
```
**Output:**
```
5
```
**Explanation:** Window covers entire array. Maximum is 5.

---

#### Test Case 4
**Input:**
```
5 1
1 2 3 4 5
```
**Output:**
```
1 2 3 4 5
```
**Explanation:** Window size 1. Each element is its own maximum.

---

#### Test Case 5
**Input:**
```
6 3
100 90 80 70 60 50
```
**Output:**
```
100 90 80 70
```
**Explanation:** Decreasing sequence. First element of each window is maximum.

---

#### Test Case 6
**Input:**
```
6 3
50 60 70 80 90 100
```
**Output:**
```
70 80 90 100
```
**Explanation:** Increasing sequence. Last element of each window is maximum.

---

#### Test Case 7
**Input:**
```
7 4
4 3 5 4 3 3 6
```
**Output:**
```
5 5 5 6
```
**Explanation:** Track maximum using monotonic deque as window slides.

---

### Solutions

#### Python

```python
from collections import deque

class Solution:
    def maxSlidingWindow(self, readings: list[int], k: int) -> list[int]:
        # start your solution
        result = []
        dq = deque()  # stores indices
        
        for i in range(len(readings)):
            # Remove indices outside current window
            while dq and dq[0] < i - k + 1:
                dq.popleft()
            
            # Remove smaller elements from back
            while dq and readings[dq[-1]] < readings[i]:
                dq.pop()
            
            dq.append(i)
            
            # Add to result once first window is complete
            if i >= k - 1:
                result.append(readings[dq[0]])
        
        return result
        # end your solution


def main():
    n, k = map(int, input().split())
    readings = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.maxSlidingWindow(readings, k)
    print(' '.join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <deque>
using namespace std;

class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& readings, int k) {
        // start your solution
        vector<int> result;
        deque<int> dq;  // stores indices
        
        for (int i = 0; i < readings.size(); i++) {
            // Remove indices outside current window
            while (!dq.empty() && dq.front() < i - k + 1) {
                dq.pop_front();
            }
            
            // Remove smaller elements from back
            while (!dq.empty() && readings[dq.back()] < readings[i]) {
                dq.pop_back();
            }
            
            dq.push_back(i);
            
            // Add to result once first window is complete
            if (i >= k - 1) {
                result.push_back(readings[dq.front()]);
            }
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> readings(n);
    for (int i = 0; i < n; i++) {
        cin >> readings[i];
    }
    
    Solution sol;
    vector<int> result = sol.maxSlidingWindow(readings, k);
    
    for (int i = 0; i < result.size(); i++) {
        cout << result[i];
        if (i < result.size() - 1) cout << " ";
    }
    cout << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] maxSlidingWindow(int[] readings, int k) {
        // start your solution
        int n = readings.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> dq = new ArrayDeque<>();  // stores indices
        
        for (int i = 0; i < n; i++) {
            // Remove indices outside current window
            while (!dq.isEmpty() && dq.peekFirst() < i - k + 1) {
                dq.pollFirst();
            }
            
            // Remove smaller elements from back
            while (!dq.isEmpty() && readings[dq.peekLast()] < readings[i]) {
                dq.pollLast();
            }
            
            dq.offerLast(i);
            
            // Add to result once first window is complete
            if (i >= k - 1) {
                result[i - k + 1] = readings[dq.peekFirst()];
            }
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[] readings = new int[n];
        for (int i = 0; i < n; i++) {
            readings[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.maxSlidingWindow(readings, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.length; i++) {
            sb.append(result[i]);
            if (i < result.length - 1) sb.append(" ");
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
from collections import deque

class Solution:
    def maxSlidingWindow(self, readings: list[int], k: int) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    n, k = map(int, input().split())
    readings = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.maxSlidingWindow(readings, k)
    print(' '.join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <deque>
using namespace std;

class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& readings, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> readings(n);
    for (int i = 0; i < n; i++) {
        cin >> readings[i];
    }
    
    Solution sol;
    vector<int> result = sol.maxSlidingWindow(readings, k);
    
    for (int i = 0; i < result.size(); i++) {
        cout << result[i];
        if (i < result.size() - 1) cout << " ";
    }
    cout << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] maxSlidingWindow(int[] readings, int k) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[] readings = new int[n];
        for (int i = 0; i < n; i++) {
            readings[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.maxSlidingWindow(readings, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.length; i++) {
            sb.append(result[i]);
            if (i < result.length - 1) sb.append(" ");
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```
