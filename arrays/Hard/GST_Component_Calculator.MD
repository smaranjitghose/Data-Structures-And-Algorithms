# GST Component Calculator

### Problem Statement

Meera works at the GST Network (GSTN) office in New Delhi. She's analyzing tax components where each business's tax liability depends on the product of all other businesses' turnover values, excluding its own.

Given an integer array `turnovers`, return an array `result` where `result[i]` equals the product of all elements in `turnovers` except `turnovers[i]`.

The solution must run in O(n) time and must not use division operation.

### Input Format

- The first line contains an integer `n`, the number of businesses.
- The second line contains `n` space-separated integers representing turnovers.

### Output Format

- Print `n` space-separated integers representing the product array.

### Constraints

- `2 <= n <= 10^5`
- `-30 <= turnovers[i] <= 30`
- The product of any prefix or suffix of `turnovers` fits in a 32-bit integer

### Test Cases

#### Test Case 1
**Input:**
```
4
1 2 3 4
```
**Output:**
```
24 12 8 6
```
**Explanation:** For index 0: 2×3×4=24. For index 1: 1×3×4=12. For index 2: 1×2×4=8. For index 3: 1×2×3=6.

---

#### Test Case 2
**Input:**
```
5
-1 1 0 -3 3
```
**Output:**
```
0 0 9 0 0
```
**Explanation:** Index 2 has 0, so all products except at index 2 become 0. At index 2: (-1)×1×(-3)×3=9.

---

#### Test Case 3
**Input:**
```
2
5 10
```
**Output:**
```
10 5
```
**Explanation:** Two elements. result[0]=10, result[1]=5. Each is the other element.

---

#### Test Case 4
**Input:**
```
4
2 2 2 2
```
**Output:**
```
8 8 8 8
```
**Explanation:** All elements same. Product of three 2s = 8 for each position.

---

#### Test Case 5
**Input:**
```
3
1 0 0
```
**Output:**
```
0 0 0
```
**Explanation:** Two zeros present. Every product includes at least one zero. All results are 0.

---

#### Test Case 6
**Input:**
```
5
3 5 2 6 4
```
**Output:**
```
240 144 360 120 180
```
**Explanation:** Index 0: 5×2×6×4=240. Index 1: 3×2×6×4=144. Index 2: 3×5×6×4=360. Index 3: 3×5×2×4=120. Index 4: 3×5×2×6=180.

---

#### Test Case 7
**Input:**
```
4
-2 -3 4 5
```
**Output:**
```
-60 -40 30 24
```
**Explanation:** Index 0: (-3)×4×5=-60. Index 1: (-2)×4×5=-40. Index 2: (-2)×(-3)×5=30. Index 3: (-2)×(-3)×4=24.

---

### Solutions

#### Python

```python
class Solution:
    def productExceptSelf(self, turnovers: list[int]) -> list[int]:
        # start your solution
        n = len(turnovers)
        result = [1] * n
        
        # Left pass: result[i] = product of all elements to the left
        left_product = 1
        for i in range(n):
            result[i] = left_product
            left_product *= turnovers[i]
        
        # Right pass: multiply by product of all elements to the right
        right_product = 1
        for i in range(n - 1, -1, -1):
            result[i] *= right_product
            right_product *= turnovers[i]
        
        return result
        # end your solution


def main():
    n = int(input())
    turnovers = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.productExceptSelf(turnovers)
    print(' '.join(map(str, result)))


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
    vector<int> productExceptSelf(vector<int>& turnovers) {
        // start your solution
        int n = turnovers.size();
        vector<int> result(n, 1);
        
        // Left pass
        int leftProduct = 1;
        for (int i = 0; i < n; i++) {
            result[i] = leftProduct;
            leftProduct *= turnovers[i];
        }
        
        // Right pass
        int rightProduct = 1;
        for (int i = n - 1; i >= 0; i--) {
            result[i] *= rightProduct;
            rightProduct *= turnovers[i];
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> turnovers(n);
    for (int i = 0; i < n; i++) {
        cin >> turnovers[i];
    }
    
    Solution sol;
    vector<int> result = sol.productExceptSelf(turnovers);
    
    for (int i = 0; i < n; i++) {
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
    public int[] productExceptSelf(int[] turnovers) {
        // start your solution
        int n = turnovers.length;
        int[] result = new int[n];
        Arrays.fill(result, 1);
        
        // Left pass
        int leftProduct = 1;
        for (int i = 0; i < n; i++) {
            result[i] = leftProduct;
            leftProduct *= turnovers[i];
        }
        
        // Right pass
        int rightProduct = 1;
        for (int i = n - 1; i >= 0; i--) {
            result[i] *= rightProduct;
            rightProduct *= turnovers[i];
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] turnovers = new int[n];
        
        for (int i = 0; i < n; i++) {
            turnovers[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.productExceptSelf(turnovers);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            if (i > 0) sb.append(" ");
            sb.append(result[i]);
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def productExceptSelf(self, turnovers: list[int]) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    turnovers = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.productExceptSelf(turnovers)
    print(' '.join(map(str, result)))


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
    vector<int> productExceptSelf(vector<int>& turnovers) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> turnovers(n);
    for (int i = 0; i < n; i++) {
        cin >> turnovers[i];
    }
    
    Solution sol;
    vector<int> result = sol.productExceptSelf(turnovers);
    
    for (int i = 0; i < n; i++) {
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
    public int[] productExceptSelf(int[] turnovers) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] turnovers = new int[n];
        
        for (int i = 0; i < n; i++) {
            turnovers[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.productExceptSelf(turnovers);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            if (i > 0) sb.append(" ");
            sb.append(result[i]);
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```
