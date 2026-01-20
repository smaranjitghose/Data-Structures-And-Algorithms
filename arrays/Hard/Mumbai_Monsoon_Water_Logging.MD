# Mumbai Monsoon Water Logging

### Problem Statement

Rahul is an urban planner at BMC (Brihanmumbai Municipal Corporation). During monsoon season, several areas in Mumbai face severe water logging due to uneven road elevations.

Given an array `elevation` representing the height of road segments in meters, calculate how much rainwater gets trapped between the segments after heavy rainfall.

### Input Format

- The first line contains an integer `n`, the number of road segments.
- The second line contains `n` space-separated non-negative integers representing elevations.

### Output Format

- Print a single integer — the total units of trapped rainwater.

### Constraints

- `1 <= n <= 2 * 10^4`
- `0 <= elevation[i] <= 10^5`

### Test Cases

#### Test Case 1
**Input:**
```
12
0 1 0 2 1 0 1 3 2 1 2 1
```
**Output:**
```
6
```
**Explanation:** Water fills the gaps between elevations. Total trapped = 6 units.

---

#### Test Case 2
**Input:**
```
6
4 2 0 3 2 5
```
**Output:**
```
9
```
**Explanation:** Water trapped at indices 1, 2, 3, 4 sums to 9 units.

---

#### Test Case 3
**Input:**
```
3
1 2 3
```
**Output:**
```
0
```
**Explanation:** Strictly increasing elevation, no water trapped.

---

#### Test Case 4
**Input:**
```
3
3 2 1
```
**Output:**
```
0
```
**Explanation:** Strictly decreasing elevation, no water trapped.

---

#### Test Case 5
**Input:**
```
5
5 0 0 0 5
```
**Output:**
```
15
```
**Explanation:** Deep valley between two peaks. Water = 5 * 3 = 15 units.

---

#### Test Case 6
**Input:**
```
1
7
```
**Output:**
```
0
```
**Explanation:** Single segment, no water can be trapped.

---

#### Test Case 7
**Input:**
```
8
3 0 2 0 4 0 2 0
```
**Output:**
```
10
```
**Explanation:** Multiple valleys trap water at various points totaling 10 units.

---

### Solutions

#### Python

```python
class Solution:
    def trappedWater(self, elevation: list[int]) -> int:
        # start your solution
        if not elevation:
            return 0
        
        left, right = 0, len(elevation) - 1
        left_max, right_max = elevation[left], elevation[right]
        water = 0
        
        while left < right:
            if left_max < right_max:
                left += 1
                left_max = max(left_max, elevation[left])
                water += left_max - elevation[left]
            else:
                right -= 1
                right_max = max(right_max, elevation[right])
                water += right_max - elevation[right]
        
        return water
        # end your solution


def main():
    n = int(input())
    elevation = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.trappedWater(elevation)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int trappedWater(vector<int>& elevation) {
        // start your solution
        if (elevation.empty()) return 0;
        
        int left = 0, right = elevation.size() - 1;
        int leftMax = elevation[left], rightMax = elevation[right];
        int water = 0;
        
        while (left < right) {
            if (leftMax < rightMax) {
                left++;
                leftMax = max(leftMax, elevation[left]);
                water += leftMax - elevation[left];
            } else {
                right--;
                rightMax = max(rightMax, elevation[right]);
                water += rightMax - elevation[right];
            }
        }
        
        return water;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> elevation(n);
    for (int i = 0; i < n; i++) {
        cin >> elevation[i];
    }
    
    Solution sol;
    cout << sol.trappedWater(elevation) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int trappedWater(int[] elevation) {
        // start your solution
        if (elevation.length == 0) return 0;
        
        int left = 0, right = elevation.length - 1;
        int leftMax = elevation[left], rightMax = elevation[right];
        int water = 0;
        
        while (left < right) {
            if (leftMax < rightMax) {
                left++;
                leftMax = Math.max(leftMax, elevation[left]);
                water += leftMax - elevation[left];
            } else {
                right--;
                rightMax = Math.max(rightMax, elevation[right]);
                water += rightMax - elevation[right];
            }
        }
        
        return water;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] elevation = new int[n];
        
        for (int i = 0; i < n; i++) {
            elevation[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.trappedWater(elevation));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def trappedWater(self, elevation: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    elevation = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.trappedWater(elevation)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int trappedWater(vector<int>& elevation) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> elevation(n);
    for (int i = 0; i < n; i++) {
        cin >> elevation[i];
    }
    
    Solution sol;
    cout << sol.trappedWater(elevation) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int trappedWater(int[] elevation) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] elevation = new int[n];
        
        for (int i = 0; i < n; i++) {
            elevation[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.trappedWater(elevation));
        
        sc.close();
    }
}
```
