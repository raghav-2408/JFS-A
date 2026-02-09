# Arrays

## Print the second largest element

```java
import java.util.Scanner;
import java.util.ArrayList;
import java.util.Collections;

public class Arrays {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayList<Integer> arr = new ArrayList<Integer>();
        
        int N = sc.nextInt();

        for(int i=0; i<N; i++){
            arr.add(sc.nextInt());
        }

        Collections.sort(arr, Collections.reverseOrder());
        int first = arr.get(0), second = -1;

        for(int i=0; i<arr.size(); i++){
            if (arr.get(i) < first){
                second = arr.get(i);
                break;
            }
        }

        System.out.println(second);
    }
}
```
