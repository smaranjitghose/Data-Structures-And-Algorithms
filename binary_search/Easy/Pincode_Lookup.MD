# Pincode Lookup

### Problem Statement

Kavitha works at India Post's sorting facility in Hyderabad. She has a sorted list of pincodes served by the facility and needs to quickly verify if a given pincode exists in the system.

Given a sorted array of integers `pincodes` and a target integer `target`, return the index of `target` if it exists, otherwise return -1.

You must write an algorithm with O(log n) runtime complexity.

### Input Format

- The first line contains an integer `n`, the number of pincodes.
- The second line contains `n` space-separated sorted integers.
- The third line contains the target pincode to search.

### Output Format

- Print the index of the target pincode (0-indexed), or -1 if not found.

### Constraints

- `1 <= n <= 10^4`
- `-10^4 <= pincodes[i], target <= 10^4`
- All integers in `pincodes` are unique
- `pincodes` is sorted in ascending order

### Test Cases

#### Test Case 1
**Input:**
```
6
500001 500032 500045 500072 500081 500096
500045
```
**Output:**
```
2
```
**Explanation:** Target 500045 found at index 2. Binary search: mid=500045, match found.

---

#### Test Case 2
**Input:**
```
6
500001 500032 500045 500072 500081 500096
500050
```
**Output:**
```
-1
```
**Explanation:** Target 500050 not in array. Binary search exhausts all possibilities, return -1.

---

#### Test Case 3
**Input:**
```
1
110001
```
**Output:**
```
-1
```
**Explanation:** Single element 110001 doesn't match target (missing in input, defaults to search). Array has one element, not equal to any search target.

---

#### Test Case 4
**Input:**
```
5
400001 400025 400050 400075 400099
400001
```
**Output:**
```
0
```
**Explanation:** Target at first position. Binary search finds it at index 0.

---

#### Test Case 5
**Input:**
```
5
400001 400025 400050 400075 400099
400099
```
**Output:**
```
4
```
**Explanation:** Target at last position. Binary search finds it at index 4.

---

#### Test Case 6
**Input:**
```
1
600001
```
**Output:**
```
0
```
**Explanation:** Single element array, target matches. Return index 0.

---

#### Test Case 7
**Input:**
```
8
110001 110010 110025 110044 110055 110062 110078 110085
110055
```
**Output:**
```
4
```
**Explanation:** Target 110055 at index 4. Binary search: compare with mid elements until found.

---

### Solutions

#### Python

```python
class Solution:
    def searchPincode(self, pincodes: list[int], target: int) -> int:
        # start your solution
        left, right = 0, len(pincodes) - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            if pincodes[mid] == target:
                return mid
            elif pincodes[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        
        return -1
        # end your solution


def main():
    n = int(input())
    pincodes = list(map(int, input().split()))
    target = int(input())
    
    sol = Solution()
    result = sol.searchPincode(pincodes, target)
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
    int searchPincode(vector<int>& pincodes, int target) {
        // start your solution
        int left = 0, right = pincodes.size() - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (pincodes[mid] == target) {
                return mid;
            } else if (pincodes[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> pincodes(n);
    for (int i = 0; i < n; i++) {
        cin >> pincodes[i];
    }
    
    int target;
    cin >> target;
    
    Solution sol;
    cout << sol.searchPincode(pincodes, target) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int searchPincode(int[] pincodes, int target) {
        // start your solution
        int left = 0, right = pincodes.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (pincodes[mid] == target) {
                return mid;
            } else if (pincodes[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] pincodes = new int[n];
        
        for (int i = 0; i < n; i++) {
            pincodes[i] = sc.nextInt();
        }
        
        int target = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.searchPincode(pincodes, target));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def searchPincode(self, pincodes: list[int], target: int) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    pincodes = list(map(int, input().split()))
    target = int(input())
    
    sol = Solution()
    result = sol.searchPincode(pincodes, target)
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
    int searchPincode(vector<int>& pincodes, int target) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> pincodes(n);
    for (int i = 0; i < n; i++) {
        cin >> pincodes[i];
    }
    
    int target;
    cin >> target;
    
    Solution sol;
    cout << sol.searchPincode(pincodes, target) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int searchPincode(int[] pincodes, int target) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] pincodes = new int[n];
        
        for (int i = 0; i < n; i++) {
            pincodes[i] = sc.nextInt();
        }
        
        int target = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.searchPincode(pincodes, target));
        
        sc.close();
    }
}
```
