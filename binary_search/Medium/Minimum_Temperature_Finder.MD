# Minimum Temperature Finder

### Problem Statement

The India Meteorological Department (IMD) in Pune records daily temperatures. Due to a data rotation error, a sorted temperature array got rotated at an unknown pivot. The system needs to find the minimum recorded temperature efficiently.

Given a rotated sorted array `temps` of unique elements, return the minimum element.

You must write an algorithm that runs in O(log n) time.

### Input Format

- The first line contains an integer `n`, the number of temperature readings.
- The second line contains `n` space-separated integers (rotated sorted temperatures).

### Output Format

- Print the minimum temperature.

### Constraints

- `n == temps.length`
- `1 <= n <= 5000`
- `-5000 <= temps[i] <= 5000`
- All values are unique
- `temps` is sorted and rotated between 1 and n times

### Test Cases

#### Test Case 1
**Input:**
```
5
3 4 5 1 2
```
**Output:**
```
1
```
**Explanation:** Original sorted: [1,2,3,4,5]. Rotated at index 3. Minimum is 1 at index 3.

---

#### Test Case 2
**Input:**
```
7
4 5 6 7 0 1 2
```
**Output:**
```
0
```
**Explanation:** Rotation pivot at index 4. Minimum element 0 is at the pivot point.

---

#### Test Case 3
**Input:**
```
5
11 13 15 17 19
```
**Output:**
```
11
```
**Explanation:** Array not rotated (or rotated n times). Minimum at index 0.

---

#### Test Case 4
**Input:**
```
1
25
```
**Output:**
```
25
```
**Explanation:** Single element is both minimum and maximum.

---

#### Test Case 5
**Input:**
```
4
2 3 4 1
```
**Output:**
```
1
```
**Explanation:** Minimum 1 at last position. Binary search finds rotation point.

---

#### Test Case 6
**Input:**
```
6
15 18 21 24 3 9
```
**Output:**
```
3
```
**Explanation:** Temperature dropped to 3 (minimum) at index 4.

---

#### Test Case 7
**Input:**
```
8
8 9 10 11 12 1 2 3
```
**Output:**
```
1
```
**Explanation:** Minimum 1 found at rotation point, index 5.

---

### Solutions

#### Python

```python
class Solution:
    def findMin(self, temps: list[int]) -> int:
        # start your solution
        left, right = 0, len(temps) - 1
        
        while left < right:
            mid = left + (right - left) // 2
            
            if temps[mid] > temps[right]:
                left = mid + 1
            else:
                right = mid
        
        return temps[left]
        # end your solution


def main():
    n = int(input())
    temps = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.findMin(temps)
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
    int findMin(vector<int>& temps) {
        // start your solution
        int left = 0, right = temps.size() - 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            
            if (temps[mid] > temps[right]) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        return temps[left];
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> temps(n);
    for (int i = 0; i < n; i++) {
        cin >> temps[i];
    }
    
    Solution sol;
    cout << sol.findMin(temps) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int findMin(int[] temps) {
        // start your solution
        int left = 0, right = temps.length - 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            
            if (temps[mid] > temps[right]) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        return temps[left];
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] temps = new int[n];
        
        for (int i = 0; i < n; i++) {
            temps[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findMin(temps));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def findMin(self, temps: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    temps = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.findMin(temps)
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
    int findMin(vector<int>& temps) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> temps(n);
    for (int i = 0; i < n; i++) {
        cin >> temps[i];
    }
    
    Solution sol;
    cout << sol.findMin(temps) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int findMin(int[] temps) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] temps = new int[n];
        
        for (int i = 0; i < n; i++) {
            temps[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findMin(temps));
        
        sc.close();
    }
}
```
