# Holi Water Tank

### Problem Statement

Arjun is organizing a Holi celebration in his colony in Jaipur. He has set up vertical boards of different heights in a row to create a temporary water tank for storing colored water.

Given an array `heights` where `heights[i]` represents the height of the `i-th` board, find two boards that together with the ground can hold the maximum amount of water.

Return the maximum water the tank can store. Note that the boards cannot be tilted.

### Input Format

- The first line contains an integer `n`, the number of boards.
- The second line contains `n` space-separated integers representing the heights of boards.

### Output Format

- Print a single integer — the maximum amount of water the tank can hold.

### Constraints

- `2 <= n <= 10^5`
- `0 <= heights[i] <= 10^4`

### Test Cases

#### Test Case 1
**Input:**
```
9
1 8 6 2 5 4 8 3 7
```
**Output:**
```
49
```
**Explanation:** Boards at index 1 (height 8) and index 8 (height 7) form the container. Width = 8 - 1 = 7, height = min(8, 7) = 7. Area = 7 × 7 = 49.

---

#### Test Case 2
**Input:**
```
2
1 1
```
**Output:**
```
1
```
**Explanation:** Only two boards available. Width = 1, height = min(1, 1) = 1. Area = 1 × 1 = 1.

---

#### Test Case 3
**Input:**
```
5
4 3 2 1 4
```
**Output:**
```
16
```
**Explanation:** Boards at index 0 and 4 (both height 4). Width = 4, height = 4. Area = 4 × 4 = 16.

---

#### Test Case 4
**Input:**
```
3
1 2 1
```
**Output:**
```
2
```
**Explanation:** Boards at index 0 and 2. Width = 2, height = min(1, 1) = 1. Area = 2 × 1 = 2.

---

#### Test Case 5
**Input:**
```
6
2 3 4 5 18 17
```
**Output:**
```
17
```
**Explanation:** Boards at index 4 (height 18) and index 5 (height 17). Width = 1, height = 17. Area = 17.

---

#### Test Case 6
**Input:**
```
4
10 10 10 10
```
**Output:**
```
30
```
**Explanation:** Boards at index 0 and 3. Width = 3, height = 10. Area = 30.

---

#### Test Case 7
**Input:**
```
8
1 2 3 4 5 6 7 8
```
**Output:**
```
16
```
**Explanation:** Boards at index 0 (height 1) and index 7 (height 8) give area = 7 × 1 = 7. Optimal is index 1 and 7: width = 6, height = 2, area = 12. Actually optimal is index 3 and 7: width = 4, height = 4, area = 16.

---

### Solutions

#### Python

```python
class Solution:
    def maxWater(self, heights: list[int]) -> int:
        # Start your solution here
        left, right = 0, len(heights) - 1
        max_area = 0
        
        while left < right:
            width = right - left
            height = min(heights[left], heights[right])
            max_area = max(max_area, width * height)
            
            if heights[left] < heights[right]:
                left += 1
            else:
                right -= 1
        
        return max_area
        # End your solution


def main():
    n = int(input())
    heights = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.maxWater(heights)
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
    int maxWater(vector<int>& heights) {
        // Start your solution here
        int left = 0, right = heights.size() - 1;
        int maxArea = 0;
        
        while (left < right) {
            int width = right - left;
            int height = min(heights[left], heights[right]);
            maxArea = max(maxArea, width * height);
            
            if (heights[left] < heights[right]) {
                left++;
            } else {
                right--;
            }
        }
        
        return maxArea;
        // End your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> heights(n);
    for (int i = 0; i < n; i++) {
        cin >> heights[i];
    }
    
    Solution sol;
    cout << sol.maxWater(heights) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int maxWater(int[] heights) {
        // Start your solution here
        int left = 0, right = heights.length - 1;
        int maxArea = 0;
        
        while (left < right) {
            int width = right - left;
            int height = Math.min(heights[left], heights[right]);
            maxArea = Math.max(maxArea, width * height);
            
            if (heights[left] < heights[right]) {
                left++;
            } else {
                right--;
            }
        }
        
        return maxArea;
        // End your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] heights = new int[n];
        
        for (int i = 0; i < n; i++) {
            heights[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.maxWater(heights));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def maxWater(self, heights: list[int]) -> int:
        # Start your solution here
        
        
        
        # End your solution
        pass


def main():
    n = int(input())
    heights = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.maxWater(heights)
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
    int maxWater(vector<int>& heights) {
        // Start your solution here
        
        
        
        // End your solution
        return 0;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> heights(n);
    for (int i = 0; i < n; i++) {
        cin >> heights[i];
    }
    
    Solution sol;
    cout << sol.maxWater(heights) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int maxWater(int[] heights) {
        // Start your solution here
        
        
        
        // End your solution
        return 0;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] heights = new int[n];
        
        for (int i = 0; i < n; i++) {
            heights[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.maxWater(heights));
        
        sc.close();
    }
}
```
