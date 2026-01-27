# Metro Line Survey Points

### Problem Statement

The Delhi Metro Rail Corporation (DMRC) is planning a new metro line extension. Survey teams have marked potential station locations on a 2D map with coordinates. To minimize construction costs, the planners want to find the maximum number of survey points that lie on a single straight line, as building stations along a straight corridor is most efficient.

Given an array of points where `points[i] = [xi, yi]` represents a survey point on the X-Y plane, return the maximum number of points that lie on the same straight line.

### Input Format

- First line contains the number of points `n`
- Next `n` lines each contain two space-separated integers representing x and y coordinates

### Output Format

- A single integer representing the maximum number of collinear points

### Constraints

- `1 <= n <= 300`
- `-10^4 <= xi, yi <= 10^4`
- All points are unique

### Test Cases

#### Test Case 1
**Input:**
```
3
1 1
2 2
3 3
```
**Output:**
```
3
```
**Explanation:** All three points lie on the line y = x.

---

#### Test Case 2
**Input:**
```
6
1 1
3 2
5 3
4 1
2 3
1 4
```
**Output:**
```
4
```
**Explanation:** Points (1,1), (3,2), (5,3) and one more lie on same line. Maximum is 4.

---

#### Test Case 3
**Input:**
```
1
0 0
```
**Output:**
```
1
```
**Explanation:** Single point is trivially on a line.

---

#### Test Case 4
**Input:**
```
2
1 1
2 2
```
**Output:**
```
2
```
**Explanation:** Two points always form a line.

---

#### Test Case 5
**Input:**
```
4
0 0
1 0
2 0
3 0
```
**Output:**
```
4
```
**Explanation:** All points on the x-axis (y = 0).

---

#### Test Case 6
**Input:**
```
4
0 0
0 1
0 2
0 3
```
**Output:**
```
4
```
**Explanation:** All points on the y-axis (x = 0).

---

#### Test Case 7
**Input:**
```
6
1 1
2 2
3 3
1 2
2 3
3 4
```
**Output:**
```
3
```
**Explanation:** (1,1), (2,2), (3,3) on one line, (1,2), (2,3), (3,4) on another. Max is 3.

---

### Solutions

#### Python
```python
from math import gcd


class Solution:
    def maxPoints(self, points: list[list[int]]) -> int:
        # start your solution
        if len(points) <= 2:
            return len(points)
        
        max_points = 0
        
        for i in range(len(points)):
            slope_count = {}
            
            for j in range(len(points)):
                if i == j:
                    continue
                
                dx = points[j][0] - points[i][0]
                dy = points[j][1] - points[i][1]
                
                g = gcd(dx, dy)
                dx //= g
                dy //= g
                
                if dx < 0:
                    dx, dy = -dx, -dy
                elif dx == 0:
                    dy = abs(dy)
                
                slope = (dx, dy)
                slope_count[slope] = slope_count.get(slope, 0) + 1
            
            if slope_count:
                max_points = max(max_points, max(slope_count.values()) + 1)
            else:
                max_points = max(max_points, 1)
        
        return max_points
        # end your solution


def main():
    n = int(input())
    
    points = []
    for _ in range(n):
        coords = list(map(int, input().split()))
        points.append(coords)
    
    sol = Solution()
    print(sol.maxPoints(points))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>
using namespace std;

class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        // start your solution
        if (points.size() <= 2) {
            return points.size();
        }
        
        int maxPoints = 0;
        
        for (int i = 0; i < points.size(); i++) {
            map<pair<int, int>, int> slopeCount;
            
            for (int j = 0; j < points.size(); j++) {
                if (i == j) continue;
                
                int dx = points[j][0] - points[i][0];
                int dy = points[j][1] - points[i][1];
                
                int g = __gcd(dx, dy);
                dx /= g;
                dy /= g;
                
                if (dx < 0) {
                    dx = -dx;
                    dy = -dy;
                } else if (dx == 0) {
                    dy = abs(dy);
                }
                
                slopeCount[{dx, dy}]++;
            }
            
            for (auto& [slope, count] : slopeCount) {
                maxPoints = max(maxPoints, count + 1);
            }
        }
        
        return maxPoints == 0 ? 1 : maxPoints;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<vector<int>> points(n, vector<int>(2));
    for (int i = 0; i < n; i++) {
        cin >> points[i][0] >> points[i][1];
    }
    
    Solution sol;
    cout << sol.maxPoints(points) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int maxPoints(int[][] points) {
        // start your solution
        if (points.length <= 2) {
            return points.length;
        }
        
        int maxPoints = 0;
        
        for (int i = 0; i < points.length; i++) {
            Map<String, Integer> slopeCount = new HashMap<>();
            
            for (int j = 0; j < points.length; j++) {
                if (i == j) continue;
                
                int dx = points[j][0] - points[i][0];
                int dy = points[j][1] - points[i][1];
                
                int g = gcd(dx, dy);
                dx /= g;
                dy /= g;
                
                if (dx < 0) {
                    dx = -dx;
                    dy = -dy;
                } else if (dx == 0) {
                    dy = Math.abs(dy);
                }
                
                String slope = dx + "," + dy;
                slopeCount.put(slope, slopeCount.getOrDefault(slope, 0) + 1);
            }
            
            for (int count : slopeCount.values()) {
                maxPoints = Math.max(maxPoints, count + 1);
            }
        }
        
        return maxPoints == 0 ? 1 : maxPoints;
    }
    
    private int gcd(int a, int b) {
        if (b == 0) return a;
        return gcd(b, a % b);
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[][] points = new int[n][2];
        for (int i = 0; i < n; i++) {
            points[i][0] = sc.nextInt();
            points[i][1] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.maxPoints(points));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
from math import gcd


class Solution:
    def maxPoints(self, points: list[list[int]]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    
    points = []
    for _ in range(n):
        coords = list(map(int, input().split()))
        points.append(coords)
    
    sol = Solution()
    print(sol.maxPoints(points))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>
using namespace std;

class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<vector<int>> points(n, vector<int>(2));
    for (int i = 0; i < n; i++) {
        cin >> points[i][0] >> points[i][1];
    }
    
    Solution sol;
    cout << sol.maxPoints(points) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int maxPoints(int[][] points) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[][] points = new int[n][2];
        for (int i = 0; i < n; i++) {
            points[i][0] = sc.nextInt();
            points[i][1] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.maxPoints(points));
        
        sc.close();
    }
}
```