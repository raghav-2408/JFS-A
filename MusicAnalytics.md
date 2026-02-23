## Using LinkedHashMap

```java
import java.util.Collections;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.Scanner;

public class MusicAnalytics {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number of records to be added");
        int records = sc.nextInt();

        sc.nextLine();
        
        LinkedHashMap<String, Integer> map = new LinkedHashMap<String, Integer>();
        for (int i = 0; i < records; i++) {
            String details = sc.nextLine();
            String[] parts = details.split(":");

            int views = Integer.parseInt(parts[1]);
            map.put(parts[0], views);
        }

        System.out.println("Enter the song title to find the number of views");
        String songTitle = sc.nextLine();

        int foundViews = 0;

        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            if (entry.getKey().equals(songTitle)) {
                foundViews = entry.getValue();
            }
        }

        System.out.printf("Number of views for the song title %s is %d\n", songTitle ,foundViews);

        System.out.println("Songs with the maximum number of views is");
        
        int max = Collections.max(map.values());
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            if (entry.getValue() == max) {
                System.out.println(entry.getKey());
            }
        }
    }
}
```
