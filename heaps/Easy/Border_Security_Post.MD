# Border Security Post Ranking

### Problem Statement

The Border Security Force (BSF) monitors multiple outposts along the India-Pakistan border in Rajasthan. Each outpost has a row of positions that can be either manned (1) or unmanned (0). In each row, all manned positions appear before unmanned positions.

The strength of an outpost is defined by the number of manned positions. Headquarters wants to identify the `k` weakest outposts to prioritize reinforcement. An outpost `i` is weaker than outpost `j` if it has fewer manned positions, or if they have the same number of manned positions but `i` has a smaller index.

Given a binary matrix where each row represents an outpost, return the indices of the `k` weakest outposts ordered from weakest to strongest.

### Input Format

- First line contains three integers: `m` (rows), `n` (columns), and `k`
- Next `m` lines each contain `n` space-separated binary values (0 or 1)

### Output Format

- Print `k` space-separated integers representing indices of the k weakest rows

### Constraints

- `2 <= m, n <= 100`
- `1 <= k <= m`
- `matrix[i][j]` is either 0 or 1
- Each row is sorted in non-increasing order (1s before 0s)

### Test Cases

#### Test Case 1
**Input:**
```
5 5 3
1 1 0 0 0
1 1 1 1 0
1 0 0 0 0
1 1 0 0 0
1 1 1 1 1
```
**Output:**
```
2 0 3
```
**Explanation:** Strengths: [2,4,1,2,5]. Weakest is row 2 (strength 1), then rows 0 and 3 (both strength 2, but 0 < 3).

---

#### Test Case 2
**Input:**
```
4 4 2
1 0 0 0
1 1 1 1
1 1 0 0
1 1 1 0
```
**Output:**
```
0 2
```
**Explanation:** Strengths: [1,4,2,3]. Two weakest: row 0 (1), row 2 (2).

---

#### Test Case 3
**Input:**
```
3 3 3
1 1 1
1 1 1
1 1 1
```
**Output:**
```
0 1 2
```
**Explanation:** All equal strength, return by index order.

---

#### Test Case 4
**Input:**
```
4 3 2
0 0 0
1 0 0
1 1 0
1 1 1
```
**Output:**
```
0 1
```
**Explanation:** Strengths: [0,1,2,3]. Weakest: rows 0 and 1.

---

#### Test Case 5
**Input:**
```
3 4 1
1 1 1 1
1 1 0 0
1 0 0 0
```
**Output:**
```
2
```
**Explanation:** Row 2 has strength 1, which is the minimum.

---

#### Test Case 6
**Input:**
```
5 3 4
1 1 0
1 1 1
1 0 0
0 0 0
1 1 0
```
**Output:**
```
3 2 0 4
```
**Explanation:** Strengths: [2,3,1,0,2]. Sorted: row 3(0), row 2(1), row 0(2), row 4(2).

---

#### Test Case 7
**Input:**
```
2 5 2
1 1 1 1 1
0 0 0 0 0
```
**Output:**
```
1 0
```
**Explanation:** Row 1 has strength 0, row 0 has strength 5.

---

### Solutions

#### Python
```python
import heapq


class Solution:
    def kWeakestRows(self, mat: list[list[int]], k: int) -> list[int]:
        # start your solution
        max_heap = []
        
        for i, row in enumerate(mat):
            strength = sum(row)
            
            if len(max_heap) < k:
                heapq.heappush(max_heap, (-strength, -i))
            elif (-strength, -i) > max_heap[0]:
                heapq.heapreplace(max_heap, (-strength, -i))
        
        result = []
        while max_heap:
            _, idx = heapq.heappop(max_heap)
            result.append(-idx)
        
        return result[::-1]
        # end your solution


def main():
    first_line = input().split()
    m = int(first_line[0])
    n = int(first_line[1])
    k = int(first_line[2])
    
    mat = []
    for _ in range(m):
        row = list(map(int, input().split()))
        mat.append(row)
    
    sol = Solution()
    result = sol.kWeakestRows(mat, k)
    print(" ".join(map(str, result)))


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
    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
        // start your solution
        priority_queue<pair<int, int>> maxHeap;
        
        for (int i = 0; i < mat.size(); i++) {
            int strength = 0;
            for (int val : mat[i]) {
                strength += val;
            }
            
            if (maxHeap.size() < k) {
                maxHeap.push({strength, i});
            } else if (make_pair(strength, i) < maxHeap.top()) {
                maxHeap.pop();
                maxHeap.push({strength, i});
            }
        }
        
        vector<int> result;
        while (!maxHeap.empty()) {
            result.push_back(maxHeap.top().second);
            maxHeap.pop();
        }
        
        reverse(result.begin(), result.end());
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n, k;
    cin >> m >> n >> k;
    
    vector<vector<int>> mat(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> mat[i][j];
        }
    }
    
    Solution sol;
    vector<int> result = sol.kWeakestRows(mat, k);
    
    for (int i = 0; i < result.size(); i++) {
        if (i > 0) cout << " ";
        cout << result[i];
    }
    cout << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int[] kWeakestRows(int[][] mat, int k) {
        // start your solution
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> {
            if (a[0] != b[0]) return b[0] - a[0];
            return b[1] - a[1];
        });
        
        for (int i = 0; i < mat.length; i++) {
            int strength = 0;
            for (int val : mat[i]) {
                strength += val;
            }
            
            if (maxHeap.size() < k) {
                maxHeap.offer(new int[]{strength, i});
            } else if (strength < maxHeap.peek()[0] || 
                      (strength == maxHeap.peek()[0] && i < maxHeap.peek()[1])) {
                maxHeap.poll();
                maxHeap.offer(new int[]{strength, i});
            }
        }
        
        int[] result = new int[k];
        for (int i = k - 1; i >= 0; i--) {
            result[i] = maxHeap.poll()[1];
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[][] mat = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                mat[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        int[] result = sol.kWeakestRows(mat, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.length; i++) {
            if (i > 0) sb.append(" ");
            sb.append(result[i]);
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq


class Solution:
    def kWeakestRows(self, mat: list[list[int]], k: int) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    m = int(first_line[0])
    n = int(first_line[1])
    k = int(first_line[2])
    
    mat = []
    for _ in range(m):
        row = list(map(int, input().split()))
        mat.append(row)
    
    sol = Solution()
    result = sol.kWeakestRows(mat, k)
    print(" ".join(map(str, result)))


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
    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n, k;
    cin >> m >> n >> k;
    
    vector<vector<int>> mat(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> mat[i][j];
        }
    }
    
    Solution sol;
    vector<int> result = sol.kWeakestRows(mat, k);
    
    for (int i = 0; i < result.size(); i++) {
        if (i > 0) cout << " ";
        cout << result[i];
    }
    cout << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int[] kWeakestRows(int[][] mat, int k) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[][] mat = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                mat[i][j] = sc.nextInt();
            }
        }
        
        Solution sol = new Solution();
        int[] result = sol.kWeakestRows(mat, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.length; i++) {
            if (i > 0) sb.append(" ");
            sb.append(result[i]);
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```