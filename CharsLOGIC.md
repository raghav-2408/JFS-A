```java
if (c >= 'A' && c <= 'Z') {
    arr.add((char) ('A' + (c - 'A' + 2) % 26)); // Z -> B
}
if (c >= 'a' && c <= 'z') {
    arr.add((char) ('a' + (c - 'a' + 2) % 26)); // z -> b
}
```
