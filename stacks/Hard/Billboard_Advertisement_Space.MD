# Billboard Advertisement Space

### Problem Statement

An advertising agency in Marine Drive, Mumbai is planning a massive billboard installation. The available wall sections have varying heights, and they want to find the largest rectangular advertisement that can fit across consecutive wall sections.

Given an array `heights` representing the height of each wall section (width of each section is 1 unit), find the area of the largest rectangle that can be formed within these sections.

### Input Format

- The first line contains an integer `n`, the number of wall sections.
- The second line contains `n` space-separated integers representing heights.

### Output Format

- Print the maximum rectangular area possible.

### Constraints

- `1 <= n <= 10^5`
- `0 <= heights[i] <= 10^4`

### Test Cases

#### Test Case 1
**Input:**
```
6
2 1 5 6 2 3
```
**Output:**
```
10
```
**Explanation:** Largest rectangle spans indices 2-3 (heights 5,6). Width=2, height=min(5,6)=5. Area=10.

---

#### Test Case 2
**Input:**
```
2
2 4
```
**Output:**
```
4
```
**Explanation:** Either single bar of height 4 (area=4) or both bars with height 2 (area=4). Maximum=4.

---

#### Test Case 3
**Input:**
```
1
5
```
**Output:**
```
5
```
**Explanation:** Single section. Area = 5 × 1 = 5.

---

#### Test Case 4
**Input:**
```
5
2 2 2 2 2
```
**Output:**
```
10
```
**Explanation:** All same height. Rectangle spans all 5 sections. Area = 2 × 5 = 10.

---

#### Test Case 5
**Input:**
```
5
1 2 3 4 5
```
**Output:**
```
9
```
**Explanation:** Best rectangle: indices 2-4 (heights 3,4,5), width=3, height=3. Area=9.

---

#### Test Case 6
**Input:**
```
5
5 4 3 2 1
```
**Output:**
```
9
```
**Explanation:** Best rectangle: indices 0-2 (heights 5,4,3), width=3, height=3. Area=9.

---

#### Test Case 7
**Input:**
```
6
2 4 6 5 3 1
```
**Output:**
```
12
```
**Explanation:** Best rectangle: indices 1-3 (heights 4,6,5), width=3, height=4. Area=12.

---

### Solutions

#### Python

```python
class Solution:
    def largestRectangleArea(self, heights: list[int]) -> int:
        # start your solution
        stack = []  # stores indices
        maxArea = 0
        n = len(heights)
        
        for i in range(n + 1):
            currHeight = heights[i] if i < n else 0
            
            while stack and heights[stack[-1]] > currHeight:
                height = heights[stack.pop()]
                width = i if not stack else i - stack[-1] - 1
                maxArea = max(maxArea, height * width)
            
            stack.append(i)
        
        return maxArea
        # end your solution


def main():
    n = int(input())
    heights = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.largestRectangleArea(heights)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        // start your solution
        stack<int> stk;  // stores indices
        int maxArea = 0;
        int n = heights.size();
        
        for (int i = 0; i <= n; i++) {
            int currHeight = (i < n) ? heights[i] : 0;
            
            while (!stk.empty() && heights[stk.top()] > currHeight) {
                int height = heights[stk.top()];
                stk.pop();
                int width = stk.empty() ? i : i - stk.top() - 1;
                maxArea = max(maxArea, height * width);
            }
            
            stk.push(i);
        }
        
        return maxArea;
        // end your solution
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
    cout << sol.largestRectangleArea(heights) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int largestRectangleArea(int[] heights) {
        // start your solution
        Stack<Integer> stack = new Stack<>();  // stores indices
        int maxArea = 0;
        int n = heights.length;
        
        for (int i = 0; i <= n; i++) {
            int currHeight = (i < n) ? heights[i] : 0;
            
            while (!stack.isEmpty() && heights[stack.peek()] > currHeight) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }
            
            stack.push(i);
        }
        
        return maxArea;
        // end your solution
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
        System.out.println(sol.largestRectangleArea(heights));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def largestRectangleArea(self, heights: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    heights = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.largestRectangleArea(heights)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        // start your solution
        
        
        
        // end your solution
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
    cout << sol.largestRectangleArea(heights) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int largestRectangleArea(int[] heights) {
        // start your solution
        
        
        
        // end your solution
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
        System.out.println(sol.largestRectangleArea(heights));
        
        sc.close();
    }
}
```
