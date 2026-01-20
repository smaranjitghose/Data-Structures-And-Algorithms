# Missing Railway PNR

### Problem Statement

Kavita works at the IRCTC office in Chennai. The system assigns PNR numbers starting from 1 in sequential order. Due to a server crash, some PNR records were corrupted and the data now contains duplicates and invalid entries.

Given an array `pnrList` of integers representing recovered PNR numbers (may contain duplicates, zeros, and negative numbers), find the smallest positive PNR number that is missing from the system.

Solve this in O(n) time using O(1) extra space.

### Input Format

- The first line contains an integer `n`, the number of recovered PNR entries.
- The second line contains `n` space-separated integers.

### Output Format

- Print a single integer — the smallest missing positive PNR number.

### Constraints

- `1 <= n <= 10^5`
- `-2^31 <= pnrList[i] <= 2^31 - 1`

### Test Cases

#### Test Case 1
**Input:**
```
3
1 2 0
```
**Output:**
```
3
```
**Explanation:** PNR 1 and 2 exist. The smallest missing positive is 3.

---

#### Test Case 2
**Input:**
```
4
3 4 -1 1
```
**Output:**
```
2
```
**Explanation:** PNR 1, 3, 4 exist. PNR 2 is missing.

---

#### Test Case 3
**Input:**
```
3
7 8 9
```
**Output:**
```
1
```
**Explanation:** No PNR from 1-6 exists. Smallest missing is 1.

---

#### Test Case 4
**Input:**
```
5
1 2 3 4 5
```
**Output:**
```
6
```
**Explanation:** All PNRs 1-5 exist. Next missing is 6.

---

#### Test Case 5
**Input:**
```
4
1 1 1 1
```
**Output:**
```
2
```
**Explanation:** Only PNR 1 exists (duplicates ignored). Missing is 2.

---

#### Test Case 6
**Input:**
```
5
-5 -10 0 -1 -2
```
**Output:**
```
1
```
**Explanation:** No positive PNRs exist. Smallest missing positive is 1.

---

#### Test Case 7
**Input:**
```
6
2 3 4 5 6 7
```
**Output:**
```
1
```
**Explanation:** PNR 1 is missing from the sequence.

---

### Solutions

#### Python

```python
class Solution:
    def missingPNR(self, pnrList: list[int]) -> int:
        # start your solution
        n = len(pnrList)
        
        for i in range(n):
            while 1 <= pnrList[i] <= n and pnrList[pnrList[i] - 1] != pnrList[i]:
                idx = pnrList[i] - 1
                pnrList[i], pnrList[idx] = pnrList[idx], pnrList[i]
        
        for i in range(n):
            if pnrList[i] != i + 1:
                return i + 1
        
        return n + 1
        # end your solution


def main():
    n = int(input())
    pnrList = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.missingPNR(pnrList)
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
    int missingPNR(vector<int>& pnrList) {
        // start your solution
        int n = pnrList.size();
        
        for (int i = 0; i < n; i++) {
            while (pnrList[i] >= 1 && pnrList[i] <= n && pnrList[pnrList[i] - 1] != pnrList[i]) {
                swap(pnrList[i], pnrList[pnrList[i] - 1]);
            }
        }
        
        for (int i = 0; i < n; i++) {
            if (pnrList[i] != i + 1) {
                return i + 1;
            }
        }
        
        return n + 1;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> pnrList(n);
    for (int i = 0; i < n; i++) {
        cin >> pnrList[i];
    }
    
    Solution sol;
    cout << sol.missingPNR(pnrList) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int missingPNR(int[] pnrList) {
        // start your solution
        int n = pnrList.length;
        
        for (int i = 0; i < n; i++) {
            while (pnrList[i] >= 1 && pnrList[i] <= n && pnrList[pnrList[i] - 1] != pnrList[i]) {
                int idx = pnrList[i] - 1;
                int temp = pnrList[i];
                pnrList[i] = pnrList[idx];
                pnrList[idx] = temp;
            }
        }
        
        for (int i = 0; i < n; i++) {
            if (pnrList[i] != i + 1) {
                return i + 1;
            }
        }
        
        return n + 1;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] pnrList = new int[n];
        
        for (int i = 0; i < n; i++) {
            pnrList[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.missingPNR(pnrList));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def missingPNR(self, pnrList: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    pnrList = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.missingPNR(pnrList)
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
    int missingPNR(vector<int>& pnrList) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> pnrList(n);
    for (int i = 0; i < n; i++) {
        cin >> pnrList[i];
    }
    
    Solution sol;
    cout << sol.missingPNR(pnrList) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int missingPNR(int[] pnrList) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] pnrList = new int[n];
        
        for (int i = 0; i < n; i++) {
            pnrList[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.missingPNR(pnrList));
        
        sc.close();
    }
}
```
