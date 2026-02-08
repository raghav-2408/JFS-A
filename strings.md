# Strings

## Check whether a word contains Vowels using regex

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


## Reverse a string using StringBuilder

```java
public class Strings {

    public static String reverseString(String word){
        String result = new StringBuilder(word).reverse().toString();
        return result;
    }
    public static void main(String[] args) {
        System.out.println(Strings.reverseString("Hello")); // olleH
    }
}
```
