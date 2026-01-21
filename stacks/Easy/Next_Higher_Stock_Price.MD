# Next Higher Stock Price

### Problem Statement

At the National Stock Exchange (NSE) in Mumbai, analysts track stock prices to find the next higher price for selected stocks. Given a watchlist of stocks and the complete market prices, find the next greater price for each stock in the watchlist.

The next greater element of a number `x` in `watchlist` is the first greater number to its right in `market`. If no such number exists, output -1.

### Input Format

- The first line contains two integers `m` and `n`, sizes of watchlist and market arrays.
- The second line contains `m` space-separated integers (watchlist - subset of market with no duplicates).
- The third line contains `n` space-separated integers (market - no duplicates).

### Output Format

- Print `m` space-separated integers representing next greater elements for each watchlist item.

### Constraints

- `1 <= m <= n <= 1000`
- `0 <= watchlist[i], market[i] <= 10^4`
- All integers in `watchlist` and `market` are unique
- All integers in `watchlist` appear in `market`

### Test Cases

#### Test Case 1
**Input:**
```
2 4
4 1
1 3 4 2
```
**Output:**
```
-1 3
```
**Explanation:** For 4: no greater element to its right in market. For 1: next greater is 3.

---

#### Test Case 2
**Input:**
```
2 4
2 4
1 2 3 4
```
**Output:**
```
3 -1
```
**Explanation:** For 2: next greater is 3. For 4: no greater element exists.

---

#### Test Case 3
**Input:**
```
3 5
1 3 5
5 4 3 2 1
```
**Output:**
```
-1 -1 -1
```
**Explanation:** Decreasing sequence. No element has a greater element to its right.

---

#### Test Case 4
**Input:**
```
3 5
2 4 6
1 2 4 6 8
```
**Output:**
```
4 6 8
```
**Explanation:** For 2→4, for 4→6, for 6→8. Each has next greater element.

---

#### Test Case 5
**Input:**
```
1 3
5
3 5 7
```
**Output:**
```
7
```
**Explanation:** For 5: next greater is 7.

---

#### Test Case 6
**Input:**
```
4 6
6 2 4 1
1 2 6 4 3 5
```
**Output:**
```
-1 6 5 2
```
**Explanation:** For 6: no greater. For 2: next is 6. For 4: next is 5. For 1: next is 2.

---

#### Test Case 7
**Input:**
```
3 3
1 2 3
1 2 3
```
**Output:**
```
2 3 -1
```
**Explanation:** Increasing sequence. Each element's next greater is the immediate next, except last.

---

### Solutions

#### Python

```python
class Solution:
    def nextGreaterElement(self, watchlist: list[int], market: list[int]) -> list[int]:
        # start your solution
        # Build next greater map using monotonic stack
        nextGreater = {}
        stack = []
        
        for price in market:
            while stack and stack[-1] < price:
                nextGreater[stack.pop()] = price
            stack.append(price)
        
        # Remaining elements have no next greater
        while stack:
            nextGreater[stack.pop()] = -1
        
        # Build result for watchlist
        return [nextGreater[price] for price in watchlist]
        # end your solution


def main():
    m, n = map(int, input().split())
    watchlist = list(map(int, input().split()))
    market = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.nextGreaterElement(watchlist, market)
    print(' '.join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& watchlist, vector<int>& market) {
        // start your solution
        // Build next greater map using monotonic stack
        unordered_map<int, int> nextGreater;
        stack<int> stk;
        
        for (int price : market) {
            while (!stk.empty() && stk.top() < price) {
                nextGreater[stk.top()] = price;
                stk.pop();
            }
            stk.push(price);
        }
        
        // Remaining elements have no next greater
        while (!stk.empty()) {
            nextGreater[stk.top()] = -1;
            stk.pop();
        }
        
        // Build result for watchlist
        vector<int> result;
        for (int price : watchlist) {
            result.push_back(nextGreater[price]);
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<int> watchlist(m), market(n);
    for (int i = 0; i < m; i++) cin >> watchlist[i];
    for (int i = 0; i < n; i++) cin >> market[i];
    
    Solution sol;
    vector<int> result = sol.nextGreaterElement(watchlist, market);
    
    for (int i = 0; i < result.size(); i++) {
        cout << result[i];
        if (i < result.size() - 1) cout << " ";
    }
    cout << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] nextGreaterElement(int[] watchlist, int[] market) {
        // start your solution
        // Build next greater map using monotonic stack
        Map<Integer, Integer> nextGreater = new HashMap<>();
        Stack<Integer> stack = new Stack<>();
        
        for (int price : market) {
            while (!stack.isEmpty() && stack.peek() < price) {
                nextGreater.put(stack.pop(), price);
            }
            stack.push(price);
        }
        
        // Remaining elements have no next greater
        while (!stack.isEmpty()) {
            nextGreater.put(stack.pop(), -1);
        }
        
        // Build result for watchlist
        int[] result = new int[watchlist.length];
        for (int i = 0; i < watchlist.length; i++) {
            result[i] = nextGreater.get(watchlist[i]);
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
        
        int[] watchlist = new int[m];
        int[] market = new int[n];
        
        for (int i = 0; i < m; i++) watchlist[i] = sc.nextInt();
        for (int i = 0; i < n; i++) market[i] = sc.nextInt();
        
        Solution sol = new Solution();
        int[] result = sol.nextGreaterElement(watchlist, market);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.length; i++) {
            sb.append(result[i]);
            if (i < result.length - 1) sb.append(" ");
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def nextGreaterElement(self, watchlist: list[int], market: list[int]) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    m, n = map(int, input().split())
    watchlist = list(map(int, input().split()))
    market = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.nextGreaterElement(watchlist, market)
    print(' '.join(map(str, result)))


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& watchlist, vector<int>& market) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int m, n;
    cin >> m >> n;
    
    vector<int> watchlist(m), market(n);
    for (int i = 0; i < m; i++) cin >> watchlist[i];
    for (int i = 0; i < n; i++) cin >> market[i];
    
    Solution sol;
    vector<int> result = sol.nextGreaterElement(watchlist, market);
    
    for (int i = 0; i < result.size(); i++) {
        cout << result[i];
        if (i < result.size() - 1) cout << " ";
    }
    cout << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] nextGreaterElement(int[] watchlist, int[] market) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        int[] watchlist = new int[m];
        int[] market = new int[n];
        
        for (int i = 0; i < m; i++) watchlist[i] = sc.nextInt();
        for (int i = 0; i < n; i++) market[i] = sc.nextInt();
        
        Solution sol = new Solution();
        int[] result = sol.nextGreaterElement(watchlist, market);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.length; i++) {
            sb.append(result[i]);
            if (i < result.length - 1) sb.append(" ");
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```
