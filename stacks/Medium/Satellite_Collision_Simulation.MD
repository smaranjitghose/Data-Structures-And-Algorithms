# Satellite Collision Simulation

### Problem Statement

ISRO's Mission Control in Sriharikota is simulating satellite collisions in a debris field. Satellites move in a straight line. Positive values move right, negative values move left. The absolute value represents the satellite's mass.

When two satellites collide, the smaller one is destroyed. If both are equal, both are destroyed. Satellites moving in the same direction never meet.

Given an array `satellites` representing the mass and direction of each satellite, find the state of satellites after all collisions.

### Input Format

- The first line contains an integer `n`, the number of satellites.
- The second line contains `n` space-separated integers (positive = right, negative = left).

### Output Format

- Print the remaining satellites as space-separated integers, or "empty" if none survive.

### Constraints

- `2 <= n <= 10^4`
- `-1000 <= satellites[i] <= 1000`
- `satellites[i] != 0`

### Test Cases

#### Test Case 1
**Input:**
```
3
5 10 -5
```
**Output:**
```
5 10
```
**Explanation:** 10 and -5 collide. 10 survives (larger). 5 and 10 move right, no collision between them.

---

#### Test Case 2
**Input:**
```
2
8 -8
```
**Output:**
```
empty
```
**Explanation:** 8 and -8 collide. Equal mass, both destroyed.

---

#### Test Case 3
**Input:**
```
3
10 2 -5
```
**Output:**
```
10
```
**Explanation:** 2 and -5 collide, -5 wins (mass 5 > 2). 10 and -5 collide, 10 wins (mass 10 > 5).

---

#### Test Case 4
**Input:**
```
3
-2 -1 1
```
**Output:**
```
-2 -1 1
```
**Explanation:** -2 and -1 move left, 1 moves right. They diverge, no collision.

---

#### Test Case 5
**Input:**
```
4
1 -1 2 -2
```
**Output:**
```
empty
```
**Explanation:** 1 and -1 collide (both destroyed). 2 and -2 collide (both destroyed). None remain.

---

#### Test Case 6
**Input:**
```
5
5 6 7 -8 -9
```
**Output:**
```
-9
```
**Explanation:** -8 destroys 7. -8 destroys 6. -8 destroys 5. Then -9 moves left (no collision with anything).

---

#### Test Case 7
**Input:**
```
4
-5 5 -5 5
```
**Output:**
```
-5 5
```
**Explanation:** -5 moves left (no collision). 5 and -5 collide (equal, both destroyed). 5 at end survives.

---

### Solutions

#### Python

```python
class Solution:
    def asteroidCollision(self, satellites: list[int]) -> list[int]:
        # start your solution
        stack = []
        
        for sat in satellites:
            alive = True
            
            while alive and stack and sat < 0 < stack[-1]:
                # Collision: sat moving left, top of stack moving right
                if stack[-1] < -sat:
                    # Current satellite wins
                    stack.pop()
                elif stack[-1] == -sat:
                    # Both destroyed
                    stack.pop()
                    alive = False
                else:
                    # Stack satellite wins
                    alive = False
            
            if alive:
                stack.append(sat)
        
        return stack
        # end your solution


def main():
    n = int(input())
    satellites = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.asteroidCollision(satellites)
    
    if result:
        print(' '.join(map(str, result)))
    else:
        print("empty")


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
    vector<int> asteroidCollision(vector<int>& satellites) {
        // start your solution
        vector<int> stack;
        
        for (int sat : satellites) {
            bool alive = true;
            
            while (alive && !stack.empty() && sat < 0 && stack.back() > 0) {
                // Collision: sat moving left, top of stack moving right
                if (stack.back() < -sat) {
                    // Current satellite wins
                    stack.pop_back();
                } else if (stack.back() == -sat) {
                    // Both destroyed
                    stack.pop_back();
                    alive = false;
                } else {
                    // Stack satellite wins
                    alive = false;
                }
            }
            
            if (alive) {
                stack.push_back(sat);
            }
        }
        
        return stack;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> satellites(n);
    for (int i = 0; i < n; i++) {
        cin >> satellites[i];
    }
    
    Solution sol;
    vector<int> result = sol.asteroidCollision(satellites);
    
    if (result.empty()) {
        cout << "empty" << endl;
    } else {
        for (int i = 0; i < result.size(); i++) {
            cout << result[i];
            if (i < result.size() - 1) cout << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] asteroidCollision(int[] satellites) {
        // start your solution
        Stack<Integer> stack = new Stack<>();
        
        for (int sat : satellites) {
            boolean alive = true;
            
            while (alive && !stack.isEmpty() && sat < 0 && stack.peek() > 0) {
                // Collision: sat moving left, top of stack moving right
                if (stack.peek() < -sat) {
                    // Current satellite wins
                    stack.pop();
                } else if (stack.peek() == -sat) {
                    // Both destroyed
                    stack.pop();
                    alive = false;
                } else {
                    // Stack satellite wins
                    alive = false;
                }
            }
            
            if (alive) {
                stack.push(sat);
            }
        }
        
        int[] result = new int[stack.size()];
        for (int i = stack.size() - 1; i >= 0; i--) {
            result[i] = stack.pop();
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] satellites = new int[n];
        
        for (int i = 0; i < n; i++) {
            satellites[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.asteroidCollision(satellites);
        
        if (result.length == 0) {
            System.out.println("empty");
        } else {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < result.length; i++) {
                sb.append(result[i]);
                if (i < result.length - 1) sb.append(" ");
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def asteroidCollision(self, satellites: list[int]) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    satellites = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.asteroidCollision(satellites)
    
    if result:
        print(' '.join(map(str, result)))
    else:
        print("empty")


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
    vector<int> asteroidCollision(vector<int>& satellites) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> satellites(n);
    for (int i = 0; i < n; i++) {
        cin >> satellites[i];
    }
    
    Solution sol;
    vector<int> result = sol.asteroidCollision(satellites);
    
    if (result.empty()) {
        cout << "empty" << endl;
    } else {
        for (int i = 0; i < result.size(); i++) {
            cout << result[i];
            if (i < result.size() - 1) cout << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int[] asteroidCollision(int[] satellites) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] satellites = new int[n];
        
        for (int i = 0; i < n; i++) {
            satellites[i] = sc.nextInt();
        }
        
        Solution sol = new Solution();
        int[] result = sol.asteroidCollision(satellites);
        
        if (result.length == 0) {
            System.out.println("empty");
        } else {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < result.length; i++) {
                sb.append(result[i]);
                if (i < result.length - 1) sb.append(" ");
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```
