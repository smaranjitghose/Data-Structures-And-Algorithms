# Four Vendor Balance Sheet

### Problem Statement

A chartered accountant in Ahmedabad is auditing four different vendors supplying to a large corporation. Each vendor has recorded their credit (+) and debit (-) transactions. The auditor needs to find how many ways she can pick exactly one transaction from each vendor such that the total sum is zero (balanced).

Given four integer arrays `nums1`, `nums2`, `nums3`, and `nums4`, all of length `n`, return the number of tuples `(i, j, k, l)` such that:
- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

### Input Format

- First line contains the integer `n` (size of each array)
- Second line contains `n` space-separated integers for nums1
- Third line contains `n` space-separated integers for nums2
- Fourth line contains `n` space-separated integers for nums3
- Fifth line contains `n` space-separated integers for nums4

### Output Format

- A single integer representing the count of tuples that sum to zero

### Constraints

- `1 <= n <= 200`
- `-2^28 <= nums1[i], nums2[j], nums3[k], nums4[l] <= 2^28`

### Test Cases

#### Test Case 1
**Input:**
```
2
1 2
-2 -1
-1 2
0 2
```
**Output:**
```
2
```
**Explanation:** Two tuples sum to 0:
- (0,0,0,1): 1 + (-2) + (-1) + 2 = 0
- (1,1,0,0): 2 + (-1) + (-1) + 0 = 0

---

#### Test Case 2
**Input:**
```
1
0
0
0
0
```
**Output:**
```
1
```
**Explanation:** Only one tuple (0,0,0,0), sum = 0.

---

#### Test Case 3
**Input:**
```
2
1 1
1 1
1 1
1 1
```
**Output:**
```
0
```
**Explanation:** All positive values, no way to get sum 0.

---

#### Test Case 4
**Input:**
```
3
1 -1 0
1 -1 0
1 -1 0
1 -1 0
```
**Output:**
```
19
```
**Explanation:** Multiple combinations of picking 1, -1, and 0 from each array sum to 0.

---

#### Test Case 5
**Input:**
```
2
0 0
0 0
0 0
0 0
```
**Output:**
```
16
```
**Explanation:** Any combination of indices gives sum 0. Total = 2^4 = 16.

---

#### Test Case 6
**Input:**
```
3
1 2 3
4 5 6
-7 -8 -9
0 0 0
```
**Output:**
```
3
```
**Explanation:** (0,0,0,any), (0,1,1,any) with right combinations.

---

#### Test Case 7
**Input:**
```
2
-1 1
-1 1
-1 1
-1 1
```
**Output:**
```
6
```
**Explanation:** Combinations where two +1 and two -1 are picked.

---

### Solutions

#### Python
```python
class Solution:
    def fourSumCount(self, nums1: list[int], nums2: list[int], nums3: list[int], nums4: list[int]) -> int:
        # start your solution
        sum_count = {}
        
        for a in nums1:
            for b in nums2:
                s = a + b
                sum_count[s] = sum_count.get(s, 0) + 1
        
        count = 0
        for c in nums3:
            for d in nums4:
                target = -(c + d)
                if target in sum_count:
                    count += sum_count[target]
        
        return count
        # end your solution


def main():
    n = int(input())
    nums1 = list(map(int, input().split()))
    nums2 = list(map(int, input().split()))
    nums3 = list(map(int, input().split()))
    nums4 = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.fourSumCount(nums1, nums2, nums3, nums4))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        // start your solution
        unordered_map<int, int> sumCount;
        
        for (int a : nums1) {
            for (int b : nums2) {
                sumCount[a + b]++;
            }
        }
        
        int count = 0;
        for (int c : nums3) {
            for (int d : nums4) {
                int target = -(c + d);
                if (sumCount.find(target) != sumCount.end()) {
                    count += sumCount[target];
                }
            }
        }
        
        return count;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> nums1(n), nums2(n), nums3(n), nums4(n);
    for (int i = 0; i < n; i++) cin >> nums1[i];
    for (int i = 0; i < n; i++) cin >> nums2[i];
    for (int i = 0; i < n; i++) cin >> nums3[i];
    for (int i = 0; i < n; i++) cin >> nums4[i];
    
    Solution sol;
    cout << sol.fourSumCount(nums1, nums2, nums3, nums4) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        // start your solution
        Map<Integer, Integer> sumCount = new HashMap<>();
        
        for (int a : nums1) {
            for (int b : nums2) {
                int s = a + b;
                sumCount.put(s, sumCount.getOrDefault(s, 0) + 1);
            }
        }
        
        int count = 0;
        for (int c : nums3) {
            for (int d : nums4) {
                int target = -(c + d);
                if (sumCount.containsKey(target)) {
                    count += sumCount.get(target);
                }
            }
        }
        
        return count;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[] nums1 = new int[n];
        int[] nums2 = new int[n];
        int[] nums3 = new int[n];
        int[] nums4 = new int[n];
        
        for (int i = 0; i < n; i++) nums1[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums2[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums3[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums4[i] = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.fourSumCount(nums1, nums2, nums3, nums4));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def fourSumCount(self, nums1: list[int], nums2: list[int], nums3: list[int], nums4: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    nums1 = list(map(int, input().split()))
    nums2 = list(map(int, input().split()))
    nums3 = list(map(int, input().split()))
    nums4 = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.fourSumCount(nums1, nums2, nums3, nums4))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> nums1(n), nums2(n), nums3(n), nums4(n);
    for (int i = 0; i < n; i++) cin >> nums1[i];
    for (int i = 0; i < n; i++) cin >> nums2[i];
    for (int i = 0; i < n; i++) cin >> nums3[i];
    for (int i = 0; i < n; i++) cin >> nums4[i];
    
    Solution sol;
    cout << sol.fourSumCount(nums1, nums2, nums3, nums4) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        int[] nums1 = new int[n];
        int[] nums2 = new int[n];
        int[] nums3 = new int[n];
        int[] nums4 = new int[n];
        
        for (int i = 0; i < n; i++) nums1[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums2[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums3[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums4[i] = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.fourSumCount(nums1, nums2, nums3, nums4));
        
        sc.close();
    }
}
```