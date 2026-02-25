```java
  List<Map.Entry<String, Integer>> list = new ArrayList<>(map.entrySet());
        Collections.sort(list, new Comparator<Map.Entry<String, Integer>>() {
            @Override
            public int compare(Map.Entry<String, Integer> e1, 
                    Map.Entry<String, Integer> e2) {
            return e1.getValue().compareTo(e2.getValue());
                    }
        });

        System.out.println(list);
```
