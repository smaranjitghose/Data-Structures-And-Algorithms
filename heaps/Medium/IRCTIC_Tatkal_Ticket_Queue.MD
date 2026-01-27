# IRCTC Tatkal Ticket Queue

### Problem Statement

The IRCTC Tatkal booking system processes ticket requests stored in a matrix format. Each row represents requests from a regional server, and each column represents a time slot. The matrix is sorted such that each row is sorted in ascending order (left to right), and each column is also sorted in ascending order (top to bottom).

During high-demand periods, the system needs to find the kth smallest priority ticket request to process it next. Given this sorted matrix and an integer k, return the kth smallest element in the matrix.

Note: The kth smallest element is in the sorted order, not the kth distinct element.

### Input Format

- First line contains two integers: `n` (matrix dimension n×n) and `k`
- Next `n` lines each contain `n` space-separated integers representing the matrix

### Output Format

- A single integer representing the kth smallest element

### Constraints

- `1 <= n <= 300`
- `-10^9 <= matrix[i][j] <= 10^9`
- Each row is sorted in ascending order
- Each column is sorted in ascending order
- `1 <= k <= n^2`

### Test Cases

#### Test Case 1
**Input:**
```
3 8
1 5 9
10 11 13
12 13 15
```
**Output:**
```
13
```
**Explanation:** Sorted elements: [1,5,9,10,11,12,13,13,15]. The 8th smallest is 13.

---

#### Test Case 2
**Input:**
```
2 2
-5 -4
-3 -2
```
**Output:**
```
-4
```
**Explanation:** Sorted: [-5,-4,-3,-2]. 2nd smallest is -4.

---

#### Test Case 3
**Input:**
```
1 1
5
```
**Output:**
```
5
```
**Explanation:** Single element matrix, only answer is 5.

---

#### Test Case 4
**Input:**
```
3 1
1 2 3
4 5 6
7 8 9
```
**Output:**
```
1
```
**Explanation:** 1st smallest (minimum) is 1.

---

#### Test Case 5
**Input:**
```
3 9
1 2 3
4 5 6
7 8 9
```
**Output:**
```
9
```
**Explanation:** 9th smallest (maximum) is 9.

---

#### Test Case 6
**Input:**
```
4 7
1 1 3 5
1 2 4 7
2 4 6 8
3 5 7 9
```
**Output:**
```
3
```
**Explanation:** Sorted with duplicates: [1,1,1,2,2,3,3,4,4,5,5,6,7,7,8,9]. 7th is 3.

---

#### Test Case 7
**Input:**
```
3 5
10 20 30
15 25 35
24 29 37
```
**Output:**
```
24
```
**Explanation:** Sorted: [10,15,20,24,25,29,30,35,37]. 5th smallest is 24.

---

### Solutions

#### Python
```python
import heapq


class Solution:
    def kthSmallest(self, matrix: list[list[int]], k: int) -> int:
        # start your solution
        n = len(matrix)
        min_heap = []
        
        for i in range(min(n, k)):
            heapq.heappush(min_heap, (matrix[i][0], i, 0))
        
        result = 0
        for _ in range(k):
            result, row, col = heapq.heappop(min_heap)
            
            if col + 1 < n:
                heapq.heappush(min_heap, (matrix[row][col + 1], row, col + 1))
        
        return result
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    matrix = []
    for _ in range(n):
        row = list(map(int, input().split()))
        matrix.append(row)
    
    sol = Solution()
    print(sol.kthSmallest(matrix, k))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        // start your solution
        int n = matrix.size();
        
        auto cmp = [](const tuple<int, int, int>& a, const tuple<int, int, int>& b) {
            return get<0>(a) > get<0>(b);
        };
        priority_queue<tuple<int, int, int>, vector<tuple<int, int, int>>, decltype(cmp)> minHeap(cmp);
        
        for (int i = 0; i < min(n, k); i++) {
            minHeap.push({matrix[i][0], i, 0});
        }
        
        int result = 0;
        for (int i = 0; i < k; i++) {
            auto [val, row, col] = minHeap.top();
            minHeap.pop();
            result = val;
            
            if (col + 1 < n) {
                minHeap.push({matrix[row][col + 1], row, col + 1});
            }
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<vector<int>> matrix(n, vector<int>(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> matrix[i][j];
        }
    }
    
    Solution sol;
    cout << sol.kthSmallest(matrix, k) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        // start your solution
        int n = matrix.length;
        
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        
        for (int i = 0; i < Math.min(n, k); i++) {
            minHeap.offer(new int[]{matrix[i][0], i, 0});
        }
        
        int result = 0;
        for (int i = 0; i < k; i++) {
            int[] curr = minHeap.poll();
            result = curr[0];
            int row = curr[1];
            int col = curr[2];
            
            if (col + 1 < n) {
                minHeap.offer(new int[]{matrix[row][col + 1], row, col + 1});
            }
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[][] matrix = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.kthSmallest(matrix, k));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq


class Solution:
    def kthSmallest(self, matrix: list[list[int]], k: int) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    matrix = []
    for _ in range(n):
        row = list(map(int, input().split()))
        matrix.append(row)
    
    sol = Solution()
    print(sol.kthSmallest(matrix, k))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<vector<int>> matrix(n, vector<int>(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> matrix[i][j];
        }
    }
    
    Solution sol;
    cout << sol.kthSmallest(matrix, k) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[][] matrix = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        System.out.println(sol.kthSmallest(matrix, k));
        
        sc.close();
    }
}
```