# RTO Palindrome Check

### Problem Statement

Amit works at the Regional Transport Office (RTO) in Ahmedabad. Some vehicle owners request special "palindrome" registration numbers that read the same forwards and backwards.

Given a string `registration`, determine if it is a valid palindrome. Consider only alphanumeric characters and ignore cases.

### Input Format

- A single line containing the string `registration`.

### Output Format

- Print `true` if the string is a valid palindrome, otherwise print `false`.

### Constraints

- `1 <= registration.length <= 2 * 10^5`
- `registration` consists of printable ASCII characters

### Test Cases

#### Test Case 1
**Input:**
```
GJ01AB1010BA10JG
```
**Output:**
```
true
```
**Explanation:** Ignoring case, the registration "GJ01AB1010BA10JG" reads the same forwards and backwards.

---

#### Test Case 2
**Input:**
```
MH12CD5678
```
**Output:**
```
false
```
**Explanation:** "MH12CD5678" does not read the same backwards.

---

#### Test Case 3
**Input:**
```
KA 05 MN 2002 NM 50 AK
```
**Output:**
```
true
```
**Explanation:** After removing spaces: "KA05MN2002NM50AK" is a palindrome when case is ignored.

---

#### Test Case 4
**Input:**
```
 
```
**Output:**
```
true
```
**Explanation:** Empty string (only space) is considered a valid palindrome.

---

#### Test Case 5
**Input:**
```
A
```
**Output:**
```
true
```
**Explanation:** Single character is always a palindrome.

---

#### Test Case 6
**Input:**
```
DL9CD99DC9LD
```
**Output:**
```
true
```
**Explanation:** Delhi registration "DL9CD99DC9LD" reads same forwards and backwards.

---

#### Test Case 7
**Input:**
```
TN22 ZZ 1234
```
**Output:**
```
false
```
**Explanation:** After removing spaces: "TN22ZZ1234" is not a palindrome.

---

### Solutions

#### Python

```python
class Solution:
    def isPalindrome(self, registration: str) -> bool:
        # start your solution
        left, right = 0, len(registration) - 1
        
        while left < right:
            while left < right and not registration[left].isalnum():
                left += 1
            while left < right and not registration[right].isalnum():
                right -= 1
            
            if registration[left].lower() != registration[right].lower():
                return False
            
            left += 1
            right -= 1
        
        return True
        # end your solution


def main():
    registration = input()
    
    sol = Solution()
    result = sol.isPalindrome(registration)
    print("true" if result else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
using namespace std;

class Solution {
public:
    bool isPalindrome(string registration) {
        // start your solution
        int left = 0, right = registration.length() - 1;
        
        while (left < right) {
            while (left < right && !isalnum(registration[left])) {
                left++;
            }
            while (left < right && !isalnum(registration[right])) {
                right--;
            }
            
            if (tolower(registration[left]) != tolower(registration[right])) {
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string registration;
    getline(cin, registration);
    
    Solution sol;
    cout << (sol.isPalindrome(registration) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean isPalindrome(String registration) {
        // start your solution
        int left = 0, right = registration.length() - 1;
        
        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(registration.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(registration.charAt(right))) {
                right--;
            }
            
            if (Character.toLowerCase(registration.charAt(left)) != Character.toLowerCase(registration.charAt(right))) {
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String registration = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.isPalindrome(registration) ? "true" : "false");
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def isPalindrome(self, registration: str) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    registration = input()
    
    sol = Solution()
    result = sol.isPalindrome(registration)
    print("true" if result else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
using namespace std;

class Solution {
public:
    bool isPalindrome(string registration) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string registration;
    getline(cin, registration);
    
    Solution sol;
    cout << (sol.isPalindrome(registration) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean isPalindrome(String registration) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String registration = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.isPalindrome(registration) ? "true" : "false");
        
        sc.close();
    }
}
```
