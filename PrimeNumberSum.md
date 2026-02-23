## Magic Sum (eg : for Prime N = 17 sum of primes should be the Prime N-> 2 + 3 + 5 + 7 = 17 )

```java
import java.util.ArrayList;

public class Lists {

  public static boolean isPrime(int N) {
    if (N <= 1) return false;

    for (int i = 2; i <= Math.sqrt(N); i++) {
      if (N % i == 0) return false;
    }
    return true;
  }

  public static void main(String[] args) {
    
    int N = 17;
    ArrayList<Integer> primes = new ArrayList<>();

    int sum = 0;
    for (int i = 2; i < N; i++) {
      if (isPrime(i)){
        sum += i;
        primes.add(i);
      }
    }

    int checkSum = 0;

    ArrayList<Integer> sumPrimes = new ArrayList<>();

    for(int i : primes) {
      checkSum += i;
     
      if (checkSum == N) {
        System.out.println("Yes");
        break;
      }
    }

    

  }
}
```
