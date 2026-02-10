# Stack

## Evaluation of expression

```java
import java.util.Scanner;
import java.util.Stack;

public class PTQ1 {
    public static int evaluate(String expr) {
        Stack<Double> stack = new Stack<>();
        double num = 0;
        char op = '+';

        for (int i = 0; i < expr.length(); i++) {
            char ch = expr.charAt(i);

            if (Character.isDigit(ch)) {
                num = num * 10 + (ch - '0');
            }

            if (!Character.isDigit(ch) || i == expr.length() - 1) {
                if (op == '+') stack.push(num);
                if (op == '-') stack.push(-num);
                if (op == '*') stack.push(stack.pop() * num);
                if (op == '/') {
                    double tempAbsValue = Math.floor(stack.pop() / num);
                    stack.push(tempAbsValue);
                }

                op = ch;
                num = 0;
            }
        }

        double result = 0;
        for (double n : stack) {
            // System.out.println(n);
            result += n;
        }
        return (int) result;
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String expr = sc.nextLine();
        System.out.println(evaluate(expr)); // Output : 21 (21.5)
    }

    
}
```
