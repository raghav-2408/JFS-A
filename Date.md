# Date
## Calculate Years Of Experience

```java
import java.util.Calendar;
import java.util.Date;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Scanner;

public class UserInterface {
	
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the date of joining");
		String dateOfJoining = sc.nextLine();
		
		SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy");
		sdf.setLenient(false);
		
		Date joinDate = null;
		
		try {
			joinDate = sdf.parse(dateOfJoining);
		}catch (ParseException e) {
			System.out.println(dateOfJoining + " is not the valid date");
		}
		
		
		Date currentDate = null;
		
		try {
			currentDate = sdf.parse("15/12/2020");
		}catch (ParseException e) {
			System.out.println(dateOfJoining + " is not the valid date");
		}
		
		
		Calendar c1 = Calendar.getInstance();
		c1.setTime(joinDate);
		
		Calendar c2 = Calendar.getInstance();
		c2.setTime(currentDate);
		
		int years = c2.get(Calendar.YEAR) - c1.get(Calendar.YEAR); // int - int 
		
		System.out.println(years + " years of experience");
	}

}

```

## Calculate Expiry Date

```java
import java.util.Date;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Scanner;

public class UserInterface {
	
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the Manufacturing Date");
		String manufDate = sc.nextLine();
		
		SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy");
		sdf.setLenient(false);
		
		Date date = null;
		
		try {
			date = sdf.parse(manufDate);
		}catch(ParseException e) {
			System.out.println(manufDate + " is not a valid date");
			return;
		}
		
		System.out.println("Enter the Month");
		int month = sc.nextInt();
		
		Calendar c = Calendar.getInstance();
		
		c.setTime(date);
		
		c.add(Calendar.MONTH, month);
		
		Date dd = c.getTime();
		
		String result = sdf.format(dd);
		
		System.out.println(result + " is the expiry date");
		
	}

}
```
