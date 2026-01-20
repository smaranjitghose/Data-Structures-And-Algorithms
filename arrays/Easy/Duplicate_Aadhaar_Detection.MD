# Duplicate Aadhaar Detection

### Problem Statement

Meera works at an e-governance office in Pune. She's verifying a batch of Aadhaar registration requests to ensure no duplicate entries exist in the system.

Given an array `aadhaarNumbers` representing the submitted Aadhaar numbers, determine if any number appears more than once. Return `true` if duplicates exist, `false` otherwise.

### Input Format

- The first line contains an integer `n`, the number of Aadhaar entries.
- The second line contains `n` space-separated integers representing Aadhaar numbers.

### Output Format

- Print `true` if any Aadhaar number appears more than once, otherwise print `false`.

### Constraints

- `1 <= n <= 10^5`
- `-10^9 <= aadhaarNumbers[i] <= 10^9`

### Test Cases

#### Test Case 1
**Input:**
```
4
1 2 3 1
```
**Output:**
```
true
```
**Explanation:** The number 1 appears twice, so duplicates exist.

---

#### Test Case 2
**Input:**
```
4
1 2 3 4
```
**Output:**
```
false
```
**Explanation:** All numbers are unique, no duplicates.

---

#### Test Case 3
**Input:**
```
5
1 1 1 3 3
```
**Output:**
```
true
```
**Explanation:** Both 1 and 3 appear multiple times.

---

#### Test Case 4
**Input:**
```
1
100
```
**Output:**
```
false
```
**Explanation:** Only one entry, no duplicates possible.

---

#### Test Case 5
**Input:**
```
6
-1 -2 -1 3 4 5
```
**Output:**
```
true
```
**Explanation:** The number -1 appears twice.

---

#### Test Case 6
**Input:**
```
3
0 0 0
```
**Output:**
```
true
```
**Explanation:** All entries are the same, duplicates exist.

---

#### Test Case 7
**Input:**
```
5
999999999 -999999999 123456789 -123456789 999999999
```
**Output:**
```
true
```
**Explanation:** The number 999999999 appears twice at the boundary values.

---

### Solutions

#### Python

```python
class Solution:
    def hasDuplicate(self, aadhaarNumbers: list[int]) -> bool:
        # start your solution
        seen = set()
        for num in aadhaarNumbers:
            if num in seen:
                return True
            seen.add(num)
        return False
        # end your solution


def main():
    n = int(input())
    aadhaarNumbers = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.hasDuplicate(aadhaarNumbers)
    print("true" if result else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

class Solution {
public:
    bool hasDuplicate(vector<int>& aadhaarNumbers) {
        // start your solution
        unordered_set<int> seen;
        for (int num : aadhaarNumbers) {
            if (seen.find(num) != seen.end()) {
                return true;
            }
            seen.insert(num);
        }
        return false;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> aadhaarNumbers(n);
    for (int i = 0; i < n; i++) {
        cin >> aadhaarNumbers[i];
    }
    
    Solution sol;
    cout << (sol.hasDuplicate(aadhaarNumbers) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean hasDuplicate(int[] aadhaarNumbers) {
        // start your solution
        Set<Integer> seen = new HashSet<>();
        for (int num : aadhaarNumbers) {
            if (seen.contains(num)) {
                return true;
            }
            seen.add(num);
        }
        return false;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] aadhaarNumbers = new int[n];
        
        for (int i = 0; i < n; i++) {
            aadhaarNumbers[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.hasDuplicate(aadhaarNumbers) ? "true" : "false");
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def hasDuplicate(self, aadhaarNumbers: list[int]) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    aadhaarNumbers = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.hasDuplicate(aadhaarNumbers)
    print("true" if result else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

class Solution {
public:
    bool hasDuplicate(vector<int>& aadhaarNumbers) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> aadhaarNumbers(n);
    for (int i = 0; i < n; i++) {
        cin >> aadhaarNumbers[i];
    }
    
    Solution sol;
    cout << (sol.hasDuplicate(aadhaarNumbers) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean hasDuplicate(int[] aadhaarNumbers) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] aadhaarNumbers = new int[n];
        
        for (int i = 0; i < n; i++) {
            aadhaarNumbers[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.hasDuplicate(aadhaarNumbers) ? "true" : "false");
        
        sc.close();
    }
}
```
