# Kabaddi Player Elimination

### Problem Statement

In a Pro Kabaddi League training camp in Patna, coaches have devised a unique elimination drill. Each player is assigned a strength score. In each round, the two players with the highest strength scores compete against each other.

The rules are:
- If both players have equal strength, both are eliminated from the drill.
- If the strengths are different, the weaker player is eliminated, and the stronger player's strength is reduced by the weaker player's strength value.

This continues until at most one player remains. The coaches want to know the strength of the last remaining player (or 0 if all players are eliminated).

Given an array of integers representing the strength scores of all players, return the strength of the last remaining player. If there are no players left, return 0.

### Input Format

- First line contains the number of players `n`
- Second line contains `n` space-separated integers representing strength scores

### Output Format

- A single integer representing the strength of the last remaining player (0 if none remain)

### Constraints

- `1 <= n <= 30`
- `1 <= stones[i] <= 1000`

### Test Cases

#### Test Case 1
**Input:**
```
6
2 7 4 1 8 1
```
**Output:**
```
1
```
**Explanation:** 
- Combine 8 and 7: 8-7=1 → [2,4,1,1,1]
- Combine 4 and 2: 4-2=2 → [1,1,1,2]
- Combine 2 and 1: 2-1=1 → [1,1,1]
- Combine 1 and 1: both eliminated → [1]
- Result: 1

---

#### Test Case 2
**Input:**
```
1
1
```
**Output:**
```
1
```
**Explanation:** Only one player, so they remain with strength 1.

---

#### Test Case 3
**Input:**
```
2
10 10
```
**Output:**
```
0
```
**Explanation:** Both have equal strength, both eliminated. No one remains.

---

#### Test Case 4
**Input:**
```
3
3 3 3
```
**Output:**
```
3
```
**Explanation:** Combine two 3s → eliminated → one 3 remains.

---

#### Test Case 5
**Input:**
```
4
1 2 3 4
```
**Output:**
```
0
```
**Explanation:** 
- 4 and 3: 4-3=1 → [1,2,1]
- 2 and 1: 2-1=1 → [1,1]
- 1 and 1: eliminated → []
- Result: 0

---

#### Test Case 6
**Input:**
```
5
5 5 5 5 5
```
**Output:**
```
5
```
**Explanation:** Pairs cancel out, one 5 remains.

---

#### Test Case 7
**Input:**
```
4
100 50 25 10
```
**Output:**
```
15
```
**Explanation:** 
- 100 and 50: 100-50=50 → [50,25,10]
- 50 and 25: 50-25=25 → [25,10]
- 25 and 10: 25-10=15 → [15]
- Result: 15

---

### Solutions

#### Python
```python
import heapq


class Solution:
    def lastStoneWeight(self, stones: list[int]) -> int:
        # start your solution
        max_heap = [-s for s in stones]
        heapq.heapify(max_heap)
        
        while len(max_heap) > 1:
            first = -heapq.heappop(max_heap)
            second = -heapq.heappop(max_heap)
            
            if first != second:
                heapq.heappush(max_heap, -(first - second))
        
        return -max_heap[0] if max_heap else 0
        # end your solution


def main():
    n = int(input())
    stones = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.lastStoneWeight(stones))


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
    int lastStoneWeight(vector<int>& stones) {
        // start your solution
        priority_queue<int> maxHeap(stones.begin(), stones.end());
        
        while (maxHeap.size() > 1) {
            int first = maxHeap.top();
            maxHeap.pop();
            int second = maxHeap.top();
            maxHeap.pop();
            
            if (first != second) {
                maxHeap.push(first - second);
            }
        }
        
        return maxHeap.empty() ? 0 : maxHeap.top();
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> stones(n);
    for (int i = 0; i < n; i++) {
        cin >> stones[i];
    }
    
    Solution sol;
    cout << sol.lastStoneWeight(stones) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int lastStoneWeight(int[] stones) {
        // start your solution
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        
        for (int stone : stones) {
            maxHeap.offer(stone);
        }
        
        while (maxHeap.size() > 1) {
            int first = maxHeap.poll();
            int second = maxHeap.poll();
            
            if (first != second) {
                maxHeap.offer(first - second);
            }
        }
        
        return maxHeap.isEmpty() ? 0 : maxHeap.peek();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] stones = new int[n];
        for (int i = 0; i < n; i++) {
            stones[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.lastStoneWeight(stones));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq


class Solution:
    def lastStoneWeight(self, stones: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    stones = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.lastStoneWeight(stones))


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
    int lastStoneWeight(vector<int>& stones) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> stones(n);
    for (int i = 0; i < n; i++) {
        cin >> stones[i];
    }
    
    Solution sol;
    cout << sol.lastStoneWeight(stones) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int lastStoneWeight(int[] stones) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] stones = new int[n];
        for (int i = 0; i < n; i++) {
            stones[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.lastStoneWeight(stones));
        
        sc.close();
    }
}
```