# Perfect Tile Fit

### Problem Statement

Lakshmi runs a tile shop in Jaipur. Customers often bring square tiles and want to know if the tile count can perfectly cover a square floor pattern without cutting any tiles.

Given a positive integer `tiles`, determine if it is a perfect square (i.e., can the tiles form a perfect square arrangement).

You must not use any built-in library function such as sqrt.

### Input Format

- A single positive integer `tiles`.

### Output Format

- Print `true` if tiles is a perfect square, otherwise print `false`.

### Constraints

- `1 <= tiles <= 2^31 - 1`

### Test Cases

#### Test Case 1
**Input:**
```
16
```
**Output:**
```
true
```
**Explanation:** 16 = 4 × 4. Perfect square. Tiles form a 4×4 arrangement.

---

#### Test Case 2
**Input:**
```
14
```
**Output:**
```
false
```
**Explanation:** 14 is not a perfect square. 3² = 9 < 14 < 16 = 4². No integer square root exists.

---

#### Test Case 3
**Input:**
```
1
```
**Output:**
```
true
```
**Explanation:** 1 = 1 × 1. Perfect square. Single tile forms 1×1 square.

---

#### Test Case 4
**Input:**
```
100
```
**Output:**
```
true
```
**Explanation:** 100 = 10 × 10. Perfect square for a 10×10 floor pattern.

---

#### Test Case 5
**Input:**
```
99
```
**Output:**
```
false
```
**Explanation:** 99 is not a perfect square. 9² = 81 < 99 < 100 = 10².

---

#### Test Case 6
**Input:**
```
2147483647
```
**Output:**
```
false
```
**Explanation:** Maximum 32-bit integer. 46340² = 2147395600 < 2147483647 < 46341². Not a perfect square.

---

#### Test Case 7
**Input:**
```
808201
```
**Output:**
```
true
```
**Explanation:** 808201 = 899 × 899. Perfect square. Binary search confirms 899² = 808201.

---

### Solutions

#### Python

```python
class Solution:
    def isPerfectSquare(self, tiles: int) -> bool:
        # start your solution
        if tiles < 2:
            return True
        
        left, right = 1, tiles // 2
        
        while left <= right:
            mid = left + (right - left) // 2
            square = mid * mid
            
            if square == tiles:
                return True
            elif square < tiles:
                left = mid + 1
            else:
                right = mid - 1
        
        return False
        # end your solution


def main():
    tiles = int(input())
    
    sol = Solution()
    result = sol.isPerfectSquare(tiles)
    print("true" if result else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
using namespace std;

class Solution {
public:
    bool isPerfectSquare(int tiles) {
        // start your solution
        if (tiles < 2) return true;
        
        long left = 1, right = tiles / 2;
        
        while (left <= right) {
            long mid = left + (right - left) / 2;
            long square = mid * mid;
            
            if (square == tiles) {
                return true;
            } else if (square < tiles) {
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
    
    int tiles;
    cin >> tiles;
    
    Solution sol;
    cout << (sol.isPerfectSquare(tiles) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean isPerfectSquare(int tiles) {
        // start your solution
        if (tiles < 2) return true;
        
        long left = 1, right = tiles / 2;
        
        while (left <= right) {
            long mid = left + (right - left) / 2;
            long square = mid * mid;
            
            if (square == tiles) {
                return true;
            } else if (square < tiles) {
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
        
        int tiles = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.isPerfectSquare(tiles) ? "true" : "false");
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def isPerfectSquare(self, tiles: int) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    tiles = int(input())
    
    sol = Solution()
    result = sol.isPerfectSquare(tiles)
    print("true" if result else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
using namespace std;

class Solution {
public:
    bool isPerfectSquare(int tiles) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int tiles;
    cin >> tiles;
    
    Solution sol;
    cout << (sol.isPerfectSquare(tiles) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean isPerfectSquare(int tiles) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int tiles = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.isPerfectSquare(tiles) ? "true" : "false");
        
        sc.close();
    }
}
```
