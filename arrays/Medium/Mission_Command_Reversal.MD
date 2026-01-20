# Mission Command Reversal

### Problem Statement

Deepak works at ISRO's Mission Control Center in Bengaluru. During satellite communication, commands are sometimes received in reversed word order due to signal processing. He needs to restore the original command sequence.

Given a string `command`, reverse the order of words. A word is a sequence of non-space characters. Return the corrected string with words separated by single spaces and no leading or trailing spaces.

### Input Format

- A single line containing the string `command`.

### Output Format

- Print the string with words in reversed order.

### Constraints

- `1 <= command.length <= 10^4`
- `command` contains English letters, digits, and spaces
- At least one word exists in `command`

### Test Cases

#### Test Case 1
**Input:**
```
launch sequence initiated
```
**Output:**
```
initiated sequence launch
```
**Explanation:** Three words identified: "launch", "sequence", "initiated". Reverse order. Join with single spaces. Result = "initiated sequence launch".

---

#### Test Case 2
**Input:**
```
  satellite online  
```
**Output:**
```
online satellite
```
**Explanation:** Leading/trailing spaces ignored. Words: "satellite", "online". Reverse order. No extra spaces in output. Result = "online satellite".

---

#### Test Case 3
**Input:**
```
orbit   correction   needed
```
**Output:**
```
needed correction orbit
```
**Explanation:** Multiple spaces treated as single separator. Words: "orbit", "correction", "needed". Reversed = "needed correction orbit".

---

#### Test Case 4
**Input:**
```
Chandrayaan
```
**Output:**
```
Chandrayaan
```
**Explanation:** Single word. Reversing word order gives same result. Output = "Chandrayaan".

---

#### Test Case 5
**Input:**
```
  Jai   Hind  
```
**Output:**
```
Hind Jai
```
**Explanation:** Strip leading/trailing spaces. Words: "Jai", "Hind". Reversed with single space. Result = "Hind Jai".

---

#### Test Case 6
**Input:**
```
Mangalyaan Mars Orbiter Mission
```
**Output:**
```
Mission Orbiter Mars Mangalyaan
```
**Explanation:** Four words, no extra spaces. Simple reversal. Result = "Mission Orbiter Mars Mangalyaan".

---

#### Test Case 7
**Input:**
```
ignition thrust nominal
```
**Output:**
```
nominal thrust ignition
```
**Explanation:** Three words: "ignition", "thrust", "nominal". Reversed order = "nominal thrust ignition".

---

### Solutions

#### Python

```python
class Solution:
    def reverseCommand(self, command: str) -> str:
        # start your solution
        words = command.split()
        return ' '.join(reversed(words))
        # end your solution


def main():
    command = input()
    
    sol = Solution()
    result = sol.reverseCommand(command)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <sstream>
#include <algorithm>
using namespace std;

class Solution {
public:
    string reverseCommand(string command) {
        // start your solution
        vector<string> words;
        stringstream ss(command);
        string word;
        
        while (ss >> word) {
            words.push_back(word);
        }
        
        reverse(words.begin(), words.end());
        
        string result;
        for (int i = 0; i < words.size(); i++) {
            if (i > 0) result += " ";
            result += words[i];
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string command;
    getline(cin, command);
    
    Solution sol;
    cout << sol.reverseCommand(command) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String reverseCommand(String command) {
        // start your solution
        String[] words = command.trim().split("\\s+");
        
        StringBuilder result = new StringBuilder();
        for (int i = words.length - 1; i >= 0; i--) {
            result.append(words[i]);
            if (i > 0) result.append(" ");
        }
        
        return result.toString();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String command = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.reverseCommand(command));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def reverseCommand(self, command: str) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    command = input()
    
    sol = Solution()
    result = sol.reverseCommand(command)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <sstream>
#include <algorithm>
using namespace std;

class Solution {
public:
    string reverseCommand(string command) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string command;
    getline(cin, command);
    
    Solution sol;
    cout << sol.reverseCommand(command) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String reverseCommand(String command) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String command = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.reverseCommand(command));
        
        sc.close();
    }
}
```
