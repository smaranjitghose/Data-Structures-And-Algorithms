# Election Vote Range

### Problem Statement

During Lok Sabha elections, the Election Commission of India in New Delhi processes sorted vote records. Each candidate's votes are recorded consecutively. Given a sorted array of candidate IDs, find the starting and ending position of votes for a specific candidate.

Given a sorted array `votes` and a target candidate ID `target`, return the starting and ending positions (0-indexed). If target is not found, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

### Input Format

- The first line contains an integer `n`, the number of votes.
- The second line contains `n` space-separated sorted integers (candidate IDs).
- The third line contains the target candidate ID.

### Output Format

- Print two space-separated integers: starting and ending positions.

### Constraints

- `0 <= n <= 10^5`
- `-10^9 <= votes[i], target <= 10^9`
- `votes` is sorted in non-decreasing order

### Test Cases

#### Test Case 1
**Input:**
```
6
5 7 7 8 8 10
8
```
**Output:**
```
3 4
```
**Explanation:** Candidate 8 received votes at indices 3 and 4. First occurrence at 3, last at 4.

---

#### Test Case 2
**Input:**
```
6
5 7 7 8 8 10
6
```
**Output:**
```
-1 -1
```
**Explanation:** Candidate 6 has no votes in the record.

---

#### Test Case 3
**Input:**
```
0

0
```
**Output:**
```
-1 -1
```
**Explanation:** Empty vote array. No candidates found.

---

#### Test Case 4
**Input:**
```
5
1 1 1 1 1
1
```
**Output:**
```
0 4
```
**Explanation:** All votes for candidate 1. Range is entire array [0, 4].

---

#### Test Case 5
**Input:**
```
5
1 2 3 4 5
3
```
**Output:**
```
2 2
```
**Explanation:** Candidate 3 appears once at index 2. Start and end are same.

---

#### Test Case 6
**Input:**
```
8
1 2 2 2 3 3 4 5
2
```
**Output:**
```
1 3
```
**Explanation:** Candidate 2's votes span from index 1 to 3.

---

#### Test Case 7
**Input:**
```
7
1 1 2 2 2 3 3
2
```
**Output:**
```
2 4
```
**Explanation:** Candidate 2's votes at indices 2, 3, 4. First = 2, Last = 4.

---

### Solutions

#### Python

```python
class Solution:
    def searchRange(self, votes: list[int], target: int) -> list[int]:
        # start your solution
        def findFirst(nums, target):
            left, right = 0, len(nums) - 1
            result = -1
            while left <= right:
                mid = left + (right - left) // 2
                if nums[mid] == target:
                    result = mid
                    right = mid - 1
                elif nums[mid] < target:
                    left = mid + 1
                else:
                    right = mid - 1
            return result
        
        def findLast(nums, target):
            left, right = 0, len(nums) - 1
            result = -1
            while left <= right:
                mid = left + (right - left) // 2
                if nums[mid] == target:
                    result = mid
                    left = mid + 1
                elif nums[mid] < target:
                    left = mid + 1
                else:
                    right = mid - 1
            return result
        
        return [findFirst(votes, target), findLast(votes, target)]
        # end your solution


def main():
    n = int(input())
    votes = list(map(int, input().split())) if n > 0 else []
    target = int(input())
    
    sol = Solution()
    result = sol.searchRange(votes, target)
    print(result[0], result[1])


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
    vector<int> searchRange(vector<int>& votes, int target) {
        // start your solution
        return {findFirst(votes, target), findLast(votes, target)};
    }
    
private:
    int findFirst(vector<int>& nums, int target) {
        int left = 0, right = nums.size() - 1;
        int result = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                result = mid;
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return result;
    }
    
    int findLast(vector<int>& nums, int target) {
        int left = 0, right = nums.size() - 1;
        int result = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                result = mid;
                left = mid + 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
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
    
    vector<int> votes(n);
    for (int i = 0; i < n; i++) {
        cin >> votes[i];
    }
    
    int target;
    cin >> target;
    
    Solution sol;
    vector<int> result = sol.searchRange(votes, target);
    cout << result[0] << " " << result[1] << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] searchRange(int[] votes, int target) {
        // start your solution
        return new int[]{findFirst(votes, target), findLast(votes, target)};
    }
    
    private int findFirst(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int result = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                result = mid;
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return result;
    }
    
    private int findLast(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int result = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                result = mid;
                left = mid + 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine().trim());
        int[] votes = new int[n];
        
        if (n > 0) {
            String[] parts = sc.nextLine().split(" ");
            for (int i = 0; i < n; i++) {
                votes[i] = Integer.parseInt(parts[i]);
            }
        } else {
            sc.nextLine();
        }
        
        int target = Integer.parseInt(sc.nextLine().trim());
        
        Solution sol = new Solution();
        int[] result = sol.searchRange(votes, target);
        System.out.println(result[0] + " " + result[1]);
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def searchRange(self, votes: list[int], target: int) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    votes = list(map(int, input().split())) if n > 0 else []
    target = int(input())
    
    sol = Solution()
    result = sol.searchRange(votes, target)
    print(result[0], result[1])


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
    vector<int> searchRange(vector<int>& votes, int target) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> votes(n);
    for (int i = 0; i < n; i++) {
        cin >> votes[i];
    }
    
    int target;
    cin >> target;
    
    Solution sol;
    vector<int> result = sol.searchRange(votes, target);
    cout << result[0] << " " << result[1] << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] searchRange(int[] votes, int target) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine().trim());
        int[] votes = new int[n];
        
        if (n > 0) {
            String[] parts = sc.nextLine().split(" ");
            for (int i = 0; i < n; i++) {
                votes[i] = Integer.parseInt(parts[i]);
            }
        } else {
            sc.nextLine();
        }
        
        int target = Integer.parseInt(sc.nextLine().trim());
        
        Solution sol = new Solution();
        int[] result = sol.searchRange(votes, target);
        System.out.println(result[0] + " " + result[1]);
        
        sc.close();
    }
}
```
