# UPSC Topper Tracker

### Problem Statement

The Union Public Service Commission (UPSC) conducts the Civil Services Examination annually. A coaching institute in Delhi wants to track the kth highest score among all students who have appeared for their mock tests. As new students take the test, their scores are added to the system.

Design a class that finds the kth largest score in a stream of mock test scores. Note that it is the kth largest score in sorted order, not the kth distinct score.

Implement the `KthLargest` class:
- `KthLargest(int k, int[] nums)` - Initializes the object with the integer k and the initial stream of scores nums.
- `int add(int val)` - Appends the score val to the stream and returns the kth largest score in the current stream.

### Input Format

- First line contains two integers: `k` and `n` (initial number of scores)
- Second line contains `n` space-separated integers representing initial scores (or empty if n=0)
- Third line contains `q` (number of add operations)
- Next `q` lines each contain a score to add

### Output Format

- For each add operation, print the kth largest element after adding that score

### Constraints

- `1 <= k <= 10^4`
- `0 <= nums.length <= 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `-10^4 <= val <= 10^4`
- At most `10^4` calls will be made to add
- It is guaranteed that there will be at least k elements when you search for the kth largest

### Test Cases

#### Test Case 1
**Input:**
```
3 4
4 5 8 2
3
3
5
10
```
**Output:**
```
4
5
5
```
**Explanation:** Initial scores [4,5,8,2]. After adding 3: [2,3,4,5,8] → 3rd largest is 4. After adding 5: [2,3,4,5,5,8] → 3rd largest is 5. After adding 10: [2,3,4,5,5,8,10] → 3rd largest is 5.

---

#### Test Case 2
**Input:**
```
1 0

1
-1
```
**Output:**
```
-1
```
**Explanation:** k=1, empty initial array. After adding -1, the 1st largest is -1.

---

#### Test Case 3
**Input:**
```
2 3
1 2 3
2
4
5
```
**Output:**
```
3
4
```
**Explanation:** Initial [1,2,3]. After adding 4: [1,2,3,4] → 2nd largest is 3. After adding 5: [1,2,3,4,5] → 2nd largest is 4.

---

#### Test Case 4
**Input:**
```
3 5
5 5 5 5 5
2
5
5
```
**Output:**
```
5
5
```
**Explanation:** All same values. 3rd largest is always 5.

---

#### Test Case 5
**Input:**
```
4 3
7 7 7
3
7
7
7
```
**Output:**
```
7
7
7
```
**Explanation:** After each add, 4th largest exists and is 7.

---

#### Test Case 6
**Input:**
```
2 5
10 20 30 40 50
3
15
25
60
```
**Output:**
```
40
40
50
```
**Explanation:** Initial sorted [10,20,30,40,50]. 2nd largest is 40. After 15: still 40. After 25: still 40. After 60: [10,15,20,25,30,40,50,60] → 2nd largest is 50.

---

#### Test Case 7
**Input:**
```
1 3
100 200 300
2
50
400
```
**Output:**
```
300
400
```
**Explanation:** k=1 means finding max. After 50: max is 300. After 400: max is 400.

---

### Solutions

#### Python
```python
import heapq


class KthLargest:
    def __init__(self, k: int, nums: list[int]):
        # start your solution
        self.k = k
        self.min_heap = []
        
        for num in nums:
            self.add(num)
    
    def add(self, val: int) -> int:
        if len(self.min_heap) < self.k:
            heapq.heappush(self.min_heap, val)
        elif val > self.min_heap[0]:
            heapq.heapreplace(self.min_heap, val)
        
        return self.min_heap[0]
        # end your solution


def main():
    first_line = input().split()
    k = int(first_line[0])
    n = int(first_line[1])
    
    nums_line = input().strip()
    if nums_line and n > 0:
        nums = list(map(int, nums_line.split()))
    else:
        nums = []
    
    obj = KthLargest(k, nums)
    
    q = int(input())
    for _ in range(q):
        val = int(input())
        print(obj.add(val))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class KthLargest {
private:
    int k;
    priority_queue<int, vector<int>, greater<int>> minHeap;
    
public:
    // start your solution
    KthLargest(int k, vector<int>& nums) {
        this->k = k;
        for (int num : nums) {
            add(num);
        }
    }
    
    int add(int val) {
        if (minHeap.size() < k) {
            minHeap.push(val);
        } else if (val > minHeap.top()) {
            minHeap.pop();
            minHeap.push(val);
        }
        return minHeap.top();
    }
    // end your solution
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int k, n;
    cin >> k >> n;
    
    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }
    
    KthLargest obj(k, nums);
    
    int q;
    cin >> q;
    
    for (int i = 0; i < q; i++) {
        int val;
        cin >> val;
        cout << obj.add(val) << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class KthLargest {
    // start your solution
    private int k;
    private PriorityQueue<Integer> minHeap;
    
    public KthLargest(int k, int[] nums) {
        this.k = k;
        this.minHeap = new PriorityQueue<>();
        
        for (int num : nums) {
            add(num);
        }
    }
    
    public int add(int val) {
        if (minHeap.size() < k) {
            minHeap.offer(val);
        } else if (val > minHeap.peek()) {
            minHeap.poll();
            minHeap.offer(val);
        }
        return minHeap.peek();
    }
    // end your solution
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int k = sc.nextInt();
        int n = sc.nextInt();
        
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        
        KthLargest obj = new KthLargest(k, nums);
        
        int q = sc.nextInt();
        for (int i = 0; i < q; i++) {
            int val = sc.nextInt();
            System.out.println(obj.add(val));
        }
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq


class KthLargest:
    def __init__(self, k: int, nums: list[int]):
        # start your solution
        
        
    
    def add(self, val: int) -> int:
        
        
        # end your solution


def main():
    first_line = input().split()
    k = int(first_line[0])
    n = int(first_line[1])
    
    nums_line = input().strip()
    if nums_line and n > 0:
        nums = list(map(int, nums_line.split()))
    else:
        nums = []
    
    obj = KthLargest(k, nums)
    
    q = int(input())
    for _ in range(q):
        val = int(input())
        print(obj.add(val))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class KthLargest {
private:
    
    
public:
    // start your solution
    KthLargest(int k, vector<int>& nums) {
        
    }
    
    int add(int val) {
        
    }
    // end your solution
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int k, n;
    cin >> k >> n;
    
    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }
    
    KthLargest obj(k, nums);
    
    int q;
    cin >> q;
    
    for (int i = 0; i < q; i++) {
        int val;
        cin >> val;
        cout << obj.add(val) << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class KthLargest {
    // start your solution
    
    public KthLargest(int k, int[] nums) {
        
    }
    
    public int add(int val) {
        
    }
    // end your solution
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int k = sc.nextInt();
        int n = sc.nextInt();
        
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        
        KthLargest obj = new KthLargest(k, nums);
        
        int q = sc.nextInt();
        for (int i = 0; i < q; i++) {
            int val = sc.nextInt();
            System.out.println(obj.add(val));
        }
        
        sc.close();
    }
}
```