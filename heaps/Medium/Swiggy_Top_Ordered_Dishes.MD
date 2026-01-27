# Swiggy Top Ordered Dishes

### Problem Statement

Swiggy's Bengaluru analytics team is analyzing order patterns to identify trending dishes. They have a dataset of dish IDs from recent orders and want to find the k most frequently ordered dishes.

Given an array of integers representing dish IDs and an integer k, return the k most frequent dish IDs. The answer may be returned in any order.

### Input Format

- First line contains two integers: `n` (number of orders) and `k`
- Second line contains `n` space-separated integers representing dish IDs

### Output Format

- Print k space-separated integers representing the k most frequent dish IDs (any order)

### Constraints

- `1 <= n <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `k` is in the range `[1, number of unique elements]`
- The answer is guaranteed to be unique

### Test Cases

#### Test Case 1
**Input:**
```
6 2
1 1 1 2 2 3
```
**Output:**
```
1 2
```
**Explanation:** Dish 1 appears 3 times, dish 2 appears 2 times, dish 3 appears 1 time. Top 2 are 1 and 2.

---

#### Test Case 2
**Input:**
```
1 1
1
```
**Output:**
```
1
```
**Explanation:** Single dish, so it's the most frequent.

---

#### Test Case 3
**Input:**
```
5 2
1 2 3 4 5
```
**Output:**
```
1 2
```
**Explanation:** All have frequency 1. Any 2 can be returned (order-dependent in actual implementation).

---

#### Test Case 4
**Input:**
```
8 3
4 4 4 3 3 2 2 1
```
**Output:**
```
4 3 2
```
**Explanation:** Frequencies: 4→3, 3→2, 2→2, 1→1. Top 3 are 4, 3, 2.

---

#### Test Case 5
**Input:**
```
10 1
5 5 5 5 5 1 2 3 4 6
```
**Output:**
```
5
```
**Explanation:** Dish 5 has highest frequency (5 times).

---

#### Test Case 6
**Input:**
```
7 3
1 1 2 2 3 3 3
```
**Output:**
```
3 1 2
```
**Explanation:** Frequencies: 1→2, 2→2, 3→3. Top 3 are 3, 1, 2 (or 3, 2, 1).

---

#### Test Case 7
**Input:**
```
9 2
-1 -1 -1 0 0 1 1 1 1
```
**Output:**
```
1 -1
```
**Explanation:** Frequencies: -1→3, 0→2, 1→4. Top 2 are 1 and -1.

---

### Solutions

#### Python
```python
import heapq
from collections import Counter


class Solution:
    def topKFrequent(self, nums: list[int], k: int) -> list[int]:
        # start your solution
        count = Counter(nums)
        
        min_heap = []
        for num, freq in count.items():
            if len(min_heap) < k:
                heapq.heappush(min_heap, (freq, num))
            elif freq > min_heap[0][0]:
                heapq.heapreplace(min_heap, (freq, num))
        
        return [num for freq, num in min_heap]
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    nums = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.topKFrequent(nums, k)
    print(" ".join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // start your solution
        unordered_map<int, int> count;
        for (int num : nums) {
            count[num]++;
        }
        
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> minHeap;
        
        for (auto& [num, freq] : count) {
            if (minHeap.size() < k) {
                minHeap.push({freq, num});
            } else if (freq > minHeap.top().first) {
                minHeap.pop();
                minHeap.push({freq, num});
            }
        }
        
        vector<int> result;
        while (!minHeap.empty()) {
            result.push_back(minHeap.top().second);
            minHeap.pop();
        }
        
        return result;
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
    vector<int> result = sol.topKFrequent(nums, k);
    
    for (int i = 0; i < result.size(); i++) {
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
    public int[] topKFrequent(int[] nums, int k) {
        // start your solution
        Map<Integer, Integer> count = new HashMap<>();
        for (int num : nums) {
            count.put(num, count.getOrDefault(num, 0) + 1);
        }
        
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        
        for (Map.Entry<Integer, Integer> entry : count.entrySet()) {
            int num = entry.getKey();
            int freq = entry.getValue();
            
            if (minHeap.size() < k) {
                minHeap.offer(new int[]{freq, num});
            } else if (freq > minHeap.peek()[0]) {
                minHeap.poll();
                minHeap.offer(new int[]{freq, num});
            }
        }
        
        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = minHeap.poll()[1];
        }
        
        return result;
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
        int[] result = sol.topKFrequent(nums, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.length; i++) {
            if (i > 0) sb.append(" ");
            sb.append(result[i]);
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq
from collections import Counter


class Solution:
    def topKFrequent(self, nums: list[int], k: int) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    nums = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.topKFrequent(nums, k)
    print(" ".join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
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
    vector<int> result = sol.topKFrequent(nums, k);
    
    for (int i = 0; i < result.size(); i++) {
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
    public int[] topKFrequent(int[] nums, int k) {
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
        int[] result = sol.topKFrequent(nums, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.length; i++) {
            if (i > 0) sb.append(" ");
            sb.append(result[i]);
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```