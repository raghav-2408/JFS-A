# Strings

## Check whether a word contains Vowels

```java
public class Strings {
    public static boolean checkVowels(String word){
        boolean result = word.toLowerCase().matches(".*[aeiou].*");
        return result;
    }

    public static void main(String[] args) {
        System.out.println(Strings.checkVowels("Hello")); // true
    }
}
```
