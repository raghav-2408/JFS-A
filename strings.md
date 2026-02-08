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

## Reverse string using a temp variable (simple loop)

```java
public class Strings {

    public static String reverseString(String word){
        String temp = "";
        for (int i = word.length() - 1; i >= 0; i--){
            temp = temp + word.charAt(i);
        }
        return temp;
    }
    public static void main(String[] args) {
        System.out.println(Strings.reverseString("Hello"));
    }
}
```


## Reverse using swapping (without creating a new string

```java

public class Strings {

    public static String reverseUsingSwap (String word){
        char[] arr = word.toCharArray();
        int left = 0, right = word.length()-1;
        while (left < right) {
            char temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
        return new String(arr);
    }

    public static void main(String[] args) {
        System.out.println(reverseUsingSwap("Raghav"));
    }
}

```
