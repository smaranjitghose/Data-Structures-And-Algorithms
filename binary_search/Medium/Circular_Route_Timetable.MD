# Circular Route Timetable

### Problem Statement

Vikram works at the Chennai Central railway station. The circular route trains have departure times stored in a rotated sorted array — the schedule was sorted but then rotated at some unknown pivot point.

Given a rotated sorted array `times` of distinct integers and a target departure `target`, return the index of target if it exists, otherwise return -1.

You must write an algorithm with O(log n) runtime complexity.

### Input Format

- The first line contains an integer `n`, the number of departure times.
- The second line contains `n` space-separated integers (rotated sorted).
- The third line contains the target time to search.

### Output Format

- Print the index of target, or -1 if not found.

### Constraints

- `1 <= n <= 5000`
- `-10^4 <= times[i], target <= 10^4`
- All values in `times` are unique
- `times` is a rotated sorted array

### Test Cases

#### Test Case 1
**Input:**
```
7
4 5 6 7 0 1 2
0
```
**Output:**
```
4
```
**Explanation:** Array rotated at index 4. Target 0 found at index 4. Binary search identifies sorted half and narrows down.

---

#### Test Case 2
**Input:**
```
7
4 5 6 7 0 1 2
3
```
**Output:**
```
-1
```
**Explanation:** Target 3 not in array. Binary search exhausts possibilities.

---

#### Test Case 3
**Input:**
```
1
1
0
```
**Output:**
```
-1
```
**Explanation:** Single element 1, target 0 not found.

---

#### Test Case 4
**Input:**
```
5
3 4 5 1 2
5
```
**Output:**
```
2
```
**Explanation:** Rotated at index 3. Target 5 at index 2.

---

#### Test Case 5
**Input:**
```
4
2 3 4 1
1
```
**Output:**
```
3
```
**Explanation:** Target 1 at last position (index 3).

---

#### Test Case 6
**Input:**
```
5
5 1 2 3 4
5
```
**Output:**
```
0
```
**Explanation:** Target 5 at first position. Rotated by 1 position.

---

#### Test Case 7
**Input:**
```
6
6 7 8 1 2 3
8
```
**Output:**
```
2
```
**Explanation:** Target 8 in the left sorted portion at index 2.

---

### Solutions

#### Python

```python
class Solution:
    def searchTime(self, times: list[int], target: int) -> int:
        # start your solution
        left, right = 0, len(times) - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            if times[mid] == target:
                return mid
            
            # Left half is sorted
            if times[left] <= times[mid]:
                if times[left] <= target < times[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            # Right half is sorted
            else:
                if times[mid] < target <= times[right]:
                    left = mid + 1
                else:
                    right = mid - 1
        
        return -1
        # end your solution


def main():
    n = int(input())
    times = list(map(int, input().split()))
    target = int(input())
    
    sol = Solution()
    result = sol.searchTime(times, target)
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
    int searchTime(vector<int>& times, int target) {
        // start your solution
        int left = 0, right = times.size() - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (times[mid] == target) {
                return mid;
            }
            
            // Left half is sorted
            if (times[left] <= times[mid]) {
                if (times[left] <= target && target < times[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
            // Right half is sorted
            else {
                if (times[mid] < target && target <= times[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
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
    
    vector<int> times(n);
    for (int i = 0; i < n; i++) {
        cin >> times[i];
    }
    
    int target;
    cin >> target;
    
    Solution sol;
    cout << sol.searchTime(times, target) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int searchTime(int[] times, int target) {
        // start your solution
        int left = 0, right = times.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (times[mid] == target) {
                return mid;
            }
            
            // Left half is sorted
            if (times[left] <= times[mid]) {
                if (times[left] <= target && target < times[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
            // Right half is sorted
            else {
                if (times[mid] < target && target <= times[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
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
        int[] times = new int[n];
        
        for (int i = 0; i < n; i++) {
            times[i] = sc.nextInt();
        }
        
        int target = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.searchTime(times, target));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def searchTime(self, times: list[int], target: int) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    times = list(map(int, input().split()))
    target = int(input())
    
    sol = Solution()
    result = sol.searchTime(times, target)
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
    int searchTime(vector<int>& times, int target) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> times(n);
    for (int i = 0; i < n; i++) {
        cin >> times[i];
    }
    
    int target;
    cin >> target;
    
    Solution sol;
    cout << sol.searchTime(times, target) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int searchTime(int[] times, int target) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] times = new int[n];
        
        for (int i = 0; i < n; i++) {
            times[i] = sc.nextInt();
        }
        
        int target = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.searchTime(times, target));
        
        sc.close();
    }
}
```
