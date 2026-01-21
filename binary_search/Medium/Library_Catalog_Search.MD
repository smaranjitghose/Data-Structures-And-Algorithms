# Library Catalog Search

### Problem Statement

The National Library of India in Kolkata maintains a digital catalog organized as a 2D matrix. Each row contains book IDs sorted in ascending order, and the first book of each row has a larger ID than the last book of the previous row.

Given an `m x n` integer matrix `catalog` and an integer `bookId`, return `true` if `bookId` exists in the catalog, otherwise return `false`.

You must write an algorithm with O(log(m * n)) runtime complexity.

### Input Format

- The first line contains two integers `m` and `n`, the matrix dimensions.
- The next `m` lines each contain `n` space-separated integers.
- The last line contains the target `bookId`.

### Output Format

- Print `true` if bookId exists, otherwise `false`.

### Constraints

- `m == catalog.length`
- `n == catalog[i].length`
- `1 <= m, n <= 100`
- `-10^4 <= catalog[i][j], bookId <= 10^4`
- Each row is sorted in ascending order
- First integer of each row is greater than last integer of previous row

### Test Cases

#### Test Case 1
**Input:**
```
3 4
1 3 5 7
10 11 16 20
23 30 34 60
3
```
**Output:**
```
true
```
**Explanation:** BookId 3 found at row 0, column 1. Binary search on flattened matrix locates it.

---

#### Test Case 2
**Input:**
```
3 4
1 3 5 7
10 11 16 20
23 30 34 60
13
```
**Output:**
```
false
```
**Explanation:** BookId 13 not in catalog. Falls between row 1 and row 2, but doesn't exist.

---

#### Test Case 3
**Input:**
```
1 1
5
5
```
**Output:**
```
true
```
**Explanation:** Single element matrix. BookId 5 matches the only element.

---

#### Test Case 4
**Input:**
```
2 3
1 2 3
4 5 6
6
```
**Output:**
```
true
```
**Explanation:** BookId 6 at last position of matrix.

---

#### Test Case 5
**Input:**
```
2 3
1 2 3
4 5 6
0
```
**Output:**
```
false
```
**Explanation:** BookId 0 smaller than all elements. Not found.

---

#### Test Case 6
**Input:**
```
3 3
1 5 9
14 18 22
27 31 35
18
```
**Output:**
```
true
```
**Explanation:** BookId 18 found in middle row at column 1.

---

#### Test Case 7
**Input:**
```
4 4
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
11
```
**Output:**
```
true
```
**Explanation:** BookId 11 at row 2, column 2. Treat as flattened sorted array and binary search.

---

### Solutions

#### Python

```python
class Solution:
    def searchMatrix(self, catalog: list[list[int]], bookId: int) -> bool:
        # start your solution
        if not catalog or not catalog[0]:
            return False
        
        m, n = len(catalog), len(catalog[0])
        left, right = 0, m * n - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            row, col = mid // n, mid % n
            value = catalog[row][col]
            
            if value == bookId:
                return True
            elif value < bookId:
                left = mid + 1
            else:
                right = mid - 1
        
        return False
        # end your solution


def main():
    m, n = map(int, input().split())
    catalog = []
    for _ in range(m):
        row = list(map(int, input().split()))
        catalog.append(row)
    bookId = int(input())
    
    sol = Solution()
    result = sol.searchMatrix(catalog, bookId)
    print("true" if result else "false")


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
    bool searchMatrix(vector<vector<int>>& catalog, int bookId) {
        // start your solution
        if (catalog.empty() || catalog[0].empty()) return false;
        
        int m = catalog.size(), n = catalog[0].size();
        int left = 0, right = m * n - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            int row = mid / n, col = mid % n;
            int value = catalog[row][col];
            
            if (value == bookId) {
                return true;
            } else if (value < bookId) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return false;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<vector<int>> catalog(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> catalog[i][j];
        }
    }
    
    int bookId;
    cin >> bookId;
    
    Solution sol;
    cout << (sol.searchMatrix(catalog, bookId) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean searchMatrix(int[][] catalog, int bookId) {
        // start your solution
        if (catalog.length == 0 || catalog[0].length == 0) return false;
        
        int m = catalog.length, n = catalog[0].length;
        int left = 0, right = m * n - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            int row = mid / n, col = mid % n;
            int value = catalog[row][col];
            
            if (value == bookId) {
                return true;
            } else if (value < bookId) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return false;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[][] catalog = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                catalog[i][j] = sc.nextInt();
            }
        }
        
        int bookId = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.searchMatrix(catalog, bookId) ? "true" : "false");
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def searchMatrix(self, catalog: list[list[int]], bookId: int) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    m, n = map(int, input().split())
    catalog = []
    for _ in range(m):
        row = list(map(int, input().split()))
        catalog.append(row)
    bookId = int(input())
    
    sol = Solution()
    result = sol.searchMatrix(catalog, bookId)
    print("true" if result else "false")


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
    bool searchMatrix(vector<vector<int>>& catalog, int bookId) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<vector<int>> catalog(m, vector<int>(n));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cin >> catalog[i][j];
        }
    }
    
    int bookId;
    cin >> bookId;
    
    Solution sol;
    cout << (sol.searchMatrix(catalog, bookId) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean searchMatrix(int[][] catalog, int bookId) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[][] catalog = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                catalog[i][j] = sc.nextInt();
            }
        }
        
        int bookId = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.searchMatrix(catalog, bookId) ? "true" : "false");
        
        sc.close();
    }
}
```
