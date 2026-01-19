# JEE Rank Median

### Problem Statement

The National Testing Agency (NTA) conducts JEE Main in two sessions each year. After both sessions, they need to merge the percentile scores to determine the overall median performance.

Given two sorted arrays `session1` and `session2` representing percentile scores from each session, find the median of the combined scores.

The solution must run in O(log(m+n)) time complexity.

### Input Format

- The first line contains two integers `m` and `n` — sizes of the two arrays.
- The second line contains `m` space-separated integers (sorted) for session 1.
- The third line contains `n` space-separated integers (sorted) for session 2.

### Output Format

- Print the median as a decimal number with one decimal place.

### Constraints

- `0 <= m, n <= 1000`
- `1 <= m + n <= 2000`
- `-10^6 <= session1[i], session2[i] <= 10^6`

### Test Cases

#### Test Case 1
**Input:**
```
2 1
1 3
2
```
**Output:**
```
2.0
```
**Explanation:** Merged array = [1, 2, 3]. Median = 2.0.

---

#### Test Case 2
**Input:**
```
2 2
1 2
3 4
```
**Output:**
```
2.5
```
**Explanation:** Merged array = [1, 2, 3, 4]. Median = (2 + 3) / 2 = 2.5.

---

#### Test Case 3
**Input:**
```
3 3
1 3 5
2 4 6
```
**Output:**
```
3.5
```
**Explanation:** Merged = [1, 2, 3, 4, 5, 6]. Median = (3 + 4) / 2 = 3.5.

---

#### Test Case 4
**Input:**
```
0 5
 
1 2 3 4 5
```
**Output:**
```
3.0
```
**Explanation:** Only session 2 has scores. Median of [1, 2, 3, 4, 5] = 3.0.

---

#### Test Case 5
**Input:**
```
1 1
1
2
```
**Output:**
```
1.5
```
**Explanation:** Merged = [1, 2]. Median = (1 + 2) / 2 = 1.5.

---

#### Test Case 6
**Input:**
```
4 4
10 20 30 40
15 25 35 45
```
**Output:**
```
27.5
```
**Explanation:** Merged = [10, 15, 20, 25, 30, 35, 40, 45]. Median = (25 + 30) / 2 = 27.5.

---

#### Test Case 7
**Input:**
```
5 5
1 1 1 1 1
2 2 2 2 2
```
**Output:**
```
1.5
```
**Explanation:** Merged = [1, 1, 1, 1, 1, 2, 2, 2, 2, 2]. Median = (1 + 2) / 2 = 1.5.

---

### Solutions

#### Python

```python
class Solution:
    def findMedian(self, session1: list[int], session2: list[int]) -> float:
        # Start your solution here
        if len(session1) > len(session2):
            session1, session2 = session2, session1
        
        m, n = len(session1), len(session2)
        low, high = 0, m
        
        while low <= high:
            cut1 = (low + high) // 2
            cut2 = (m + n + 1) // 2 - cut1
            
            left1 = float('-inf') if cut1 == 0 else session1[cut1 - 1]
            left2 = float('-inf') if cut2 == 0 else session2[cut2 - 1]
            right1 = float('inf') if cut1 == m else session1[cut1]
            right2 = float('inf') if cut2 == n else session2[cut2]
            
            if left1 <= right2 and left2 <= right1:
                if (m + n) % 2 == 0:
                    return (max(left1, left2) + min(right1, right2)) / 2
                else:
                    return max(left1, left2)
            elif left1 > right2:
                high = cut1 - 1
            else:
                low = cut1 + 1
        
        return 0.0
        # End your solution


def main():
    first_line = input().split()
    m, n = int(first_line[0]), int(first_line[1])
    
    session1 = list(map(int, input().split())) if m > 0 else []
    session2 = list(map(int, input().split())) if n > 0 else []
    
    sol = Solution()
    result = sol.findMedian(session1, session2)
    print(f"{result:.1f}")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <climits>
#include <algorithm>
#include <iomanip>
using namespace std;

class Solution {
public:
    double findMedian(vector<int>& session1, vector<int>& session2) {
        // Start your solution here
        if (session1.size() > session2.size()) {
            swap(session1, session2);
        }
        
        int m = session1.size(), n = session2.size();
        int low = 0, high = m;
        
        while (low <= high) {
            int cut1 = (low + high) / 2;
            int cut2 = (m + n + 1) / 2 - cut1;
            
            int left1 = (cut1 == 0) ? INT_MIN : session1[cut1 - 1];
            int left2 = (cut2 == 0) ? INT_MIN : session2[cut2 - 1];
            int right1 = (cut1 == m) ? INT_MAX : session1[cut1];
            int right2 = (cut2 == n) ? INT_MAX : session2[cut2];
            
            if (left1 <= right2 && left2 <= right1) {
                if ((m + n) % 2 == 0) {
                    return (max(left1, left2) + min(right1, right2)) / 2.0;
                } else {
                    return max(left1, left2);
                }
            } else if (left1 > right2) {
                high = cut1 - 1;
            } else {
                low = cut1 + 1;
            }
        }
        
        return 0.0;
        // End your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<int> session1(m), session2(n);
    for (int i = 0; i < m; i++) cin >> session1[i];
    for (int i = 0; i < n; i++) cin >> session2[i];
    
    Solution sol;
    cout << fixed << setprecision(1) << sol.findMedian(session1, session2) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public double findMedian(int[] session1, int[] session2) {
        // Start your solution here
        if (session1.length > session2.length) {
            int[] temp = session1;
            session1 = session2;
            session2 = temp;
        }
        
        int m = session1.length, n = session2.length;
        int low = 0, high = m;
        
        while (low <= high) {
            int cut1 = (low + high) / 2;
            int cut2 = (m + n + 1) / 2 - cut1;
            
            int left1 = (cut1 == 0) ? Integer.MIN_VALUE : session1[cut1 - 1];
            int left2 = (cut2 == 0) ? Integer.MIN_VALUE : session2[cut2 - 1];
            int right1 = (cut1 == m) ? Integer.MAX_VALUE : session1[cut1];
            int right2 = (cut2 == n) ? Integer.MAX_VALUE : session2[cut2];
            
            if (left1 <= right2 && left2 <= right1) {
                if ((m + n) % 2 == 0) {
                    return (Math.max(left1, left2) + Math.min(right1, right2)) / 2.0;
                } else {
                    return Math.max(left1, left2);
                }
            } else if (left1 > right2) {
                high = cut1 - 1;
            } else {
                low = cut1 + 1;
            }
        }
        
        return 0.0;
        // End your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[] session1 = new int[m];
        int[] session2 = new int[n];
        
        for (int i = 0; i < m; i++) session1[i] = sc.nextInt();
        for (int i = 0; i < n; i++) session2[i] = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.printf("%.1f%n", sol.findMedian(session1, session2));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def findMedian(self, session1: list[int], session2: list[int]) -> float:
        # Start your solution here
        
        
        
        # End your solution
        pass


def main():
    first_line = input().split()
    m, n = int(first_line[0]), int(first_line[1])
    
    session1 = list(map(int, input().split())) if m > 0 else []
    session2 = list(map(int, input().split())) if n > 0 else []
    
    sol = Solution()
    result = sol.findMedian(session1, session2)
    print(f"{result:.1f}")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <climits>
#include <algorithm>
#include <iomanip>
using namespace std;

class Solution {
public:
    double findMedian(vector<int>& session1, vector<int>& session2) {
        // Start your solution here
        
        
        
        // End your solution
        return 0.0;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<int> session1(m), session2(n);
    for (int i = 0; i < m; i++) cin >> session1[i];
    for (int i = 0; i < n; i++) cin >> session2[i];
    
    Solution sol;
    cout << fixed << setprecision(1) << sol.findMedian(session1, session2) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public double findMedian(int[] session1, int[] session2) {
        // Start your solution here
        
        
        
        // End your solution
        return 0.0;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[] session1 = new int[m];
        int[] session2 = new int[n];
        
        for (int i = 0; i < m; i++) session1[i] = sc.nextInt();
        for (int i = 0; i < n; i++) session2[i] = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.printf("%.1f%n", sol.findMedian(session1, session2));
        
        sc.close();
    }
}
```
