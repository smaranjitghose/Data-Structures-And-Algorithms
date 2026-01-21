# Monsoon Temperature Wait

### Problem Statement

The India Meteorological Department (IMD) in Pune is analyzing monsoon data. For each day's temperature, farmers want to know how many days they must wait until a warmer day arrives. This helps plan agricultural activities.

Given an array `temperatures` representing daily temperatures, return an array where each element tells how many days you have to wait for a warmer temperature. If there is no future day with a warmer temperature, put 0.

### Input Format

- The first line contains an integer `n`, the number of days.
- The second line contains `n` space-separated integers representing temperatures.

### Output Format

- Print `n` space-separated integers representing wait days.

### Constraints

- `1 <= n <= 10^5`
- `30 <= temperatures[i] <= 100`

### Test Cases

#### Test Case 1
**Input:**
```
8
73 74 75 71 69 72 76 73
```
**Output:**
```
1 1 4 2 1 1 0 0
```
**Explanation:** Day 0 (73): Day 1 is warmer (74), wait=1. Day 2 (75): Day 6 is warmer (76), wait=4. Last two days have no warmer day ahead.

---

#### Test Case 2
**Input:**
```
4
30 40 50 60
```
**Output:**
```
1 1 1 0
```
**Explanation:** Strictly increasing. Each day waits 1 day except last.

---

#### Test Case 3
**Input:**
```
4
30 60 90 60
```
**Output:**
```
1 1 0 0
```
**Explanation:** Day 0→1 (wait 1), Day 1→2 (wait 1), Day 2 and 3 have no warmer day.

---

#### Test Case 4
**Input:**
```
5
50 50 50 50 50
```
**Output:**
```
0 0 0 0 0
```
**Explanation:** All same temperature. No day is strictly warmer than another.

---

#### Test Case 5
**Input:**
```
1
42
```
**Output:**
```
0
```
**Explanation:** Single day, no future day exists.

---

#### Test Case 6
**Input:**
```
6
35 34 33 32 31 40
```
**Output:**
```
5 4 3 2 1 0
```
**Explanation:** Decreasing then spike. All wait for day 5 (40°).

---

#### Test Case 7
**Input:**
```
7
40 35 32 37 38 33 45
```
**Output:**
```
6 2 1 1 2 1 0
```
**Explanation:** Various wait times based on next warmer day positions.

---

### Solutions

#### Python

```python
class Solution:
    def dailyTemperatures(self, temperatures: list[int]) -> list[int]:
        # start your solution
        n = len(temperatures)
        result = [0] * n
        stack = []  # stores indices
        
        for i in range(n):
            while stack and temperatures[i] > temperatures[stack[-1]]:
                prevIndex = stack.pop()
                result[prevIndex] = i - prevIndex
            stack.append(i)
        
        return result
        # end your solution


def main():
    n = int(input())
    temperatures = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.dailyTemperatures(temperatures)
    print(' '.join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        // start your solution
        int n = temperatures.size();
        vector<int> result(n, 0);
        stack<int> stk;  // stores indices
        
        for (int i = 0; i < n; i++) {
            while (!stk.empty() && temperatures[i] > temperatures[stk.top()]) {
                int prevIndex = stk.top();
                stk.pop();
                result[prevIndex] = i - prevIndex;
            }
            stk.push(i);
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> temperatures(n);
    for (int i = 0; i < n; i++) {
        cin >> temperatures[i];
    }
    
    Solution sol;
    vector<int> result = sol.dailyTemperatures(temperatures);
    
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
    public int[] dailyTemperatures(int[] temperatures) {
        // start your solution
        int n = temperatures.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();  // stores indices
        
        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prevIndex = stack.pop();
                result[prevIndex] = i - prevIndex;
            }
            stack.push(i);
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] temperatures = new int[n];
        
        for (int i = 0; i < n; i++) {
            temperatures[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.dailyTemperatures(temperatures);
        
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
class Solution:
    def dailyTemperatures(self, temperatures: list[int]) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    temperatures = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.dailyTemperatures(temperatures)
    print(' '.join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> temperatures(n);
    for (int i = 0; i < n; i++) {
        cin >> temperatures[i];
    }
    
    Solution sol;
    vector<int> result = sol.dailyTemperatures(temperatures);
    
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
    public int[] dailyTemperatures(int[] temperatures) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] temperatures = new int[n];
        
        for (int i = 0; i < n; i++) {
            temperatures[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.dailyTemperatures(temperatures);
        
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
