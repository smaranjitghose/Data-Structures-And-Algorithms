# UPI Transaction Match

### Problem Statement

Priya works at a fintech startup in Bengaluru. She's building a feature for their UPI payment app that helps users split bills.

Given an array `transactions` representing amounts received from different friends and a `target` amount that needs to be settled, find the indices of two transactions that add up exactly to the target.

Return the indices of the two transactions. You may assume that each input has exactly one solution, and you cannot use the same transaction twice.

### Input Format

- The first line contains two integers `n` and `target` — the number of transactions and the target amount.
- The second line contains `n` space-separated integers representing the transaction amounts.

### Output Format

- Print two space-separated integers — the indices (0-indexed) of the two transactions that sum to the target.

### Constraints

- `2 <= n <= 10^4`
- `-10^9 <= transactions[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- Exactly one valid solution exists.

### Test Cases

#### Test Case 1
**Input:**
```
4 9
2 7 11 15
```
**Output:**
```
0 1
```
**Explanation:** transactions[0] + transactions[1] = 2 + 7 = 9. So the answer is indices 0 and 1.

---

#### Test Case 2
**Input:**
```
3 6
3 2 4
```
**Output:**
```
1 2
```
**Explanation:** transactions[1] + transactions[2] = 2 + 4 = 6.

---

#### Test Case 3
**Input:**
```
2 6
3 3
```
**Output:**
```
0 1
```
**Explanation:** transactions[0] + transactions[1] = 3 + 3 = 6.

---

#### Test Case 4
**Input:**
```
5 100
10 90 20 80 50
```
**Output:**
```
0 1
```
**Explanation:** transactions[0] + transactions[1] = 10 + 90 = 100.

---

#### Test Case 5
**Input:**
```
4 0
-3 4 3 90
```
**Output:**
```
0 2
```
**Explanation:** transactions[0] + transactions[2] = -3 + 3 = 0.

---

#### Test Case 6
**Input:**
```
6 150
25 75 50 100 125 25
```
**Output:**
```
1 4
```
**Explanation:** transactions[1] + transactions[4] = 75 + 125 = 150.

---

#### Test Case 7
**Input:**
```
3 -5
-10 5 -3
```
**Output:**
```
0 1
```
**Explanation:** transactions[0] + transactions[1] = -10 + 5 = -5.

---

### Solutions

#### Python

```python
class Solution:
    def findTransactionPair(self, transactions: list[int], target: int) -> list[int]:
        # start your solution
        seen = {}
        for i, amount in enumerate(transactions):
            complement = target - amount
            if complement in seen:
                return [seen[complement], i]
            seen[amount] = i
        return []
        # end your solution


def main():
    first_line = input().split()
    n, target = int(first_line[0]), int(first_line[1])
    transactions = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.findTransactionPair(transactions, target)
    print(result[0], result[1])


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
    vector<int> findTransactionPair(vector<int>& transactions, int target) {
        // start your solution
        unordered_map<int, int> seen;
        for (int i = 0; i < transactions.size(); i++) {
            int complement = target - transactions[i];
            if (seen.find(complement) != seen.end()) {
                return {seen[complement], i};
            }
            seen[transactions[i]] = i;
        }
        return {};
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, target;
    cin >> n >> target;
    
    vector<int> transactions(n);
    for (int i = 0; i < n; i++) {
        cin >> transactions[i];
    }
    
    Solution sol;
    vector<int> result = sol.findTransactionPair(transactions, target);
    cout << result[0] << " " << result[1] << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] findTransactionPair(int[] transactions, int target) {
        // start your solution
        Map<Integer, Integer> seen = new HashMap<>();
        for (int i = 0; i < transactions.length; i++) {
            int complement = target - transactions[i];
            if (seen.containsKey(complement)) {
                return new int[] {seen.get(complement), i};
            }
            seen.put(transactions[i], i);
        }
        return new int[] {};
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int target = sc.nextInt();
        int[] transactions = new int[n];
        
        for (int i = 0; i < n; i++) {
            transactions[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.findTransactionPair(transactions, target);
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
    def findTransactionPair(self, transactions: list[int], target: int) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    n, target = int(first_line[0]), int(first_line[1])
    transactions = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.findTransactionPair(transactions, target)
    print(result[0], result[1])


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
    vector<int> findTransactionPair(vector<int>& transactions, int target) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, target;
    cin >> n >> target;
    
    vector<int> transactions(n);
    for (int i = 0; i < n; i++) {
        cin >> transactions[i];
    }
    
    Solution sol;
    vector<int> result = sol.findTransactionPair(transactions, target);
    cout << result[0] << " " << result[1] << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] findTransactionPair(int[] transactions, int target) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int target = sc.nextInt();
        int[] transactions = new int[n];
        
        for (int i = 0; i < n; i++) {
            transactions[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.findTransactionPair(transactions, target);
        System.out.println(result[0] + " " + result[1]);
        
        sc.close();
    }
}
```
