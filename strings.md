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


## Reverse using swapping (without creating a new string)

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

## Check Palindrome

```java
public class Strings {

    public static Boolean isPalindrome(String word){
        int left = 0, right = word.length() - 1;

        while (left < right){
            if (word.charAt(left) != word.charAt(right)){
                return false;
            }
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isPalindrome("madam"));
    }
}
```

## Count Vowels

```
Initial values

word = "Hello"
vowels = "aeiouAEIOU"

Loop through each character:
i = 0

word.charAt(0) = 'H'
vowels.indexOf('H') → -1 (not found)
if (-1 != -1) → false → continue

i = 1

word.charAt(1) = 'e'
vowels.indexOf('e') → 1 (found at index 1)
if (1 != -1) → true
return true;  ⟶ Method stops here and returns true
```

```java

public class Strings {

    public static int countVowels(String word){
        int count = 0;
        String vowels = "aeiouAEIOU";
        for(int i = 0; i < word.length(); i++){
            if (vowels.indexOf(word.charAt(i)) != -1){
                count+=1;
            }
        }
        
        return count;
    }

    public static void main(String[] args) {
        System.out.println(countVowels("madam"));
    }
}

```

## Count Words in a Sentence

```java
public class Strings {

    public static int countwWords(String word){
        if (word.trim().isEmpty()){
            return 0;
        }
        return word.trim().split("\\s+").length;
    }

    public static void main(String[] args) {
        System.out.println(countwWords("there are 4 words"));
    }
}
```

## Remove Vowels

```java
public class Strings {

    public static String removeVowels(String word){
        return word.replaceAll("[aeiouAEIOU]", "");
    }

    public static void main(String[] args) {
        System.out.println(removeVowels("Hello"));
    }
}
```

## Check Anagram

```java

import java.util.Arrays;

public class Strings {

    public static boolean checkAnagram(String word1, String word2){

        if (word1.length() != word2.length()) 
            {
                return false;
            }
        
        char[] s1 = word1.toCharArray();
        char[] s2 = word2.toCharArray();

        Arrays.sort(s1);
        Arrays.sort(s2);

        return Arrays.equals(s1, s2);
    }

    public static void main(String[] args) {
        System.out.println(checkAnagram("listen", "silent"));
    }
}

```

## Reverse each word of a sentence

```java
import java.util.*;
public class Strings {

    public static void main(String[] args) {
        ArrayList<String> s = new ArrayList<String>();

        Scanner sc = new Scanner(System.in);

        String stInput = sc.nextLine();

        s.add(stInput);

        for(String i : s){
            String[] word = i.split(" ");
            for(String j : word){
                String reversedString = new StringBuilder(j).reverse().toString();
                System.out.print(reversedString + " ");
            }
        }
    }
}
```

