## Comparator<T>
### String:INT:INT

```java
package dayFour;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Scanner;
import java.util.Comparator;

class Product{
	int productid;
	String productName;
	double price;
	
	public Product(int productid, String productName, double price) {
		this.productid = productid;
		this.productName = productName;
		this.price = price;
	}
	
	public int getProductId() {
		return productid;
	}
	
	public String getProductName() {
		return productName;
	}
	
	public double getPrice() {
		return price;
	}
	
	@Override
	
	public String toString() {
		return productid + " " + productName + " " + price;
	}
	
}

class SortById implements Comparator<Product>{ // why <Product> ? hum Java ko bolre hai we are going to compare object of Product Class!
	public int compare(Product a, Product b) {
		return a.productid - b.productid;
	}
}

class SortByPrice implements Comparator<Product>{
	public int compare(Product a, Product b) {
		return Double.compare(a.getPrice(), b.getPrice());
	}
}

public class Q_Eleven {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("Enter the products count : ");
		int prodCount = sc.nextInt();
		sc.nextLine();
		
		if (prodCount <= 0) {
			System.out.println("Invalid count");
			return;
		}
		
		ArrayList<Product> arr = new ArrayList<Product>();
		
		System.out.println("Enter Product details :");
		
		for (int i = 0; i < prodCount; i++) {
			String inputString = sc.nextLine();
			String[] parts = inputString.split(":");
			
			int pID = Integer.parseInt(parts[0]);
			String pName = parts[1];
			double price = Double.parseDouble(parts[2]);
			
			// actually works as a setter!
			arr.add(new Product(pID, pName, price)); // yaha har baar naya object ko create krra hai!
		}
				
		int ch = sc.nextInt();
		
		System.out.println("1.Sort By Id");
		System.out.println("2.Sort By Price");
		
		
		if(ch == 1) {
			Collections.sort(arr, new SortById());
			System.out.println("After Sorting By Id");
			
		}else if(ch ==2) {
			Collections.sort(arr, new SortByPrice());
			System.out.println("After Sorting By Price");
			
		}else {
			System.out.println("Invalid Choice!");
		}
		
		for(Product p : arr) {
			System.out.println(p);
		}
		
	}
		
}

```


## Swap and Reverse

```java
import java.util.Arrays;
import java.util.Scanner;

public class UserInterface {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Enter the sentence");
        String sentence = sc.nextLine();

        String[] parts = sentence.trim().split("\\s+");

        if (parts.length <= 2){
            System.out.println("Invalid Length");
            return;
        }

        if(!sentence.matches("[a-zA-Z ]+")){
            System.out.println(sentence + " is an invalid sentence");
            return;
        }

        int N = parts.length;

        String[] clean = new String[N];

        clean[0] = parts[N-1];
        clean[N-1] = parts[0];

        for (int i = 1; i < N-1; i++){
            StringBuilder temp = new StringBuilder();
            temp.append(parts[i]).reverse();
            clean[N-i-1] = temp.toString();
        }

        StringBuilder result = new StringBuilder();
        result.append(Arrays.toString(clean));

        
        String output = String.join(" ", clean);
        System.out.println(output);

    }
}
```
