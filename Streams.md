# List<Integer> arr = Arrays.asList(1, 2, 3, 2);
```java
 int total = arr.stream()
                            .mapToInt(N -> N)
                            .sum();
```

```java
arr.stream()
            .distinct()
            .forEach(N -> System.out.println(N));
```
```java
 List<Integer> newList = arr.stream()
                                        .distinct()
                                        .toList();
        System.out.println(newList);
```
```java
Map<String, Integer> newMap = arr.stream()
                                        .distinct()
                                        .filter(N -> N % 2 == 0)
                                        .collect(Collectors.toMap(
                                            N -> "A",
                                            N -> N
                                        ));
        System.out.println(newMap);
```
