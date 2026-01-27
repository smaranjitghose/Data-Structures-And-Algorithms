# Diwali Mithai Distribution

### Problem Statement

During Diwali celebrations in Jaipur, a generous businessman has arranged multiple boxes of mithai (sweets) to distribute among the poor. Each box contains a certain number of sweets. A volunteer follows a specific distribution process for `k` rounds.

In each round:
1. The volunteer picks the box with the maximum number of sweets
2. Takes sweets from it, leaving behind only the floor of the square root of the original count
3. The remaining sweets stay in that box for future rounds

After `k` rounds of distribution, the businessman wants to know the total number of sweets remaining across all boxes.

Given an array representing the number of sweets in each box and the number of distribution rounds `k`, return the total number of sweets remaining after `k` rounds.

### Input Format

- First line contains two integers: `n` (number of boxes) and `k` (number of rounds)
- Second line contains `n` space-separated integers representing sweets in each box

### Output Format

- A single integer representing the total remaining sweets

### Constraints

- `1 <= n <= 10^3`
- `1 <= k <= 10^3`
- `1 <= gifts[i] <= 10^9`

### Test Cases

#### Test Case 1
**Input:**
```
5 4
25 64 9 4 100
```
**Output:**
```
29
```
**Explanation:**
- Round 1: Pick 100 → leave √100=10 → [25,64,9,4,10]
- Round 2: Pick 64 → leave √64=8 → [25,8,9,4,10]
- Round 3: Pick 25 → leave √25=5 → [5,8,9,4,10]
- Round 4: Pick 10 → leave √10=3 → [5,8,9,4,3]
- Total: 5+8+9+4+3 = 29

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
**Explanation:** √1 = 1, so the box still has 1 sweet.

---

#### Test Case 3
**Input:**
```
3 2
16 16 16
```
**Output:**
```
24
```
**Explanation:**
- Round 1: Pick any 16 → leave 4 → [4,16,16]
- Round 2: Pick any 16 → leave 4 → [4,4,16]
- Total: 4+4+16 = 24

---

#### Test Case 4
**Input:**
```
4 3
81 27 9 3
```
**Output:**
```
24
```
**Explanation:**
- Round 1: 81 → 9 → [9,27,9,3]
- Round 2: 27 → 5 → [9,5,9,3]
- Round 3: 9 → 3 → [3,5,9,3]
- Total: 3+5+9+3 = 20

---

#### Test Case 5
**Input:**
```
2 10
1 1
```
**Output:**
```
2
```
**Explanation:** Both boxes have 1. √1=1. No matter how many rounds, total stays 2.

---

#### Test Case 6
**Input:**
```
3 1
1000000000 1000000000 1000000000
```
**Output:**
```
2000031622
```
**Explanation:** One box: 10^9 → √(10^9) ≈ 31622. Total = 31622 + 10^9 + 10^9 = 2000031622.

---

#### Test Case 7
**Input:**
```
4 2
49 36 25 16
```
**Output:**
```
53
```
**Explanation:**
- Round 1: 49 → 7 → [7,36,25,16]
- Round 2: 36 → 6 → [7,6,25,16]
- Total: 7+6+25+16 = 54

---

### Solutions

#### Python
```python
import heapq
import math


class Solution:
    def pickGifts(self, gifts: list[int], k: int) -> int:
        # start your solution
        max_heap = [-g for g in gifts]
        heapq.heapify(max_heap)
        
        for _ in range(k):
            max_val = -heapq.heappop(max_heap)
            new_val = int(math.sqrt(max_val))
            heapq.heappush(max_heap, -new_val)
        
        return -sum(max_heap)
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    gifts = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.pickGifts(gifts, k))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <cmath>
using namespace std;

class Solution {
public:
    long long pickGifts(vector<int>& gifts, int k) {
        // start your solution
        priority_queue<long long> maxHeap;
        
        for (int g : gifts) {
            maxHeap.push(g);
        }
        
        for (int i = 0; i < k; i++) {
            long long maxVal = maxHeap.top();
            maxHeap.pop();
            maxHeap.push((long long)sqrt(maxVal));
        }
        
        long long total = 0;
        while (!maxHeap.empty()) {
            total += maxHeap.top();
            maxHeap.pop();
        }
        
        return total;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> gifts(n);
    for (int i = 0; i < n; i++) {
        cin >> gifts[i];
    }
    
    Solution sol;
    cout << sol.pickGifts(gifts, k) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public long pickGifts(int[] gifts, int k) {
        // start your solution
        PriorityQueue<Long> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        
        for (int g : gifts) {
            maxHeap.offer((long) g);
        }
        
        for (int i = 0; i < k; i++) {
            long maxVal = maxHeap.poll();
            maxHeap.offer((long) Math.sqrt(maxVal));
        }
        
        long total = 0;
        while (!maxHeap.isEmpty()) {
            total += maxHeap.poll();
        }
        
        return total;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[] gifts = new int[n];
        for (int i = 0; i < n; i++) {
            gifts[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.pickGifts(gifts, k));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq
import math


class Solution:
    def pickGifts(self, gifts: list[int], k: int) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    gifts = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.pickGifts(gifts, k))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <cmath>
using namespace std;

class Solution {
public:
    long long pickGifts(vector<int>& gifts, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> gifts(n);
    for (int i = 0; i < n; i++) {
        cin >> gifts[i];
    }
    
    Solution sol;
    cout << sol.pickGifts(gifts, k) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public long pickGifts(int[] gifts, int k) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[] gifts = new int[n];
        for (int i = 0; i < n; i++) {
            gifts[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.pickGifts(gifts, k));
        
        sc.close();
    }
}
```