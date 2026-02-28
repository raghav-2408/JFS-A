```
Provides a comparator that sorts employees by skill count (descending) and then by salary (descending)
```
```java
public static Comparator<Employee> compareBySkillCountThenSalary() {
    Comparator<Employee> result = Comparator
                    .comparingInt((Employee e) -> e.getSkills().size())
                    .reversed()
                    .thenComparing((Employee e) -> e.getBasicSalary(), Comparator.reverseOrder());
    return result;  
}
```

```
Returns a predicate to filter employees who joined before the specified year.
```
```java
public static Predicate<Employee> joinedBefore(int year) {
    Predicate<Employee> result = N -> N.getJoiningYear() < year;
    return result;
}
```
```
Computes the bonus amount : basicSalary × (rating / 100).
```
```java
public static Function<Employee, Double> computeBonus() {
    Function<Employee, Double> result = N -> N.getBasicSalary() * (N.getRating() / 100);
    return result;
}
```
```
Returns a function that calculates final salary = basicSalary + bonus + experience-based percent increment (applied only if experience ≥ 5 years).
```

```java
public static BiFunction<Employee, Integer, Double> computeFinalSalary(double experiencePercent) {
    BiFunction<Employee, Integer, Double> result = 
        (N, currentYear) ->{
          double basicSalary = N.getBasicSalary();
          double bonus = computeBonus().apply(N);
          int experience = currentYear - N.getJoiningYear();
          double experienceInc = 0;
          if (experience >= 5) {
            experienceInc = basicSalary * (experiencePercent / 100);
          }
          return  basicSalary + bonus  + experienceInc;
        };
return result;
}
```


```	
Returns a consumer that updates an employee's basic salary with the computed final salary.
```
```java
public static Consumer<Double> applyFinalSalary(Employee e) {
    Consumer<Double> result = N -> e.setBasicSalary(N);
    return result;
}
```

```java
import java.util.Comparator;
import java.util.List;
import java.util.NoSuchElementException;
import java.util.stream.Stream;

public class CartonUtility {
	private List<Carton> cartonList;
	
	//FILL THE CODE HERE 
	public List<Carton> getCartonList () {
		return cartonList;
	}
	
	public void setCartonList (List<Carton> list) {
		this.cartonList = list;
	}
	
	public Stream<Carton> convertToStream() {
		
		Stream<Carton> s = cartonList.stream();
		return s;
	}

	public Carton findMax(Stream<Carton> stream1) {
		
		return stream1.max(Comparator.comparingInt(Carton :: getQuantity))
					.orElseThrow (() -> new NoSuchElementException("No Cartons available"));			
	}
}
```
