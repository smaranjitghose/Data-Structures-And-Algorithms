# Continuous House Number Survey

### Problem Statement

A census officer in Jaipur is conducting a housing survey. The houses in an area don't have sequential numbering due to haphazard construction over the years. The officer has collected house numbers from a locality and wants to find the longest stretch of consecutive house numbers present in the survey data.

Given an unsorted array of integers representing house numbers, return the length of the longest sequence of consecutive house numbers. The sequence doesn't need to be contiguous in the array but must consist of consecutive integers.

Your algorithm must run in O(n) time complexity.

### Input Format

- First line contains the number of houses `n`
- Second line contains `n` space-separated integers representing house numbers

### Output Format

- A single integer representing the length of the longest consecutive sequence

### Constraints

- `0 <= n <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

### Test Cases

#### Test Case 1
**Input:**
```
6
100 4 200 1 3 2
```
**Output:**
```
4
```
**Explanation:** Longest consecutive sequence is [1,2,3,4], length 4.

---

#### Test Case 2
**Input:**
```
10
0 3 7 2 5 8 4 6 0 1
```
**Output:**
```
9
```
**Explanation:** Sequence [0,1,2,3,4,5,6,7,8] has length 9.

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
**Explanation:** Empty array, no sequence.

---

#### Test Case 4
**Input:**
```
1
5
```
**Output:**
```
1
```
**Explanation:** Single element forms sequence of length 1.

---

#### Test Case 5
**Input:**
```
5
1 1 1 1 1
```
**Output:**
```
1
```
**Explanation:** All duplicates, longest consecutive is just 1.

---

#### Test Case 6
**Input:**
```
7
10 5 12 3 55 30 11
```
**Output:**
```
3
```
**Explanation:** Sequence [10,11,12] has length 3.

---

#### Test Case 7
**Input:**
```
8
-5 -4 -3 0 1 2 3 4
```
**Output:**
```
5
```
**Explanation:** Sequence [0,1,2,3,4] has length 5.

---

### Solutions

#### Python
```python
class Solution:
    def longestConsecutive(self, nums: list[int]) -> int:
        # start your solution
        if not nums:
            return 0
        
        num_set = set(nums)
        max_length = 0
        
        for num in num_set:
            if num - 1 not in num_set:
                current_num = num
                current_length = 1
                
                while current_num + 1 in num_set:
                    current_num += 1
                    current_length += 1
                
                max_length = max(max_length, current_length)
        
        return max_length
        # end your solution


def main():
    n = int(input())
    
    if n == 0:
        input()  # consume empty line
        print(0)
        return
    
    nums = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.longestConsecutive(nums))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        // start your solution
        if (nums.empty()) {
            return 0;
        }
        
        unordered_set<int> numSet(nums.begin(), nums.end());
        int maxLength = 0;
        
        for (int num : numSet) {
            if (numSet.find(num - 1) == numSet.end()) {
                int currentNum = num;
                int currentLength = 1;
                
                while (numSet.find(currentNum + 1) != numSet.end()) {
                    currentNum++;
                    currentLength++;
                }
                
                maxLength = max(maxLength, currentLength);
            }
        }
        
        return maxLength;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    if (n == 0) {
        cout << 0 << endl;
        return 0;
    }
    
    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }
    
    Solution sol;
    cout << sol.longestConsecutive(nums) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int longestConsecutive(int[] nums) {
        // start your solution
        if (nums.length == 0) {
            return 0;
        }
        
        Set<Integer> numSet = new HashSet<>();
        for (int num : nums) {
            numSet.add(num);
        }
        
        int maxLength = 0;
        
        for (int num : numSet) {
            if (!numSet.contains(num - 1)) {
                int currentNum = num;
                int currentLength = 1;
                
                while (numSet.contains(currentNum + 1)) {
                    currentNum++;
                    currentLength++;
                }
                
                maxLength = Math.max(maxLength, currentLength);
            }
        }
        
        return maxLength;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        if (n == 0) {
            System.out.println(0);
            sc.close();
            return;
        }
        
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.longestConsecutive(nums));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def longestConsecutive(self, nums: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    
    if n == 0:
        input()  # consume empty line
        print(0)
        return
    
    nums = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.longestConsecutive(nums))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    if (n == 0) {
        cout << 0 << endl;
        return 0;
    }
    
    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }
    
    Solution sol;
    cout << sol.longestConsecutive(nums) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int longestConsecutive(int[] nums) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        if (n == 0) {
            System.out.println(0);
            sc.close();
            return;
        }
        
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.longestConsecutive(nums));
        
        sc.close();
    }
}
```