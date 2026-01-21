# Parliament Voting Round

### Problem Statement

In the Indian Parliament, Lok Sabha members from two parties (Ruling 'R' and Opposition 'O') vote in rounds. Each member can either ban one member from the opposite party or vote if all opponents are banned.

In each round, members vote in order. A member can:
1. Ban one upcoming member from the opposing party (they lose all rights this and future rounds)
2. Announce victory if all opponents are already banned

Given a string representing the party sequence, determine which party wins.

### Input Format

- A single line containing a string of 'R' and 'O' characters representing party members.

### Output Format

- Print "Ruling" if R wins, or "Opposition" if O wins.

### Constraints

- `1 <= senate.length <= 10^4`
- `senate[i]` is either 'R' or 'O'

### Test Cases

#### Test Case 1
**Input:**
```
RD
```
**Output:**
```
Ruling
```
**Explanation:** R bans O. Only R remains. Ruling party wins.

---

#### Test Case 2
**Input:**
```
RDD
```
**Output:**
```
Opposition
```
**Explanation:** R bans first O. Second O bans R. Only O remains. Opposition wins.

---

#### Test Case 3
**Input:**
```
RROO
```
**Output:**
```
Ruling
```
**Explanation:** R1 bans O1, R2 bans O2. Both Os banned. Ruling wins.

---

#### Test Case 4
**Input:**
```
OORR
```
**Output:**
```
Opposition
```
**Explanation:** O1 bans R1, O2 bans R2. Both Rs banned. Opposition wins.

---

#### Test Case 5
**Input:**
```
RORO
```
**Output:**
```
Ruling
```
**Explanation:** R1 bans O1, O2 bans R1 (already acted), R2 (next round) bans O2. Ruling wins.

---

#### Test Case 6
**Input:**
```
OROR
```
**Output:**
```
Opposition
```
**Explanation:** O1 bans R1, R2 bans O2, O2 (banned) can't act. Round 2: O1 bans R2. Opposition wins.

---

#### Test Case 7
**Input:**
```
RRRROOOO
```
**Output:**
```
Ruling
```
**Explanation:** Each R bans an O before Os get to act. Ruling wins with 4 bans.

---

### Solutions

#### Python

```python
from collections import deque

class Solution:
    def predictPartyVictory(self, senate: str) -> str:
        # start your solution
        ruling = deque()
        opposition = deque()
        n = len(senate)
        
        for i, c in enumerate(senate):
            if c == 'R':
                ruling.append(i)
            else:
                opposition.append(i)
        
        while ruling and opposition:
            r_idx = ruling.popleft()
            o_idx = opposition.popleft()
            
            # The one with smaller index bans the other
            # Winner goes to end of queue with new index
            if r_idx < o_idx:
                ruling.append(r_idx + n)
            else:
                opposition.append(o_idx + n)
        
        return "Ruling" if ruling else "Opposition"
        # end your solution


def main():
    senate = input().strip()
    # Convert O to D for compatibility with standard problem, or use as is
    # Here we assume input uses R and O
    senate = senate.replace('D', 'O')  # In case D is used for Opposition
    
    sol = Solution()
    result = sol.predictPartyVictory(senate)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <queue>
#include <string>
using namespace std;

class Solution {
public:
    string predictPartyVictory(string senate) {
        // start your solution
        queue<int> ruling, opposition;
        int n = senate.size();
        
        for (int i = 0; i < n; i++) {
            if (senate[i] == 'R') {
                ruling.push(i);
            } else {
                opposition.push(i);
            }
        }
        
        while (!ruling.empty() && !opposition.empty()) {
            int r_idx = ruling.front(); ruling.pop();
            int o_idx = opposition.front(); opposition.pop();
            
            if (r_idx < o_idx) {
                ruling.push(r_idx + n);
            } else {
                opposition.push(o_idx + n);
            }
        }
        
        return ruling.empty() ? "Opposition" : "Ruling";
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string senate;
    getline(cin, senate);
    
    // Replace D with O if needed
    for (char& c : senate) {
        if (c == 'D') c = 'O';
    }
    
    Solution sol;
    cout << sol.predictPartyVictory(senate) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String predictPartyVictory(String senate) {
        // start your solution
        Queue<Integer> ruling = new LinkedList<>();
        Queue<Integer> opposition = new LinkedList<>();
        int n = senate.length();
        
        for (int i = 0; i < n; i++) {
            if (senate.charAt(i) == 'R') {
                ruling.offer(i);
            } else {
                opposition.offer(i);
            }
        }
        
        while (!ruling.isEmpty() && !opposition.isEmpty()) {
            int rIdx = ruling.poll();
            int oIdx = opposition.poll();
            
            if (rIdx < oIdx) {
                ruling.offer(rIdx + n);
            } else {
                opposition.offer(oIdx + n);
            }
        }
        
        return ruling.isEmpty() ? "Opposition" : "Ruling";
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String senate = sc.nextLine().replace('D', 'O');
        
        Solution sol = new Solution();
        System.out.println(sol.predictPartyVictory(senate));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
from collections import deque

class Solution:
    def predictPartyVictory(self, senate: str) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    senate = input().strip()
    senate = senate.replace('D', 'O')
    
    sol = Solution()
    result = sol.predictPartyVictory(senate)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <queue>
#include <string>
using namespace std;

class Solution {
public:
    string predictPartyVictory(string senate) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string senate;
    getline(cin, senate);
    
    for (char& c : senate) {
        if (c == 'D') c = 'O';
    }
    
    Solution sol;
    cout << sol.predictPartyVictory(senate) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String predictPartyVictory(String senate) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String senate = sc.nextLine().replace('D', 'O');
        
        Solution sol = new Solution();
        System.out.println(sol.predictPartyVictory(senate));
        
        sc.close();
    }
}
```
