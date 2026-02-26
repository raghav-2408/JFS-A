```java
    for (Map.Entry<String, Integer> entry : map.entrySet()) {
// Get Highest
            if (entry.getValue() >= maxMarks) {
                high = entry.getKey();
                maxMarks = entry.getValue();
                highList.add(high + ":" + entry.getValue());
            }
// Get lowest
            if (entry.getValue() <= minMarks && !highList.contains(entry.getKey() + ":" + entry.getValue())) {
                low = entry.getKey();
                minMarks = entry.getValue();
                lowList.add(low + ":" + entry.getValue());
            }
        }
```
