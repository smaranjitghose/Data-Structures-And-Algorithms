# The Unique Diwali Gift

### Problem Statement

Rohan runs a gift shop in Chandni Chowk, Delhi. During Diwali, he introduced a "Buy One Get One Free" (BOGO) scheme where every purchased gift box comes with an identical free one. This means every gift box ID appears exactly twice in his sales register.

At the end of the day, Rohan notices that due to a billing glitch, exactly one gift box was sold without the BOGO scheme — it appears only once.

Given an array `gifts` of gift box IDs, find the ID of the unique gift box sold without the BOGO offer.

**Note:** Implement a solution with O(n) time complexity and O(1) space.

### Input Format

- The first line contains an integer `n`, the number of entries in the sales register.
- The second line contains `n` space-separated integers representing the gift box IDs.

### Output Format

- Print a single integer — the ID of the unique gift box that was sold without the BOGO offer.

### Constraints

- `1 <= gifts.length <= 3 * 10^4`
- `gifts.length` is always odd
- `-3 * 10^4 <= gifts[i] <= 3 * 10^4`
- Each element in the array appears twice except for one element which appears only once

### Test Cases

#### Test Case 1
**Input:**
```
3
2 2 1
```
**Output:**
```
1
```
**Explanation:** Gift box with ID 2 was sold under BOGO (appears twice). Gift box with ID 1 was sold without the offer (appears once). Hence, the answer is 1.

---

#### Test Case 2
**Input:**
```
7
4 1 2 1 2 4 5
```
**Output:**
```
5
```
**Explanation:** Gift boxes with IDs 4, 1, and 2 each appear twice (sold under BOGO). Gift box with ID 5 appears only once, so it's the unique one sold without the offer.

---

#### Test Case 3
**Input:**
```
1
99
```
**Output:**
```
99
```
**Explanation:** There's only one gift box in the register with ID 99. Since it appears only once, it's the unique gift box sold without the BOGO offer.

---

#### Test Case 4
**Input:**
```
5
1000 500 1000 500 777
```
**Output:**
```
777
```
**Explanation:** Gift boxes 1000 and 500 appear twice each. Gift box 777 appears only once, making it the unique one.

---

#### Test Case 5
**Input:**
```
9
-5 10 -5 20 10 20 -100 30 30
```
**Output:**
```
-100
```
**Explanation:** This test case includes negative gift box IDs (representing special festive edition boxes with negative serial numbers). All IDs except -100 appear twice. Hence, -100 is the unique gift box.

---

#### Test Case 6
**Input:**
```
5
0 1 0 1 -1
```
**Output:**
```
-1
```
**Explanation:** Gift boxes with IDs 0 and 1 appear twice. The gift box with ID -1 appears only once, so it's the answer.

---

#### Test Case 7
**Input:**
```
11
100 200 300 400 500 100 200 300 400 500 999
```
**Output:**
```
999
```
**Explanation:** All gift box IDs from 100 to 500 appear exactly twice. Only 999 appears once, making it the unique gift box sold without the BOGO scheme.

---

### Solutions

#### Python

```python
class Solution:
    def findUniqueGift(self, gifts: list[int]) -> int:
        # Start your solution here
        result = 0
        for gift_id in gifts:
            result ^= gift_id
        return result
        # End your solution


def main():
    n = int(input())
    gifts = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.findUniqueGift(gifts)
    print(result)


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
    int findUniqueGift(vector<int>& gifts) {
        // Start your solution here
        int result = 0;
        for (int giftId : gifts) {
            result ^= giftId;
        }
        return result;
        // End your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> gifts(n);
    for (int i = 0; i < n; i++) {
        cin >> gifts[i];
    }
    
    Solution sol;
    cout << sol.findUniqueGift(gifts) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.Scanner;

class Solution {
    public int findUniqueGift(int[] gifts) {
        // Start your solution here
        int result = 0;
        for (int giftId : gifts) {
            result ^= giftId;
        }
        return result;
        // End your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] gifts = new int[n];
        
        for (int i = 0; i < n; i++) {
            gifts[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findUniqueGift(gifts));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def findUniqueGift(self, gifts: list[int]) -> int:
        # Start your solution here
        
        
        
        # End your solution
        pass


def main():
    n = int(input())
    gifts = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.findUniqueGift(gifts)
    print(result)


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
    int findUniqueGift(vector<int>& gifts) {
        // Start your solution here
        
        
        
        // End your solution
        return 0;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> gifts(n);
    for (int i = 0; i < n; i++) {
        cin >> gifts[i];
    }
    
    Solution sol;
    cout << sol.findUniqueGift(gifts) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.Scanner;

class Solution {
    public int findUniqueGift(int[] gifts) {
        // Start your solution here
        
        
        
        // End your solution
        return 0;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] gifts = new int[n];
        
        for (int i = 0; i < n; i++) {
            gifts[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.findUniqueGift(gifts));
        
        sc.close();
    }
}
```
