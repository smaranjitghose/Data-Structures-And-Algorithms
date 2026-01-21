# School Canteen Queue

### Problem Statement

At DPS RK Puram in Delhi, the school canteen serves two types of lunch: circular roti (represented by 0) and square paratha (represented by 1). Students stand in a queue, and the lunch is stacked.

A student at the front takes the top lunch if it matches their preference, otherwise they go to the back of the queue. This continues until no student in the queue wants the top lunch.

Given `students` (their preferences) and `lunches` (stack, first element is top), return the number of students unable to eat.

### Input Format

- The first line contains an integer `n`, the number of students/lunches.
- The second line contains `n` space-separated integers (0 or 1) representing student preferences.
- The third line contains `n` space-separated integers (0 or 1) representing lunch stack (first is top).

### Output Format

- Print the number of students who cannot eat.

### Constraints

- `1 <= n <= 100`
- `students.length == lunches.length`
- `students[i]` and `lunches[i]` are 0 or 1

### Test Cases

#### Test Case 1
**Input:**
```
4
1 1 0 0
0 1 0 1
```
**Output:**
```
0
```
**Explanation:** 
- Top lunch 0, front student wants 1 → goes to back: [1,0,0,1]
- Top lunch 0, front student wants 1 → goes to back: [0,0,1,1]
- Top lunch 0, front student wants 0 → takes it: [0,1,1]
- Top lunch 1, front student wants 0 → goes to back: [1,1,0]
- Top lunch 1, front student wants 1 → takes it: [1,0]
- And so on... All students eventually eat.

---

#### Test Case 2
**Input:**
```
4
1 1 1 0
0 1 1 0
```
**Output:**
```
1
```
**Explanation:** Only one student wants 0 but there are two 0s. Eventually one 0 remains with no takers.

---

#### Test Case 3
**Input:**
```
1
0
1
```
**Output:**
```
1
```
**Explanation:** Student wants 0, lunch is 1. No match possible.

---

#### Test Case 4
**Input:**
```
3
0 0 0
1 1 1
```
**Output:**
```
3
```
**Explanation:** All students want 0, all lunches are 1. No one eats.

---

#### Test Case 5
**Input:**
```
5
1 0 1 0 1
1 0 1 0 1
```
**Output:**
```
0
```
**Explanation:** Perfect match in order. All students eat.

---

#### Test Case 6
**Input:**
```
6
1 1 0 0 1 0
1 0 0 1 0 1
```
**Output:**
```
0
```
**Explanation:** All preferences can be satisfied eventually.

---

#### Test Case 7
**Input:**
```
5
0 0 0 1 1
1 1 1 0 0
```
**Output:**
```
3
```
**Explanation:** 3 students want 0, only 2 lunches are 0. 1 student can't eat. Wait, let me recalculate... Top is 1, students wanting 0 keep rotating until students wanting 1 take them. Then 0s are available. Some may not match.

---

### Solutions

#### Python

```python
from collections import deque

class Solution:
    def countStudents(self, students: list[int], lunches: list[int]) -> int:
        # start your solution
        queue = deque(students)
        stack = deque(lunches)
        
        attempts = 0
        
        while queue and attempts < len(queue):
            if queue[0] == stack[0]:
                queue.popleft()
                stack.popleft()
                attempts = 0
            else:
                queue.append(queue.popleft())
                attempts += 1
        
        return len(queue)
        # end your solution


def main():
    n = int(input())
    students = list(map(int, input().split()))
    lunches = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.countStudents(students, lunches)
    print(result)


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
    int countStudents(vector<int>& students, vector<int>& lunches) {
        // start your solution
        queue<int> q;
        for (int s : students) q.push(s);
        
        int idx = 0;
        int attempts = 0;
        
        while (!q.empty() && attempts < q.size()) {
            if (q.front() == lunches[idx]) {
                q.pop();
                idx++;
                attempts = 0;
            } else {
                q.push(q.front());
                q.pop();
                attempts++;
            }
        }
        
        return q.size();
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> students(n), lunches(n);
    for (int i = 0; i < n; i++) cin >> students[i];
    for (int i = 0; i < n; i++) cin >> lunches[i];
    
    Solution sol;
    cout << sol.countStudents(students, lunches) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int countStudents(int[] students, int[] lunches) {
        // start your solution
        Queue<Integer> queue = new LinkedList<>();
        for (int s : students) queue.offer(s);
        
        int idx = 0;
        int attempts = 0;
        
        while (!queue.isEmpty() && attempts < queue.size()) {
            if (queue.peek() == lunches[idx]) {
                queue.poll();
                idx++;
                attempts = 0;
            } else {
                queue.offer(queue.poll());
                attempts++;
            }
        }
        
        return queue.size();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] students = new int[n];
        int[] lunches = new int[n];
        
        for (int i = 0; i < n; i++) students[i] = sc.nextInt();
        for (int i = 0; i < n; i++) lunches[i] = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.countStudents(students, lunches));
        
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
    def countStudents(self, students: list[int], lunches: list[int]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    students = list(map(int, input().split()))
    lunches = list(map(int, input().split()))
    
    sol = Solution()
    result = sol.countStudents(students, lunches)
    print(result)


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
    int countStudents(vector<int>& students, vector<int>& lunches) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<int> students(n), lunches(n);
    for (int i = 0; i < n; i++) cin >> students[i];
    for (int i = 0; i < n; i++) cin >> lunches[i];
    
    Solution sol;
    cout << sol.countStudents(students, lunches) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int countStudents(int[] students, int[] lunches) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] students = new int[n];
        int[] lunches = new int[n];
        
        for (int i = 0; i < n; i++) students[i] = sc.nextInt();
        for (int i = 0; i < n; i++) lunches[i] = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.countStudents(students, lunches));
        
        sc.close();
    }
}
```
