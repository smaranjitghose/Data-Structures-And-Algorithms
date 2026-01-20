# IPL Batting Order Rotation

### Problem Statement

Vikram is the coach of a franchise in the Indian Premier League (IPL). Before a crucial match at Wankhede Stadium in Mumbai, he decides to rotate the batting order to confuse the opponent's bowling strategy.

Given an array `players` representing jersey numbers of batsmen in the current order and an integer `k`, rotate the array to the right by `k` positions. After rotation, the last `k` players move to the front.

Perform the rotation in-place with O(1) extra space.

### Input Format

- The first line contains two integers `n` and `k` — the number of players and rotation count.
- The second line contains `n` space-separated integers representing player jersey numbers.

### Output Format

- Print the rotated array as space-separated integers.

### Constraints

- `1 <= n <= 10^5`
- `0 <= k <= 10^5`
- `-2^31 <= players[i] <= 2^31 - 1`

### Test Cases

#### Test Case 1
**Input:**
```
7 3
1 2 3 4 5 6 7
```
**Output:**
```
5 6 7 1 2 3 4
```
**Explanation:** Rotate right by 3: last 3 players [5, 6, 7] move to front.

---

#### Test Case 2
**Input:**
```
4 2
-1 -100 3 99
```
**Output:**
```
3 99 -1 -100
```
**Explanation:** Rotate right by 2: last 2 elements [3, 99] move to front.

---

#### Test Case 3
**Input:**
```
5 0
10 20 30 40 50
```
**Output:**
```
10 20 30 40 50
```
**Explanation:** No rotation needed when k = 0.

---

#### Test Case 4
**Input:**
```
3 3
7 18 45
```
**Output:**
```
7 18 45
```
**Explanation:** Rotating by array length results in same order.

---

#### Test Case 5
**Input:**
```
5 7
11 22 33 44 55
```
**Output:**
```
44 55 11 22 33
```
**Explanation:** k = 7, n = 5. Effective rotation = 7 % 5 = 2.

---

#### Test Case 6
**Input:**
```
1 5
42
```
**Output:**
```
42
```
**Explanation:** Single element array remains unchanged regardless of k.

---

#### Test Case 7
**Input:**
```
6 4
8 16 24 32 40 48
```
**Output:**
```
24 32 40 48 8 16
```
**Explanation:** Last 4 elements [24, 32, 40, 48] move to front.

---

### Solutions

#### Python

```python
class Solution:
    def rotatePlayers(self, players: list[int], k: int) -> None:
        # start your solution
        n = len(players)
        k = k % n
        
        def reverse(left, right):
            while left < right:
                players[left], players[right] = players[right], players[left]
                left += 1
                right -= 1
        
        reverse(0, n - 1)
        reverse(0, k - 1)
        reverse(k, n - 1)
        # end your solution


def main():
    first_line = input().split()
    n, k = int(first_line[0]), int(first_line[1])
    players = list(map(int, input().split()))
    
    sol = Solution()
    sol.rotatePlayers(players, k)
    print(' '.join(map(str, players)))


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
    void rotatePlayers(vector<int>& players, int k) {
        // start your solution
        int n = players.size();
        k = k % n;
        
        reverse(players.begin(), players.end());
        reverse(players.begin(), players.begin() + k);
        reverse(players.begin() + k, players.end());
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> players(n);
    for (int i = 0; i < n; i++) {
        cin >> players[i];
    }
    
    Solution sol;
    sol.rotatePlayers(players, k);
    
    for (int i = 0; i < n; i++) {
        cout << players[i];
        if (i < n - 1) cout << " ";
    }
    cout << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public void rotatePlayers(int[] players, int k) {
        // start your solution
        int n = players.length;
        k = k % n;
        
        reverse(players, 0, n - 1);
        reverse(players, 0, k - 1);
        reverse(players, k, n - 1);
        // end your solution
    }
    
    private void reverse(int[] arr, int left, int right) {
        while (left < right) {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        int[] players = new int[n];
        
        for (int i = 0; i < n; i++) {
            players[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        sol.rotatePlayers(players, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            sb.append(players[i]);
            if (i < n - 1) sb.append(" ");
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
    def rotatePlayers(self, players: list[int], k: int) -> None:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    n, k = int(first_line[0]), int(first_line[1])
    players = list(map(int, input().split()))
    
    sol = Solution()
    sol.rotatePlayers(players, k)
    print(' '.join(map(str, players)))


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
    void rotatePlayers(vector<int>& players, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<int> players(n);
    for (int i = 0; i < n; i++) {
        cin >> players[i];
    }
    
    Solution sol;
    sol.rotatePlayers(players, k);
    
    for (int i = 0; i < n; i++) {
        cout << players[i];
        if (i < n - 1) cout << " ";
    }
    cout << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public void rotatePlayers(int[] players, int k) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        int[] players = new int[n];
        
        for (int i = 0; i < n; i++) {
            players[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        sol.rotatePlayers(players, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            sb.append(players[i]);
            if (i < n - 1) sb.append(" ");
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```
