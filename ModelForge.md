```java
import java.util.List;
import java.util.Map;
import java.util.Scanner;
import java.util.Set;

public class UserInterface {
    public static void main(String[] args) {
    	Scanner sc = new Scanner(System.in);
    	System.out.println("1. Add Training Job");
    	System.out.println("2. Retrieve Training Job by ID");
    	System.out.println("3. Retrieve Jobs With Highest Training Cost");
    	System.out.println("4. Compute Hours By Region");
    	System.out.println("5. Group Jobs By Model Type");
    	System.out.println("6. Update Compute Hours By Job ID");
    	System.out.println("7. Filter Jobs By Region and Status");
    	System.out.println("8. Top-N Costly Jobs By Region");
    	System.out.println("9. Status Statistics");
    	System.out.println("10. Calculate Total Training Cost");
    	System.out.println("11. Exit");
    	
    	TrainingJobService tjs = new TrainingJobService();
    	
    	while(true) {
    		System.out.println("Enter your choice");
    		int choice = sc.nextInt();
    		sc.nextLine();
    		
    		if (choice == 1) {
    			System.out.println("Enter job details");
    			TrainingJobUtil tuObj = new TrainingJobUtil();
    			String details = sc.nextLine();
    			TrainingJob p = tuObj.parseTrainingJob(details);
    			tjs.addTrainingJob(p);
    			System.out.println("Training job added successfully");
    		}
    		
    		else if (choice == 2) {
    			System.out.println("Enter Job ID:");
    			String jobId = sc.nextLine();
    			TrainingJob job = tjs.getTrainingJobById(jobId);
    			
    			if (job == null) {
    				System.out.println("job not found");
    				continue;
    			}
    			
    			System.out.println(job.toString());
    		}
    		
    		else if (choice == 3) {	
    			Set<TrainingJob> result = tjs.getJobsWithHighestTrainingCost();
    			
    			if (result.isEmpty()) {
    				System.out.println("Job not found");
    				continue;
    			}
    			
    			for (TrainingJob job : result) {
    				System.out.println(job.toString());
    			}
    		}
    		
    		else if (choice == 4) {
    			Map<String, Double> result = tjs.getComputeHoursByRegion();
    			
    			for (Map.Entry<String, Double> entry : result.entrySet()) {
    				System.out.println(entry.getKey() + "-" + entry.getValue());
    			}
    		}
    		
    		else if (choice == 5) {
    			Map<String, List<TrainingJob>> result = tjs.groupJobsByModelType();
    			
    			for (Map.Entry<String, List<TrainingJob>> entry : result.entrySet()) {
    				System.out.println("Model Type:" + entry.getKey());
    				System.out.println(entry.getValue().toString() + "\n");
    				System.out.println();
    			}
    		}
    		
    		else if (choice == 6) {
    			System.out.println("Enter Job ID:");
    			String jobId = sc.nextLine();
    			System.out.println("Enter additional compute hours:");
    			int computeHours = sc.nextInt();
    			sc.nextLine();
    			if (tjs.updateComputeHours(jobId, computeHours)) {
    				System.out.println("Compute hours updated successfully");
    			} else {
    				System.out.println("Job not found");
    			} // 6, 9, 10
    		}
    		
    		else if (choice == 7) {
    			System.out.println("Enter Region:");
    			String region = sc.nextLine();
    			
    			System.out.println("Enter Status:");
    			String status = sc.nextLine();
    			
    			List<TrainingJob> result = tjs.filterJobs(region, status);
    			
    			for (TrainingJob job : result) {
    				System.out.println(job.toString() + "\n");
    				System.out.println();
    			}
    		}
    		
    		else if (choice == 8) {
    			System.out.println("Enter N:");
    			int N = sc.nextInt();
    			sc.nextLine();
    			
    			Map<String, List<TrainingJob>> result = tjs.getTopCostlyJobsByRegion(N);
    			
    			for (Map.Entry<String, List<TrainingJob>> entry : result.entrySet()) {
    				System.out.println("Region:" +entry.getKey());
    				System.out.println(entry.getValue().toString());
    			}
    			
    		}
    		
    		else if (choice == 9) {
    			Map<String, Integer> result = tjs.getStatusStats();
    			
    			for (Map.Entry<String, Integer> entry : result.entrySet()) {
    				System.out.println(entry.getKey() + ":" + entry.getValue());
    			}
    		}
    		
    		else if (choice == 10) {
    			double result = tjs.calculateTotalTrainingCost();
    			System.out.printf("Total training Cost for COMPLETED jobs: %.1f\n", result);
    		}
    		
    		else if (choice == 11) {
    			System.out.println("Exiting application");
    			break;
    		}
    	}
    }
}

```
# 2

```java
import java.util.*;

public class TrainingJobService {
    private List<TrainingJob> jobList = new ArrayList<>();
    
    public List<TrainingJob> getJobList() {
        return jobList;
    }

    public void setJobList(List<TrainingJob> jobList) {
        this.jobList = jobList;
    }

    // adds training job object to the list
    public void addTrainingJob(TrainingJob job) {
    	if (job != null) {    		
    		this.jobList.add(job); 
    	}
    }

    
    // 2
    public TrainingJob getTrainingJobById(String jobId) {
        if (jobId == null || jobList.isEmpty()) return null;
        
        for (TrainingJob job : jobList) { // job is Object
        	if (job.getJobId().equals(jobId)) {
        		return job;
        	}
        }
        return null;
    }

   // 3
    public Set<TrainingJob> getJobsWithHighestTrainingCost() {
        Set<TrainingJob> result = new LinkedHashSet<>();
        double maxTrainingCost = 0;
        
        for (TrainingJob job : jobList) {
        	if (job.getTrainingCost() > maxTrainingCost) {
        		maxTrainingCost = job.getTrainingCost();
        	}
        }
        
        for (TrainingJob job : jobList) {
        	if (job.getTrainingCost() == maxTrainingCost) {
        		result.add(job);
        	}
        }
        return result;
    }

    
    // 4
   public Map<String, Double> getComputeHoursByRegion() {
        Map<String, Double> map = new LinkedHashMap<>();
        
        for (TrainingJob job : jobList) {
        	String region = job.getRegion();
        	Double computeHours = job.getComputeHours();
        	map.put(region, map.getOrDefault(region, 0.0) + computeHours);
        }
        return map;
    }

   // 5
    public Map<String, List<TrainingJob>> groupJobsByModelType() {
        Map<String, List<TrainingJob>> map = new LinkedHashMap<>();
        for (TrainingJob job : jobList) {
        	String modelType = job.getModelType();
        	
        	if (!map.containsKey(modelType)) {        		
        		map.put(modelType, new ArrayList<TrainingJob>());
        	}
        	map.get(modelType).add(job);
        }
        return map;
    }

    // 6
    public boolean updateComputeHours(String jobId, double additionalHours) {
    	if(jobId == null) return false;
    	
        for (TrainingJob job : jobList) {
        	if (jobId.equals(job.getJobId())) {
        		double additional = job.getComputeHours() + additionalHours;
        		job.setComputeHours(additional);
        		return true;
        	}
        }
        return false;
    }

    // 7
    public List<TrainingJob> filterJobs(String region, String status) {
        List<TrainingJob> result = new ArrayList<>();
        
        for (TrainingJob job : jobList) {
        	if (job.getRegion().equalsIgnoreCase(region) && job.getStatus().equalsIgnoreCase(status)) {
        		result.add(job);
        	}
        }
        return result;
    }

    // 8
    public Map<String, List<TrainingJob>> getTopCostlyJobsByRegion(int n) {
        Map<String, List<TrainingJob>> grouped = new HashMap<>();
        
        // region ke hisab se group kro objects ko list mein
        for (TrainingJob job : jobList) {
        	String region = job.getRegion();
        	List<TrainingJob> list = grouped.get(region); // if region nahi hai toh null return krega
        	if (list == null) {
        		list = new ArrayList<TrainingJob>(); // null hai toh naya arraylist bnao
        		grouped.put(region, list); 
        	}
        	list.add(job);
        }
        // theek hai, abhi map mai sab kuch hai region : OBJECTS
        // ab usko sort krna hai using Comparator
        //sort kro
        
        // Store top N after sorting, sort krke saare nahi print krni hai
        Map<String, List<TrainingJob>> res = new LinkedHashMap<String, List<TrainingJob>>();
        
        for (Map.Entry<String, List<TrainingJob>> entry : grouped.entrySet()) {
        	List<TrainingJob> list = entry.getValue();
        	Collections.sort(list, new Comparator<TrainingJob>() {
        		@Override
        		public int compare (TrainingJob a, TrainingJob b) {
        			return Double.compare(b.getTrainingCost(), a.getTrainingCost());
        		}
			});

        	 int end = Math.min(n, list.size());
        	 res.put(entry.getKey(), new ArrayList<>(list.subList(0, end)));

        }
        
        return grouped;
    }

    // 9
    public Map<String, Integer> getStatusStats() {
        Map<String, Integer> result = new HashMap<>();
        
        for (TrainingJob job : jobList) {
        	String status = job.getStatus();
        	result.put(status, result.getOrDefault(status, 0) + 1);
        }
        return result;
    }

    // 10
    public double calculateTotalTrainingCost() {
        double total = 0;
        
        for (TrainingJob job : jobList) {
        	// yaha pe sirf COMPLETED rkna hai
        	
        	String status = job.getStatus();
        	
        	if (status.equalsIgnoreCase("COMPLETED")) {
	        	double baseCost = 0;
	        	baseCost = job.getComputeHours() * job.getTrainingCost();
	        	if (job.getModelType().equals("LLM")) {
	        		total += baseCost + 1000;
	        	}
	        	else if (job.getModelType().equals("Vision")) {
	        		total += baseCost + 800;
	        	}
	        	else if (job.getModelType().equals("Speech")) {
	        		total += baseCost + 600;
	        	}
	        	else {
	        		total += baseCost + 400;
	        	}
	        } 
        	else {
        		// agar null hai yaa COMPLETED ke alawa kuch aur aya toh skip the iteration
        		continue;
        	}
        }
        return total;
    }
}
```

# 3

```java
public class TrainingJobUtil {

    public TrainingJob parseTrainingJob(String input) {

    	String[] p = input.split(":");

        return new TrainingJob(
                p[0],        // jobId
                p[1],        // modelId
                p[2],        // modelType
                p[3],        // datasetType
                p[4],        // region
                Double.parseDouble(p[5]),  
                Double.parseDouble(p[6]),
                p[7]       // status
        );
        
        
    }
}
```
