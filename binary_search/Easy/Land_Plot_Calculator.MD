# Land Plot Calculator

### Problem Statement

Gopal is a patwari (land records officer) in a village near Nagpur. Farmers often have square plots of land and know the total area. Gopal needs to calculate the side length of the square plot.

Given a non-negative integer `area` representing the area in square meters, compute and return the square root of `area` rounded down to the nearest integer.

You must not use any built-in exponent function or operator.

### Input Format

- A single integer `area`.

### Output Format

- Print the integer square root (floor value).

### Constraints

- `0 <= area <= 2^31 - 1`

### Test Cases

#### Test Case 1
**Input:**
```
4
```
**Output:**
```
2
```
**Explanation:** √4 = 2. Perfect square, exact answer.

---

#### Test Case 2
**Input:**
```
8
```
**Output:**
```
2
```
**Explanation:** √8 ≈ 2.828. Floor value = 2. The side length is 2m (ignoring the fractional part).

---

#### Test Case 3
**Input:**
```
0
```
**Output:**
```
0
```
**Explanation:** √0 = 0. Zero area means zero side length.

---

#### Test Case 4
**Input:**
```
1
```
**Output:**
```
1
```
**Explanation:** √1 = 1. Smallest positive perfect square.

---

#### Test Case 5
**Input:**
```
100
```
**Output:**
```
10
```
**Explanation:** √100 = 10. Perfect square, exact answer.

---

#### Test Case 6
**Input:**
```
2147395600
```
**Output:**
```
46340
```
**Explanation:** Large area near integer limit. √2147395600 = 46340 exactly.

---

#### Test Case 7
**Input:**
```
99
```
**Output:**
```
9
```
**Explanation:** √99 ≈ 9.95. Floor value = 9. Binary search finds largest n where n² ≤ 99.

---

### Solutions

#### Python

```python
class Solution:
    def mySqrt(self, area: int) -> int:
        # start your solution
        if area < 2:
            return area
        
        left, right = 1, area // 2
        
        while left <= right:
            mid = left + (right - left) // 2
            square = mid * mid
            
            if square == area:
                return mid
            elif square < area:
                left = mid + 1
            else:
                right = mid - 1
        
        return right
        # end your solution


def main():
    area = int(input())
    
    sol = Solution()
    result = sol.mySqrt(area)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
using namespace std;

class Solution {
public:
    int mySqrt(int area) {
        // start your solution
        if (area < 2) return area;
        
        long left = 1, right = area / 2;
        
        while (left <= right) {
            long mid = left + (right - left) / 2;
            long square = mid * mid;
            
            if (square == area) {
                return mid;
            } else if (square < area) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return right;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int area;
    cin >> area;
    
    Solution sol;
    cout << sol.mySqrt(area) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int mySqrt(int area) {
        // start your solution
        if (area < 2) return area;
        
        long left = 1, right = area / 2;
        
        while (left <= right) {
            long mid = left + (right - left) / 2;
            long square = mid * mid;
            
            if (square == area) {
                return (int)mid;
            } else if (square < area) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return (int)right;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int area = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.mySqrt(area));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def mySqrt(self, area: int) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    area = int(input())
    
    sol = Solution()
    result = sol.mySqrt(area)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
using namespace std;

class Solution {
public:
    int mySqrt(int area) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int area;
    cin >> area;
    
    Solution sol;
    cout << sol.mySqrt(area) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int mySqrt(int area) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int area = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.mySqrt(area));
        
        sc.close();
    }
}
```
