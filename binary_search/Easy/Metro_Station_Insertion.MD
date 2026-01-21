# Metro Station Insertion

### Problem Statement

The Delhi Metro Rail Corporation (DMRC) is planning to add a new station on the Blue Line. Stations are arranged by their distance (in km) from the starting terminal. Arjun needs to find where to insert the new station to maintain sorted order.

Given a sorted array of distinct integers `distances` and a target value `target`, return the index where the target is found. If not found, return the index where it would be inserted in order.

You must write an algorithm with O(log n) runtime complexity.

### Input Format

- The first line contains an integer `n`, the number of existing stations.
- The second line contains `n` space-separated sorted integers (distances in km).
- The third line contains the target distance.

### Output Format

- Print the index where target is found or should be inserted.

### Constraints

- `1 <= n <= 10^4`
- `-10^4 <= distances[i], target <= 10^4`
- `distances` contains distinct values sorted in ascending order

### Test Cases

#### Test Case 1
**Input:**
```
4
1 3 5 6
5
```
**Output:**
```
2
```
**Explanation:** Target 5 exists at index 2. Return 2.

---

#### Test Case 2
**Input:**
```
4
1 3 5 6
2
```
**Output:**
```
1
```
**Explanation:** Target 2 not found. Should be inserted between 1 and 3, at index 1.

---

#### Test Case 3
**Input:**
```
4
1 3 5 6
7
```
**Output:**
```
4
```
**Explanation:** Target 7 greater than all elements. Insert at end, index 4.

---

#### Test Case 4
**Input:**
```
4
1 3 5 6
0
```
**Output:**
```
0
```
**Explanation:** Target 0 smaller than all elements. Insert at beginning, index 0.

---

#### Test Case 5
**Input:**
```
1
5
5
```
**Output:**
```
0
```
**Explanation:** Single element equals target. Return index 0.

---

#### Test Case 6
**Input:**
```
5
2 4 6 8 10
7
```
**Output:**
```
3
```
**Explanation:** Target 7 between 6 (index 2) and 8 (index 3). Insert at index 3.

---

#### Test Case 7
**Input:**
```
6
5 10 15 20 25 30
15
```
**Output:**
```
2
```
**Explanation:** Target 15 found at index 2. Return 2.

---

### Solutions

#### Python

```python
class Solution:
    def searchInsert(self, distances: list[int], target: int) -> int:
        # start your solution
        left, right = 0, len(distances) - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            if distances[mid] == target:
                return mid
            elif distances[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        
        return left
        # end your solution


def main():
    n = int(input())
    distances = list(map(int, input().split()))
    target = int(input())
    
    sol = Solution()
    result = sol.searchInsert(distances, target)
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
    int searchInsert(vector<int>& distances, int target) {
        // start your solution
        int left = 0, right = distances.size() - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (distances[mid] == target) {
                return mid;
            } else if (distances[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
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
    
    vector<int> distances(n);
    for (int i = 0; i < n; i++) {
        cin >> distances[i];
    }
    
    int target;
    cin >> target;
    
    Solution sol;
    cout << sol.searchInsert(distances, target) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int searchInsert(int[] distances, int target) {
        // start your solution
        int left = 0, right = distances.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (distances[mid] == target) {
                return mid;
            } else if (distances[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
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
        int[] distances = new int[n];
        
        for (int i = 0; i < n; i++) {
            distances[i] = sc.nextInt();
        }
        
        int target = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.searchInsert(distances, target));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def searchInsert(self, distances: list[int], target: int) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    distances = list(map(int, input().split()))
    target = int(input())
    
    sol = Solution()
    result = sol.searchInsert(distances, target)
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
    int searchInsert(vector<int>& distances, int target) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> distances(n);
    for (int i = 0; i < n; i++) {
        cin >> distances[i];
    }
    
    int target;
    cin >> target;
    
    Solution sol;
    cout << sol.searchInsert(distances, target) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int searchInsert(int[] distances, int target) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] distances = new int[n];
        
        for (int i = 0; i < n; i++) {
            distances[i] = sc.nextInt();
        }
        
        int target = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.searchInsert(distances, target));
        
        sc.close();
    }
}
```
