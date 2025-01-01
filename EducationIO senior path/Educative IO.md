# Educative IO

## Basic Code review



### 0. basic expression

get the count of characters with an odd number of occurrences统计字符出现次数为奇数的字符数量。



### 1. Two Pointer

linear traverse: 

Generate a string of 𝑛*n* balanced parentheses. 不能用需要backtracking 

Find all permutations of the following set of elements: {1,2,3}{1,2,3}. 不能用需要decision tree



#### Valid Palindrome

![Screenshot 2024-07-29 at 2.35.53 PM](/Users/bban/Documents/notes/EducationIO senior path/Screenshot 2024-07-29 at 2.35.53 PM.png)

#### Sum of Three Values

Logic: 

- sort the input array in ascending order.
- Iterate over the entire sorted array to find the triplet whose sum is equal to the target
- In each iteration, make a triplet by storing the curreny array element and the other two elements using two pointers, and calculate their sum.
- Adjust the calculated sum value, until it becomes equal to the target value, by conditionally moving the pointers, low and high.
- Return True if the required sum is found. Otherwise, return FALSE.



#### Remove Nth Node from End of List

Logic: 

- Set up two pointers, left and right, at the head of linkedList
- Move the right pointer n steps forward
- Move the both right and left pointers forward untail the right pointer reaches the last node. At this point, the left pointer will pointing to the node behind the nth last node by ensuring the constant gap.
- Relink the left node to the node next to the left's next node;
- Return the head of linkedlist

### 2. Fast and Slow Pointers



#### Happy Number

![Screenshot 2024-10-07 at 9.04.08 PM](/Users/bban/Documents/notes/EducationIO senior path/Screenshot 2024-10-07 at 9.04.08 PM.png)

- Set up two pointers, slow pointers to the input number, the fast pointers to the sum of squared digits of input number;
- Start a loop until fast pointer reachs 1 or both pointers meet, indicating a cycle;
- Update the slow pointe by adding the squares of its digits, and fastPointer by adding the squares of its digits twice.
- If fastPointer equals 1, return True, otherwise, return false;

注意asci字符转换问题

int value = Character.getNumericValue(i);

Math.sqrt是平方根

Time Compexity : O(logn)

To estimate the count of numbers in a cycle, let’s consider the following two cases:

1. **Numbers with three digits:** The largest three-digit number is 999. The sum of the squares of its digits is 243. Therefore, for three-digit numbers, no number in the cycle can go beyond 243. Therefore, the time complexity in this case is given as O(243×3),* where 243 is the maximum count of numbers in a cycle and 3 is the number of digits in a three-digit number. This is why the time complexity in the case of numbers with three digits comes out to be O(1)
2. **Numbers with more than three digits:** Any number with more than three digits will lose at least one digit at every step until it becomes a three-digit number. For example, the first four-digit number that we can get in the cycle is 1053, which is the sum of the square of the digits in 9999999999999. Therefore, the time complexity of any number with more than three digits can be expressed as O(log⁡n+log⁡log⁡n+log⁡log⁡log⁡n+…) Since O*(log*n*) is the dominating term, we can write the time complexity as O(log⁡n).

### 3. Stack

#### Remove All Adjacent Duplicates In String

- Initialize a stack to store result string; Traverse every character in the string;
- In each iteration, if the string character is the same as the char at the top of the stack, pop the character from the stack.
- If the current character is diff from the top of the stack, push current char on the top of string.
- After all iteration, generate a string from the characters from the stack

```java
import java.util.*;
public class Main{
    public static String removeDuplicates(String s) {
        // 使用泛型 Stack<Character> 避免不安全操作警告
        Stack<Character> temp = new Stack<>();
        
        for (char i : s.toCharArray()) {
            if (temp.isEmpty()) {
                temp.push(i);
            } else {
                char curTop = temp.peek();
                
                if (curTop == i) {
                    temp.pop();  // 如果当前字符和栈顶相同，弹出栈顶元素
                } else {
                    temp.push(i);  // 如果不同，压入当前字符
                }
            }
        }
        
        // 构建最终结果
        int n = temp.size();
        char[] result = new char[n];//使用new char
        for (int i = n - 1; i >= 0; i--) {
            char cur = temp.pop();
            result[i] = cur;
        }
        
        return new String(result);  // 将字符数组转换为字符串
    }
}
```

#### Basic Calculator

Given a string containing an arithmetic expression, implement a basic calculator that evaluates the expression string. The expression string can contain integer numeric values and should be able to handle the “+” and “-” operators, as well as “()” parentheses.

**Constraints:**

Let `s` be the expression string. We can assume the following constraints:

- 1≤ `s.length` ≤3×103
- `s` consists of digits, “+”, “-”, “(”, and “)”.
- `s` represents a valid expression.
- “+” is not used as a unary operation ( +1 and +(2+3) are invalid).
- “-” could be used as a unary operation (−1 and −(2+3) are valid).
- There will be no two consecutive operators in the input.
- Every number and running calculation will fit in a signed 32-bit integer.

Logic:

- Initialize a stack to manage nested expressions and three variables for the current number, sign value and result;
- Iterate through the input string to process the equation. Determine if the charater is digit, parenthesis, or operator
- when encouter a digit, update the number variable by appending the digit to it
- For opterators, compute the left expression using the current sign and update the result
- If an opening parenthesis is found, push the current result and sign onto stack for nexted expressions. For a closing parenthesis, compute the expression with in it andu update the result

``` java
import java.util.*;

public class Main{
    public static int calculator(String expression) {
        Stack<Integer> temp = new Stack<>();
        int result = 0;
        int signValue = 1;
        int number = 0;
        int second_value = 0;
        
        for(char i : expression.toCharArray()){
          if(Character.isDigit(i)){
            number = number * 10 + Character.getNumericValue(i);
          }else if(i == '-' || i == '+'){
            result += signValue * number;
            if(i == '-'){
              signValue = -1;
            }else{
              signValue = 1;
            }
            number = 0;
          }else if(i == '('){
            temp.push(result);
            temp.push(signValue);
            result = 0;
            signValue = 1;
          }else if(i == ')'){
            result += signValue * number;
            result *= temp.pop();
            second_value = temp.pop();
            result += second_value;
            number = 0;
            signValue = 1;
          }
        }
        // Replace this placeholder return statement with your code
        return result += signValue * number;
    }
}
```

### 4. HashMap

#### Create a new HashMap 

创建一个2000size的bucket数组，对key取hash值，放到数组中bucket(arrayList中kvPair)

    public DesignHashMap() {
        keySpace = 2069;
        buckets = new Bucket[keySpace];
        for (int i = 0; i < keySpace; i++) {
            buckets[i] = new Bucket();
        }
    }
    这段代码的作用是在创建一个大小为 keySpace 的 buckets 数组，并初始化数组中的每个元素为一个新的 Bucket 实例。需要遍历的原因是数组只是分配了空间（容纳 Bucket 对象的引用），但并没有真正创建 Bucket 实例。因此，你必须通过遍历数组，在每个位置创建并分配 Bucket 实例。

#### Valid Anagram比较时注意

``` 
Map<Character, Integer> map = new HashMap<>();
```

其中get出来比较的时候比如 map1.get(i) !=  map2.get(i) 是不对的，比较的是引用地址而不是真实value

Java 对 Integer 对象有一个缓存池。当你通过自动装箱（auto-boxing）或某些构造方法创建 Integer 对象时，**如果值在范围** -128 **到** 127 **之间，Java 会从缓存池中返回相同的对象**，而不会创建新的实例。

也可直接使用 数组更快效率更高

```java
    public static boolean isAnagram(String str1, String str2) {
        if (str1.length() != str2.length()) {
            return false; // 如果长度不同，直接返回 false
        }

        // 用两个长度为 26 的数组来统计字符频率
        int[] count1 = new int[26];
        int[] count2 = new int[26];

        // 遍历两个字符串，分别统计字符出现次数
        for (int i = 0; i < str1.length(); i++) {
            count1[str1.charAt(i) - 'a']++;
            count2[str2.charAt(i) - 'a']++;
        }

        // 比较两个频率数组
        for (int i = 0; i < 26; i++) {
            if (count1[i] != count2[i]) {
                return false;
            }
        }

        return true;
    }
```

#### Maximum Frequency Stack

- **FreqStack**: This is a class used to declare a frequency stack.

- **Push(value)**: This is used to push an integer data onto the top of the stack.

- **Pop()**: This is used to remove and return the most frequent element in the stack.

  ```java
  import java.util.*;
  class FreqStack {
      Map<Integer, Integer> freqMap;
      Map<Integer, Stack<Integer>> groupMap;
      int maxFreq = 0;
      public FreqStack() {
          freqMap = new HashMap<>();
          groupMap = new HashMap<>();
      }
  
      public void push(int value) {
          if(value < 0){
            throw new IllegalArgumentException("need check your value")
          }
          // update freqMap
          int freq = freqMap.getOrDefault(value, 0) + 1;
          freqMap.put(value, freq);
          // update groupMap
          groupMap.computeIfAbsent(freq, key -> new Stack<>()).push(value);
          if(freq > maxFreq){
            maxFreq = freq;
          }
      }
  
      public int pop() {
          if (maxFreq <= 0 || !groupMap.containsKey(maxFreq)) {
              throw new IllegalStateException("No elements in the stack to pop");
          }
          Stack<Integer> stack = groupMap.get(maxFreq);
          int value = stack.pop();
          if (stack.isEmpty()) {
              groupMap.remove(maxFreq);
              maxFreq--;
          }
          freqMap.put(value, freqMap.get(value) - 1);
          if (freqMap.get(value) == 0) {
              freqMap.remove(value);
          }
          return value;
      }
  }
  ```

  
