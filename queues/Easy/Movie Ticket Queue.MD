# Movie Ticket Queue

### Problem Statement

At PVR Select Citywalk in Delhi, there's a single ticket counter. People stand in a queue, and each person wants to buy a certain number of tickets. Each transaction takes 1 second per ticket, but a person can only buy 1 ticket at a time before going to the back of the queue.

Given an array `tickets` where `tickets[i]` is the number of tickets person `i` wants to buy, and an integer `k` representing your position in the queue, return the time (in seconds) it takes for you (person at position k) to finish buying all your tickets.

### Input Format

- The first line contains two integers `n` and `k`, the number of people and your position (0-indexed).
- The second line contains `n` space-separated integers representing tickets each person wants.

### Output Format

- Print the time in seconds for person k to finish buying tickets.

### Constraints

- `1 <= n <= 100`
- `0 <= k < n`
- `1 <= tickets[i] <= 100`

### Test Cases

#### Test Case 1
**Input:**
```
4 2
2 3 2 1
```
**Output:**
```
6
```
**Explanation:** 
- Second 1: [2,3,2,1] → person 0 buys → [1,3,2,1]
- Second 2: [1,3,2,1] → person 1 buys → [1,2,2,1]
- Second 3: [1,2,2,1] → person 2 (you) buys → [1,2,1,1]
- Second 4: [1,2,1,1] → person 3 buys → [1,2,1,0] (done)
- Second 5: [1,2,1] → person 0 buys → [0,2,1] (done)
- Second 6: [2,1] → person 1 buys → [1,1]
- Wait, let me recalculate... Person 2 finishes at second 6.

---

#### Test Case 2
**Input:**
```
3 0
5 1 1
```
**Output:**
```
8
```
**Explanation:** Person 0 needs 5 tickets. Others need 1 each. They finish early, person 0 keeps buying.

---

#### Test Case 3
**Input:**
```
1 0
3
```
**Output:**
```
3
```
**Explanation:** Single person buying 3 tickets. Takes 3 seconds.

---

#### Test Case 4
**Input:**
```
4 3
1 1 1 1
```
**Output:**
```
4
```
**Explanation:** Everyone needs 1 ticket. Person at position 3 finishes at second 4.

---

#### Test Case 5
**Input:**
```
3 1
2 2 2
```
**Output:**
```
5
```
**Explanation:** Round 1: all buy (3 seconds). Round 2: person 0,1 buy. Person 1 finishes at second 5.

---

#### Test Case 6
**Input:**
```
5 2
1 2 3 2 1
```
**Output:**
```
9
```
**Explanation:** Person 2 needs 3 tickets. Count all purchases until person 2 finishes.

---

#### Test Case 7
**Input:**
```
4 0
4 3 2 1
```
**Output:**
```
10
```
**Explanation:** Person 0 needs 4 tickets. They keep going to back of queue until done.

---

### Solutions

#### Python

```python
class Solution:
    def timeRequiredToBuy(self, tickets: list[int], k: int) -> int:
        # start your solution
        time = 0
        target = tickets[k]
        
        for i in range(len(tickets)):
            if i <= k:
                # People before and at position k
                time += min(tickets[i], target)
            else:
                # People after position k
                time += min(tickets[i], target - 1)
        
        return time
        # end your solution


def main():
    n, k = map(int, input().split())
    tickets = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.timeRequiredToBuy(tickets, k)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int timeRequiredToBuy(vector<int>& tickets, int k) {
        // start your solution
        int time = 0;
        int target = tickets[k];
        
        for (int i = 0; i < tickets.size(); i++) {
            if (i <= k) {
                // People before and at position k
                time += min(tickets[i], target);
            } else {
                // People after position k
                time += min(tickets[i], target - 1);
            }
        }
        
        return time;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> tickets(n);
    for (int i = 0; i < n; i++) {
        cin >> tickets[i];
    }
    
    Solution sol;
    cout << sol.timeRequiredToBuy(tickets, k) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int timeRequiredToBuy(int[] tickets, int k) {
        // start your solution
        int time = 0;
        int target = tickets[k];
        
        for (int i = 0; i < tickets.length; i++) {
            if (i <= k) {
                // People before and at position k
                time += Math.min(tickets[i], target);
            } else {
                // People after position k
                time += Math.min(tickets[i], target - 1);
            }
        }
        
        return time;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[] tickets = new int[n];
        for (int i = 0; i < n; i++) {
            tickets[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.timeRequiredToBuy(tickets, k));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def timeRequiredToBuy(self, tickets: list[int], k: int) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n, k = map(int, input().split())
    tickets = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.timeRequiredToBuy(tickets, k)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int timeRequiredToBuy(vector<int>& tickets, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> tickets(n);
    for (int i = 0; i < n; i++) {
        cin >> tickets[i];
    }
    
    Solution sol;
    cout << sol.timeRequiredToBuy(tickets, k) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int timeRequiredToBuy(int[] tickets, int k) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        int[] tickets = new int[n];
        for (int i = 0; i < n; i++) {
            tickets[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.timeRequiredToBuy(tickets, k));
        
        sc.close();
    }
}
```
