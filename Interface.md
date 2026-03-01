```java
import java.time.LocalDate;

public interface Mission {
	public double calculatePerformanceScore(int yearsInService);
	
	public double calculateMaintenanceExpense(int yearsInService);
	
	public default Mission getHigherValueMission(Mission  m1, Mission m2) {
		// missionInfo is a child of mission so we do upCast here
		int year1 = Mission.getYearsInService(((MissionInfo) m1).getLaunchYear());
		int year2 = Mission.getYearsInService(((MissionInfo) m2).getLaunchYear());
		
		double scoreM1 = m1.calculatePerformanceScore(year1);
		double scoreM2 = m2.calculatePerformanceScore(year2);
		
		if (scoreM1 >= scoreM2) { // covers m1 m2 equals condition
			return m1;
		}
		else {
			return m2;
		}
	}
	
	public static int getYearsInService(int launchYear) {
		LocalDate date = LocalDate.now();
		int totalYears = date.getYear() - launchYear;
		return totalYears;
	}
}
```


# 2

```java

public class MissionInfo implements Mission, RiskAssessable {

    private int missionId;
    private String missionName;
    private String operatorName;
    private double baseBudget;
    private String missionType;
    private int launchYear;

    public MissionInfo(int missionId, String missionName, String operatorName,
                       double baseBudget, String missionType, int launchYear) {
        this.missionId = missionId;
        this.missionName = missionName;
        this.operatorName = operatorName;
        this.baseBudget = baseBudget;
        this.missionType = missionType;
        this.launchYear = launchYear;
    }

    public int getMissionId() { 
        return missionId; 
    }
    public String getMissionName() { 
        return missionName; 
    }
    public String getOperatorName() { 
        return operatorName; 
    }
    public double getBaseBudget() { 
        return baseBudget; 
    }
    public String getMissionType() { 
        return missionType; 
    }
    public int getLaunchYear() { 
        return launchYear; 
    }
    
    public void setMissionId(int missionId) {
		this.missionId = missionId;
	}

	public void setMissionName(String missionName) {
		this.missionName = missionName;
	}

	public void setOperatorName(String operatorName) {
		this.operatorName = operatorName;
	}

	public void setBaseBudget(double baseBudget) {
		this.baseBudget = baseBudget;
	}

	public void setMissionType(String missionType) {
		this.missionType = missionType;
	}

	public void setLaunchYear(int launchYear) {
		this.launchYear = launchYear;
	}
    


    // Override the calculatePerformanceScore method
    // Override the calculateMaintenanceExpense method
    // Override the calculateRiskFactor method
	
	@Override
	public double calculatePerformanceScore(int yearsInService) {
		double multiplier = 0;
		if (missionType.equals("Surveillance")) {
			multiplier = 2.2;
		}
		else if (missionType.equals("Delivery")) {
			multiplier = 1.5;
		}
		else if (missionType.equals("Research")) {
			multiplier = 2.8;
		}
		
		double performanceScore = (yearsInService * multiplier * baseBudget) / 100;
		return performanceScore;
	}
	
	
	public double calculateMaintenanceExpense(int yearsInService) {
		double rate = 0;
		if (missionType.equals("Surveillance")) {
			rate = 1.1;
		}
		else if (missionType.equals("Delivery")) {
			rate = 	0.7;
		}
		else if (missionType.equals("Research")) {
			rate = 1.6;
		}
		double expense =  (yearsInService * rate * baseBudget) / 10.0;
		return Math.round(expense);
	}
	
	public double calculateRiskFactor(int yearsInService) {
		double riskMultiplier = 0;
		if (missionType.equals("Surveillance")) {
			riskMultiplier = 1.8;
		}
		else if (missionType.equals("Delivery")) {
			riskMultiplier = 	1.2;
		}
		else if (missionType.equals("Research")) {
			riskMultiplier = 2.5;
		}
		
		double riskFactor = yearsInService * riskMultiplier;
		return riskFactor;
	}
	
  
}
```

# 3

```java

import java.util.Scanner;

public class UserInterface {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.println("Enter Mission 1 details:");
        int missionId1 = sc.nextInt();
        sc.nextLine();
        String missionName1 = sc.nextLine();
        String operatorName1 = sc.nextLine();
        double baseBudget1 = sc.nextDouble();
        sc.nextLine();
        String missionType1 = sc.nextLine();
        int launchYear1 = sc.nextInt();
        
        MissionInfo infoObj1 = new MissionInfo(missionId1, missionName1, operatorName1, baseBudget1, missionType1, launchYear1);
        
        System.out.println("Enter Mission 2 details:");
        int missionId12 = sc.nextInt();
        sc.nextLine();
        String missionName2 = sc.nextLine();
        String operatorName2 = sc.nextLine();
        double baseBudget2 = sc.nextDouble();
        sc.nextLine();
        String missionType2 = sc.nextLine();
        int launchYear2 = sc.nextInt();
        
        MissionInfo infoObj2 = new MissionInfo(missionId12, missionName2, operatorName2, baseBudget2, missionType2, launchYear2);

        System.out.println("Mission Summary:");
        
        int yearsInService = Mission.getYearsInService(launchYear1);
        System.out.println(missionName1 + " operated by " + operatorName1);
        System.out.println("Years In Service: " + yearsInService);
        System.out.println("Performance Score: " + infoObj1.calculatePerformanceScore(yearsInService));
        System.out.println("Maintenance Expense: " + infoObj1.calculateMaintenanceExpense(yearsInService));
        double riskFactorValue = infoObj1.calculateRiskFactor(yearsInService);
        String riskLevel = infoObj1.getRiskLevel(riskFactorValue);
        System.out.println("Risk Level: " + riskLevel);
        
        int yearsInService2 = Mission.getYearsInService(launchYear2);
        System.out.println(missionName2 + " operated by " + operatorName2);
        System.out.println("Years In Service: " + yearsInService2);
        System.out.println("Performance Score: " + infoObj2.calculatePerformanceScore(yearsInService2));
        System.out.println("Maintenance Expense: " + infoObj2.calculateMaintenanceExpense(yearsInService2));
        double riskFactorValue2 = infoObj2.calculateRiskFactor(yearsInService2);
        String riskLevel2 = infoObj2.getRiskLevel(riskFactorValue2);
        System.out.println("Risk Level: " + riskLevel2);
        
        String higherValue = null;
        
        if (infoObj1.calculateRiskFactor(yearsInService) > infoObj2.calculateRiskFactor(yearsInService2) ) {
        	higherValue = missionName1;
        }
        else {
        	higherValue = missionName2;
        }
        System.out.println("Higher Value Mission: " + higherValue);
    }
}
```

