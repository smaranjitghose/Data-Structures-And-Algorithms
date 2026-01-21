# Stock Market Peak

### Problem Statement

Nisha is an analyst at the Bombay Stock Exchange (BSE). She's analyzing a stock's price movements where a peak is defined as an element strictly greater than its neighbors.

Given an array `prices` where `prices[i] != prices[i+1]`, find a peak element and return its index. If multiple peaks exist, return the index of any one.

You must write an algorithm that runs in O(log n) time.

### Input Format

- The first line contains an integer `n`, the number of price points.
- The second line contains `n` space-separated integers.

### Output Format

- Print the index of any peak element.

### Constraints

- `1 <= n <= 1000`
- `-2^31 <= prices[i] <= 2^31 - 1`
- `prices[i] != prices[i + 1]` for all valid `i`
- `prices[-1] = prices[n] = -∞` (elements outside array are considered negative infinity)

### Test Cases

#### Test Case 1
**Input:**
```
3
1 2 3
```
**Output:**
```
2
```
**Explanation:** prices[2]=3 is a peak. It's greater than prices[1]=2 and right neighbor is -∞.

---

#### Test Case 2
**Input:**
```
6
1 2 3 1 5 6
```
**Output:**
```
2
```
**Explanation:** Index 2 (value 3) or index 5 (value 6) are peaks. Either answer is valid.

---

#### Test Case 3
**Input:**
```
1
10
```
**Output:**
```
0
```
**Explanation:** Single element. Both neighbors are -∞. Index 0 is a peak.

---

#### Test Case 4
**Input:**
```
4
4 3 2 1
```
**Output:**
```
0
```
**Explanation:** Decreasing sequence. First element is peak (left neighbor is -∞).

---

#### Test Case 5
**Input:**
```
5
1 2 1 3 5
```
**Output:**
```
1
```
**Explanation:** Index 1 (value 2) is a peak: 2 > 1 and 2 > 1. Index 4 (value 5) is also valid.

---

#### Test Case 6
**Input:**
```
4
1 3 2 4
```
**Output:**
```
1
```
**Explanation:** Index 1 (value 3) is a peak. Index 3 (value 4) is also a peak.

---

#### Test Case 7
**Input:**
```
7
1 4 3 6 5 8 7
```
**Output:**
```
1
```
**Explanation:** Multiple peaks at indices 1, 3, 5. Any is valid. Binary search finds one efficiently.

---

### Solutions

#### Python

```python
class Solution:
    def findPeakElement(self, prices: list[int]) -> int:
        # start your solution
        left, right = 0, len(prices) - 1
        
        while left < right:
            mid = left + (right - left) // 2
            
            if prices[mid] > prices[mid + 1]:
                right = mid
            else:
                left = mid + 1
        
        return left
        # end your solution


def main():
    n = int(input())
    prices = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.findPeakElement(prices)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    int findPeakElement(vector<int>& prices) {
        // start your solution
        int left = 0, right = prices.size() - 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            
            if (prices[mid] > prices[mid + 1]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return left;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> prices(n);
    for (int i = 0; i < n; i++) {
        cin >> prices[i];
    }
    
    Solution sol;
    cout << sol.findPeakElement(prices) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int findPeakElement(int[] prices) {
        // start your solution
        int left = 0, right = prices.length - 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            
            if (prices[mid] > prices[mid + 1]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return left;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] prices = new int[n];
        
        for (int i = 0; i < n; i++) {
            prices[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findPeakElement(prices));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def findPeakElement(self, prices: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    prices = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.findPeakElement(prices)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    int findPeakElement(vector<int>& prices) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> prices(n);
    for (int i = 0; i < n; i++) {
        cin >> prices[i];
    }
    
    Solution sol;
    cout << sol.findPeakElement(prices) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int findPeakElement(int[] prices) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] prices = new int[n];
        
        for (int i = 0; i < n; i++) {
            prices[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findPeakElement(prices));
        
        sc.close();
    }
}
```
