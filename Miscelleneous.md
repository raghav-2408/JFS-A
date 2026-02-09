## Temperature Problem

```java
import java.util.Scanner;
public class Q2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String ch = sc.nextLine(); // CtoF or FtoC

        switch (ch){
            case "CtoF":
                double temp1 = sc.nextDouble();
                double val1 = (temp1 * 9/5) + 32;
                System.out.printf("Value : %.2f",  val1);
                break;
            case "FtoC":
                double temp2 = sc.nextDouble();
                double val2 = (temp2 - 32) * 5/9;
                System.out.printf("Value : %.2f", val2);
                break;
            default:
                break;
        }
    }
}
```
