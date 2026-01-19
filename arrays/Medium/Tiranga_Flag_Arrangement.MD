# Tiranga Flag Arrangement

### Problem Statement

Neha is a volunteer at a Republic Day parade in New Delhi. She has a row of flags in random order, each colored saffron (0), white (1), or green (2) — the colors of the Indian Tiranga.

Given an array `flags` containing only 0s, 1s, and 2s, sort them in-place so that saffron flags come first, followed by white, then green — matching the Tiranga order.

Solve this in one pass using O(1) extra space.

### Input Format

- The first line contains an integer `n`, the number of flags.
- The second line contains `n` space-separated integers (0, 1, or 2).

### Output Format

- Print the sorted array as space-separated integers.

### Constraints

- `1 <= n <= 10^5`
- `flags[i]` is either 0, 1, or 2

### Test Cases

#### Test Case 1
**Input:**
```
6
2 0 2 1 1 0
```
**Output:**
```
0 0 1 1 2 2
```
**Explanation:** Saffron (0) flags first, then white (1), then green (2).

---

#### Test Case 2
**Input:**
```
3
2 0 1
```
**Output:**
```
0 1 2
```
**Explanation:** One flag of each color, arranged in Tiranga order.

---

#### Test Case 3
**Input:**
```
5
0 0 0 0 0
```
**Output:**
```
0 0 0 0 0
```
**Explanation:** All saffron flags, already sorted.

---

#### Test Case 4
**Input:**
```
4
1 1 1 1
```
**Output:**
```
1 1 1 1
```
**Explanation:** All white flags, already sorted.

---

#### Test Case 5
**Input:**
```
1
2
```
**Output:**
```
2
```
**Explanation:** Single green flag.

---

#### Test Case 6
**Input:**
```
9
2 2 2 1 1 1 0 0 0
```
**Output:**
```
0 0 0 1 1 1 2 2 2
```
**Explanation:** Reverse order input, sorted to Tiranga order.

---

#### Test Case 7
**Input:**
```
7
0 2 1 0 2 1 0
```
**Output:**
```
0 0 0 1 1 2 2
```
**Explanation:** Mixed input sorted to Tiranga order.

---

### Solutions

#### Python

```python
class Solution:
    def arrangeTiranga(self, flags: list[int]) -> None:
        # Start your solution here
        low, mid, high = 0, 0, len(flags) - 1
        
        while mid <= high:
            if flags[mid] == 0:
                flags[low], flags[mid] = flags[mid], flags[low]
                low += 1
                mid += 1
            elif flags[mid] == 1:
                mid += 1
            else:
                flags[mid], flags[high] = flags[high], flags[mid]
                high -= 1
        # End your solution


def main():
    n = int(input())
    flags = list(map(int, input().split()))
    
    sol = Solution()
    sol.arrangeTiranga(flags)
    print(' '.join(map(str, flags)))


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
    void arrangeTiranga(vector<int>& flags) {
        // Start your solution here
        int low = 0, mid = 0, high = flags.size() - 1;
        
        while (mid <= high) {
            if (flags[mid] == 0) {
                swap(flags[low], flags[mid]);
                low++;
                mid++;
            } else if (flags[mid] == 1) {
                mid++;
            } else {
                swap(flags[mid], flags[high]);
                high--;
            }
        }
        // End your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> flags(n);
    for (int i = 0; i < n; i++) {
        cin >> flags[i];
    }
    
    Solution sol;
    sol.arrangeTiranga(flags);
    
    for (int i = 0; i < n; i++) {
        cout << flags[i];
        if (i < n - 1) cout << " ";
    }
    cout << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public void arrangeTiranga(int[] flags) {
        // Start your solution here
        int low = 0, mid = 0, high = flags.length - 1;
        
        while (mid <= high) {
            if (flags[mid] == 0) {
                int temp = flags[low];
                flags[low] = flags[mid];
                flags[mid] = temp;
                low++;
                mid++;
            } else if (flags[mid] == 1) {
                mid++;
            } else {
                int temp = flags[mid];
                flags[mid] = flags[high];
                flags[high] = temp;
                high--;
            }
        }
        // End your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] flags = new int[n];
        
        for (int i = 0; i < n; i++) {
            flags[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        sol.arrangeTiranga(flags);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            sb.append(flags[i]);
            if (i < n - 1) sb.append(" ");
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
    def arrangeTiranga(self, flags: list[int]) -> None:
        # Start your solution here
        
        
        
        # End your solution


def main():
    n = int(input())
    flags = list(map(int, input().split()))
    
    sol = Solution()
    sol.arrangeTiranga(flags)
    print(' '.join(map(str, flags)))


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
    void arrangeTiranga(vector<int>& flags) {
        // Start your solution here
        
        
        
        // End your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> flags(n);
    for (int i = 0; i < n; i++) {
        cin >> flags[i];
    }
    
    Solution sol;
    sol.arrangeTiranga(flags);
    
    for (int i = 0; i < n; i++) {
        cout << flags[i];
        if (i < n - 1) cout << " ";
    }
    cout << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public void arrangeTiranga(int[] flags) {
        // Start your solution here
        
        
        
        // End your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] flags = new int[n];
        
        for (int i = 0; i < n; i++) {
            flags[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        sol.arrangeTiranga(flags);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            sb.append(flags[i]);
            if (i < n - 1) sb.append(" ");
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```
