```java
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
```

```
 Mission is a parent and we are downcasting to its child so we can make use of child methods using onject m1 and m2.
```
```
Mission is the supertype (interface).
MissionInfo is a subtype (a class that implements Mission).
The variable m1 is declared as type Mission, but at runtime it actually references a MissionInfo object.
You downcast (MissionInfo) m1 so you can call a method that exists only on MissionInfo (like getLaunchYear()), which is not declared on the Mission interface.
```
