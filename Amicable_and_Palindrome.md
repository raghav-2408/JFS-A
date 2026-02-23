```java

import java.util.Scanner;

public class Lists {


  
  public static int sumOfDivisors(int N) {
    int sum = 0;
    for(int i = 1; i <= N/2; i++) {
      if (N % i == 0) {
        sum+=i;
      }
    }
    return sum;
  }

  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int n1 = sc.nextInt();
    int n2 = sc.nextInt();

    int sum1 = sumOfDivisors(n1);
    int sum2 = sumOfDivisors(n2);

    if (sum1 == n2 && sum2 == n1) {
      System.out.println("Amicable numbers");
    }else{
      System.out.println("Not an Amicable numbers");
    }

    String res = "" + (n1 * n2);
    StringBuilder sb = new StringBuilder(res);

    System.out.println(res);
    System.out.println(sb.reverse());
    if(res.equals(sb.reverse().toString())){
      System.out.println("Palindrome");
    }else{
      System.out.println("Not a palindrome");
    }
  }
}
```
