## EmployeeAudit 

```java
import java.util.ArrayList;

@FunctionalInterface
public interface EmployeeAudit {

	public ArrayList<String> fetchEmployeeDetails (double salary);
	
}
```


## UserInterface
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;
import java.util.Set;

public class UserInterface {
	
	private static Map <String,Double> employeeMap = new HashMap<String, Double>();

	public Map<String, Double> getEmployeeMap() {
		return employeeMap;
	}

	public void setEmployeeMap(Map<String, Double> employeeMap) {
		UserInterface.employeeMap = employeeMap;
	}
	
	public void addEmployeeDetails(String employeeName, double salary) {
		employeeMap.put(employeeName, salary);
	}
	
	public static EmployeeAudit findEmployee() {
		return (salary) -> {
			ArrayList<String> name = new ArrayList<String>();
			for (Map.Entry<String, Double> entry : employeeMap.entrySet()) {
				if (entry.getValue() <= salary) {
					name.add(entry.getKey());
				}
			}
			return name;
		};
	}
	
	public static void main(String[] args)
	{
		
		Scanner sc=new Scanner(System.in);
		UserInterface obj = new UserInterface();
		
		
		
		while (true) {
			System.out.println("1.Add Employee Details");
			System.out.println("2.Find Employee Details");
			System.out.println("3.Exit");
			
			System.out.println("Enter the choice");
			int choice = sc.nextInt();
			
			sc.nextLine();
			
			if (choice == 1) {
				System.out.println("Enter the Employee name");
				String empName = sc.nextLine();
				
				System.out.println("Enter the Employee Salary");
				double salary = sc.nextDouble();
				
				obj.addEmployeeDetails(empName, salary);
				continue;
			}
			
			else if (choice == 2) {
				System.out.println("Enter the salary to be searched");
				double salary = sc.nextDouble();
				
				EmployeeAudit audit = findEmployee(); // method type 
				ArrayList<String> res = audit.fetchEmployeeDetails(salary);
				
				if (res.isEmpty()) {
					System.out.println("No Employee Found");
				}
				else {
					System.out.println("Employee list");
					for (String s : res) {
						System.out.println(s);
					}
				}
				continue;
			}
			
			else if (choice == 3) {
				System.out.println("Let's complete the session");
				break;
			}
		}
	}

}
```

