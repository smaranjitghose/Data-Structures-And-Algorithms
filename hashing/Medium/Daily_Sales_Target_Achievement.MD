# Daily Sales Target Achievement

### Problem Statement

A BigBazaar store manager in Kolkata tracks daily sales figures and wants to find how many consecutive day periods achieved exactly the monthly bonus target. The manager needs to count all possible continuous periods (subarrays) where the total sales equals the target amount.

Given an array of integers representing daily sales (can include returns as negative values) and an integer `k` representing the target sum, return the total number of continuous subarrays whose sum equals `k`.

### Input Format

- First line contains two integers: `n` (number of days) and `k` (target sum)
- Second line contains `n` space-separated integers representing daily sales

### Output Format

- A single integer representing the count of subarrays with sum equal to k

### Constraints

- `1 <= n <= 2 * 10^4`
- `-1000 <= nums[i] <= 1000`
- `-10^7 <= k <= 10^7`

### Test Cases

#### Test Case 1
**Input:**
```
3 2
1 1 1
```
**Output:**
```
2
```
**Explanation:** Subarrays [1,1] at indices (0,1) and (1,2) sum to 2.

---

#### Test Case 2
**Input:**
```
3 3
1 2 3
```
**Output:**
```
2
```
**Explanation:** [1,2] and [3] both sum to 3.

---

#### Test Case 3
**Input:**
```
5 0
1 -1 1 -1 1
```
**Output:**
```
4
```
**Explanation:** Subarrays summing to 0: [1,-1], [-1,1], [1,-1,1,-1], [1,-1] at different positions.

---

#### Test Case 4
**Input:**
```
4 5
2 3 2 3
```
**Output:**
```
2
```
**Explanation:** [2,3] appears twice (indices 0-1 and 2-3).

---

#### Test Case 5
**Input:**
```
5 10
1 2 3 4 5
```
**Output:**
```
1
```
**Explanation:** Only [1,2,3,4] sums to 10.

---

#### Test Case 6
**Input:**
```
3 100
1 2 3
```
**Output:**
```
0
```
**Explanation:** No subarray sums to 100.

---

#### Test Case 7
**Input:**
```
6 6
3 3 3 3 3 3
```
**Output:**
```
5
```
**Explanation:** Five subarrays of [3,3] sum to 6.

---

### Solutions

#### Python
```python
class Solution:
    def subarraySum(self, nums: list[int], k: int) -> int:
        # start your solution
        count = 0
        prefix_sum = 0
        prefix_count = {0: 1}
        
        for num in nums:
            prefix_sum += num
            
            if prefix_sum - k in prefix_count:
                count += prefix_count[prefix_sum - k]
            
            prefix_count[prefix_sum] = prefix_count.get(prefix_sum, 0) + 1
        
        return count
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    nums = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.subarraySum(nums, k))


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
    int subarraySum(vector<int>& nums, int k) {
        // start your solution
        int count = 0;
        int prefixSum = 0;
        unordered_map<int, int> prefixCount;
        prefixCount[0] = 1;
        
        for (int num : nums) {
            prefixSum += num;
            
            if (prefixCount.find(prefixSum - k) != prefixCount.end()) {
                count += prefixCount[prefixSum - k];
            }
            
            prefixCount[prefixSum]++;
        }
        
        return count;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }
    
    Solution sol;
    cout << sol.subarraySum(nums, k) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int subarraySum(int[] nums, int k) {
        // start your solution
        int count = 0;
        int prefixSum = 0;
        Map<Integer, Integer> prefixCount = new HashMap<>();
        prefixCount.put(0, 1);
        
        for (int num : nums) {
            prefixSum += num;
            
            if (prefixCount.containsKey(prefixSum - k)) {
                count += prefixCount.get(prefixSum - k);
            }
            
            prefixCount.put(prefixSum, prefixCount.getOrDefault(prefixSum, 0) + 1);
        }
        
        return count;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.subarraySum(nums, k));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def subarraySum(self, nums: list[int], k: int) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    nums = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.subarraySum(nums, k))


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
    int subarraySum(vector<int>& nums, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }
    
    Solution sol;
    cout << sol.subarraySum(nums, k) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int subarraySum(int[] nums, int k) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.subarraySum(nums, k));
        
        sc.close();
    }
}
```