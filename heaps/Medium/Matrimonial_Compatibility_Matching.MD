# Matrimonial Compatibility Matching

### Problem Statement

A popular Indian matrimonial website uses a compatibility scoring system. They have two sorted lists: one containing compatibility scores of prospective brides and another for prospective grooms. The website wants to suggest matches by pairing one bride and one groom, where the total compatibility score (sum of both individual scores) is minimized.

Given two sorted arrays `nums1` (brides' scores) and `nums2` (grooms' scores), both in ascending order, and an integer `k`, return the k pairs with the smallest sums. Each pair consists of one element from nums1 and one from nums2.

Return the pairs in order of their sums (smallest first). If there are ties, any order among tied pairs is acceptable.

### Input Format

- First line contains three integers: `m` (size of nums1), `n` (size of nums2), and `k`
- Second line contains `m` space-separated integers representing nums1 (sorted ascending)
- Third line contains `n` space-separated integers representing nums2 (sorted ascending)

### Output Format

- Print k lines, each containing two space-separated integers representing a pair

### Constraints

- `1 <= m, n <= 10^5`
- `-10^9 <= nums1[i], nums2[i] <= 10^9`
- `1 <= k <= min(10^4, m * n)`
- nums1 and nums2 are sorted in ascending order

### Test Cases

#### Test Case 1
**Input:**
```
3 3 3
1 7 11
2 4 6
```
**Output:**
```
1 2
1 4
1 6
```
**Explanation:** Pairs sorted by sum: (1,2)=3, (1,4)=5, (1,6)=7, (7,2)=9, (7,4)=11, (7,6)=13, (11,2)=13... Top 3 are (1,2), (1,4), (1,6).

---

#### Test Case 2
**Input:**
```
3 3 3
1 1 2
1 2 3
```
**Output:**
```
1 1
1 1
2 1
```
**Explanation:** (1,1)=2 appears twice, then (2,1)=3 or (1,2)=3.

---

#### Test Case 3
**Input:**
```
2 2 2
1 2
3 4
```
**Output:**
```
1 3
1 4
```
**Explanation:** (1,3)=4, (1,4)=5 are the two smallest.

---

#### Test Case 4
**Input:**
```
1 3 2
1
2 3 4
```
**Output:**
```
1 2
1 3
```
**Explanation:** Only pairs with 1: (1,2)=3, (1,3)=4, (1,4)=5. Top 2 are (1,2), (1,3).

---

#### Test Case 5
**Input:**
```
3 1 3
1 2 3
5
```
**Output:**
```
1 5
2 5
3 5
```
**Explanation:** Only one element in nums2. Pairs: (1,5)=6, (2,5)=7, (3,5)=8.

---

#### Test Case 6
**Input:**
```
2 2 4
1 2
1 2
```
**Output:**
```
1 1
1 2
2 1
2 2
```
**Explanation:** All 4 pairs: (1,1)=2, (1,2)=3, (2,1)=3, (2,2)=4.

---

#### Test Case 7
**Input:**
```
3 3 5
-5 0 5
-3 0 3
```
**Output:**
```
-5 -3
-5 0
0 -3
-5 3
0 0
```
**Explanation:** Sorted by sum: (-5,-3)=-8, (-5,0)=-5, (0,-3)=-3, (-5,3)=-2, (0,0)=0.

---

### Solutions

#### Python
```python
import heapq


class Solution:
    def kSmallestPairs(self, nums1: list[int], nums2: list[int], k: int) -> list[list[int]]:
        # start your solution
        if not nums1 or not nums2:
            return []
        
        min_heap = []
        result = []
        
        for i in range(min(k, len(nums1))):
            heapq.heappush(min_heap, (nums1[i] + nums2[0], i, 0))
        
        while min_heap and len(result) < k:
            sum_val, i, j = heapq.heappop(min_heap)
            result.append([nums1[i], nums2[j]])
            
            if j + 1 < len(nums2):
                heapq.heappush(min_heap, (nums1[i] + nums2[j + 1], i, j + 1))
        
        return result
        # end your solution


def main():
    first_line = input().split()
    m = int(first_line[0])
    n = int(first_line[1])
    k = int(first_line[2])
    
    nums1 = list(map(int, input().split()))
    nums2 = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.kSmallestPairs(nums1, nums2, k)
    
    for pair in result:
        print(pair[0], pair[1])


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
    vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        // start your solution
        vector<vector<int>> result;
        if (nums1.empty() || nums2.empty()) return result;
        
        auto cmp = [](const tuple<int, int, int>& a, const tuple<int, int, int>& b) {
            return get<0>(a) > get<0>(b);
        };
        priority_queue<tuple<int, int, int>, vector<tuple<int, int, int>>, decltype(cmp)> minHeap(cmp);
        
        for (int i = 0; i < min(k, (int)nums1.size()); i++) {
            minHeap.push({nums1[i] + nums2[0], i, 0});
        }
        
        while (!minHeap.empty() && result.size() < k) {
            auto [sum_val, i, j] = minHeap.top();
            minHeap.pop();
            result.push_back({nums1[i], nums2[j]});
            
            if (j + 1 < nums2.size()) {
                minHeap.push({nums1[i] + nums2[j + 1], i, j + 1});
            }
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n, k;
    cin >> m >> n >> k;
    
    vector<int> nums1(m), nums2(n);
    for (int i = 0; i < m; i++) cin >> nums1[i];
    for (int i = 0; i < n; i++) cin >> nums2[i];
    
    Solution sol;
    vector<vector<int>> result = sol.kSmallestPairs(nums1, nums2, k);
    
    for (auto& pair : result) {
        cout << pair[0] << " " << pair[1] << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        // start your solution
        List<List<Integer>> result = new ArrayList<>();
        if (nums1.length == 0 || nums2.length == 0) return result;
        
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        
        for (int i = 0; i < Math.min(k, nums1.length); i++) {
            minHeap.offer(new int[]{nums1[i] + nums2[0], i, 0});
        }
        
        while (!minHeap.isEmpty() && result.size() < k) {
            int[] curr = minHeap.poll();
            int i = curr[1];
            int j = curr[2];
            result.add(Arrays.asList(nums1[i], nums2[j]));
            
            if (j + 1 < nums2.length) {
                minHeap.offer(new int[]{nums1[i] + nums2[j + 1], i, j + 1});
            }
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
        
        int[] nums1 = new int[m];
        int[] nums2 = new int[n];
        for (int i = 0; i < m; i++) nums1[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums2[i] = sc.nextInt();
        
        Solution sol = new Solution();
        List<List<Integer>> result = sol.kSmallestPairs(nums1, nums2, k);
        
        for (List<Integer> pair : result) {
            System.out.println(pair.get(0) + " " + pair.get(1));
        }
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq


class Solution:
    def kSmallestPairs(self, nums1: list[int], nums2: list[int], k: int) -> list[list[int]]:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    m = int(first_line[0])
    n = int(first_line[1])
    k = int(first_line[2])
    
    nums1 = list(map(int, input().split()))
    nums2 = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.kSmallestPairs(nums1, nums2, k)
    
    for pair in result:
        print(pair[0], pair[1])


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
    vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n, k;
    cin >> m >> n >> k;
    
    vector<int> nums1(m), nums2(n);
    for (int i = 0; i < m; i++) cin >> nums1[i];
    for (int i = 0; i < n; i++) cin >> nums2[i];
    
    Solution sol;
    vector<vector<int>> result = sol.kSmallestPairs(nums1, nums2, k);
    
    for (auto& pair : result) {
        cout << pair[0] << " " << pair[1] << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
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
        
        int[] nums1 = new int[m];
        int[] nums2 = new int[n];
        for (int i = 0; i < m; i++) nums1[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums2[i] = sc.nextInt();
        
        Solution sol = new Solution();
        List<List<Integer>> result = sol.kSmallestPairs(nums1, nums2, k);
        
        for (List<Integer> pair : result) {
            System.out.println(pair.get(0) + " " + pair.get(1));
        }
        
        sc.close();
    }
}
```