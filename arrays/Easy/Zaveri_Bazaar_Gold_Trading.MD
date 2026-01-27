# Zaveri Bazaar Gold Trading

### Problem Statement

Priya runs a small jewelry business in Mumbai's famous Zaveri Bazaar, India's largest gold market. She tracks the daily gold prices (per 10 grams) and wants to maximize her profit by buying gold on one day and selling it on a future day.

Being a cautious trader, Priya will only make one transaction - she will buy gold once and sell it once. She wants to know the maximum profit she can achieve. If the gold prices are continuously falling and no profit is possible, she will not trade at all.

Given an array where `prices[i]` represents the gold price on the `i`th day, find the maximum profit Priya can achieve. If no profit is possible, return 0.

Note: You must buy before you sell - selling before buying is not allowed.

### Input Format

- First line contains the number of days `n`
- Second line contains `n` space-separated integers representing daily gold prices (₹ per 10 grams)

### Output Format

- A single integer representing the maximum profit possible (0 if no profit)

### Constraints

- `1 <= n <= 10^5`
- `0 <= prices[i] <= 10^4`

### Test Cases

#### Test Case 1
**Input:**
```
6
5200 4800 4950 4850 5100 5000
```
**Output:**
```
300
```
**Explanation:** Buy on day 2 (₹4800), sell on day 5 (₹5100). Profit = ₹300.

---

#### Test Case 2
**Input:**
```
5
5500 5400 5300 5200 5100
```
**Output:**
```
0
```
**Explanation:** Gold prices falling continuously. No profitable trade possible.

---

#### Test Case 3
**Input:**
```
2
4700 4850
```
**Output:**
```
150
```
**Explanation:** Buy on day 1 (₹4700), sell on day 2 (₹4850). Profit = ₹150.

---

#### Test Case 4
**Input:**
```
1
5000
```
**Output:**
```
0
```
**Explanation:** Only one day of data, cannot complete a buy-sell transaction.

---

#### Test Case 5
**Input:**
```
6
4900 4900 4900 4900 4900 4900
```
**Output:**
```
0
```
**Explanation:** Gold price unchanged throughout. No profit possible.

---

#### Test Case 6
**Input:**
```
5
4500 4600 4700 4800 4900
```
**Output:**
```
400
```
**Explanation:** Buy on day 1 (₹4500), sell on day 5 (₹4900). Profit = ₹400.

---

#### Test Case 7
**Input:**
```
8
4800 4700 5000 4900 4600 4800 4700 4950
```
**Output:**
```
350
```
**Explanation:** Buy on day 5 (₹4600), sell on day 8 (₹4950). Profit = ₹350.

---

### Solutions

#### Python
```python
class Solution:
    def maxProfit(self, prices: list[int]) -> int:
        # start your solution
        if len(prices) < 2:
            return 0
        
        min_price = prices[0]
        max_profit = 0
        
        for price in prices:
            if price < min_price:
                min_price = price
            else:
                max_profit = max(max_profit, price - min_price)
        
        return max_profit
        # end your solution


def main():
    n = int(input())
    prices = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.maxProfit(prices))


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
    int maxProfit(vector<int>& prices) {
        // start your solution
        if (prices.size() < 2) {
            return 0;
        }
        
        int minPrice = prices[0];
        int maxProfit = 0;
        
        for (int price : prices) {
            if (price < minPrice) {
                minPrice = price;
            } else {
                maxProfit = max(maxProfit, price - minPrice);
            }
        }
        
        return maxProfit;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> prices(n);
    for (int i = 0; i < n; i++) {
        cin >> prices[i];
    }
    
    Solution sol;
    cout << sol.maxProfit(prices) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int maxProfit(int[] prices) {
        // start your solution
        if (prices.length < 2) {
            return 0;
        }
        
        int minPrice = prices[0];
        int maxProfit = 0;
        
        for (int price : prices) {
            if (price < minPrice) {
                minPrice = price;
            } else {
                maxProfit = Math.max(maxProfit, price - minPrice);
            }
        }
        
        return maxProfit;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] prices = new int[n];
        for (int i = 0; i < n; i++) {
            prices[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.maxProfit(prices));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def maxProfit(self, prices: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    prices = list(map(int, input().split()))
    
    sol = Solution()
    print(sol.maxProfit(prices))


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
    int maxProfit(vector<int>& prices) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> prices(n);
    for (int i = 0; i < n; i++) {
        cin >> prices[i];
    }
    
    Solution sol;
    cout << sol.maxProfit(prices) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public int maxProfit(int[] prices) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] prices = new int[n];
        for (int i = 0; i < n; i++) {
            prices[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.maxProfit(prices));
        
        sc.close();
    }
}
```