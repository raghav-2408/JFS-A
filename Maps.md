# Sort Map using Comparator

```java
Collections.sort(list, new Comparator<Map.Entry<String, Integer>>() {
    @Override
    public int compare(Map.Entry<String, Integer> e1,
                       Map.Entry<String, Integer> e2) {
        return e1.getValue().compareTo(e2.getValue());
    }
});
```

# Model Forge

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
        this.jobList.add(job); 
    }

    
    // 2
    public TrainingJob getTrainingJobById(String jobId) {
        if (jobList.isEmpty()) return null;
        
        for (TrainingJob job : jobList) { // job is Object
        	if (job.getJobId().equalsIgnoreCase(jobId)) {
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
        	map.put(region, computeHours);
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

    
    public boolean updateComputeHours(String jobId, double additionalHours) {
        for (TrainingJob job : jobList) {
        	if (jobId.equals(job.getModelId())) {
        		double additional = job.getComputeHours() + additionalHours;
        		job.setComputeHours(additional);
        		return true;
        	}
        }
        return false;
    }

    
    public List<TrainingJob> filterJobs(String region, String status) {
        List<TrainingJob> result = new ArrayList<>();
        
        for (TrainingJob job : jobList) {
        	if (job.getRegion().equalsIgnoreCase(region) && job.getStatus().equalsIgnoreCase(status)) {
        		result.add(job);
        	}
        }
        return result;
    }

    
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
        
        for (Map.Entry<String, List<TrainingJob>> entry : grouped.entrySet()) {
        	List<TrainingJob> list = entry.getValue();
        	Collections.sort(list, new Comparator<TrainingJob>() {
        		@Override
        		public int compare (TrainingJob a, TrainingJob b) {
        			return Double.compare(b.getTrainingCost(), a.getTrainingCost());
        		}
			});
        }
        
        return grouped;
    }

    
    public Map<String, Integer> getStatusStats() {
        Map<String, Integer> result = new HashMap<>();
        
        for (TrainingJob job : jobList) {
        	int count = 0;
        	if (job.getStatus().equals("COMPLETED")) {
        		if (result.isEmpty()) {
        			result.put(job.getStatus(), count);
        		} else {
        			result.put(job.getStatus(), count++);
        		}
        	}
        	
        	else if (job.getStatus().equals("RUNNING")) {
        		if (result.isEmpty()) {
        			result.put(job.getStatus(), count);
        		} else {
        			result.put(job.getStatus(), count++);
        		}
        	}
        	
        	else if (job.getStatus().equals("FAILED")) {
        		if (result.isEmpty()) {
        			result.put(job.getStatus(), count);
        		} else {
        			result.put(job.getStatus(), count++);
        		}
        	}
        }
        return result;
    }

      
    public double calculateTotalTrainingCost() {
        double total = 0;
        
        for (TrainingJob job : jobList) {
        	double baseCost = 0;
        	if (job.getModelType().equals("LLM")) {
        		baseCost = job.getComputeHours() + job.getTrainingCost();
        		total = baseCost + 1000;
        	}
        	else if (job.getModelType().equals("Vision")) {
        		baseCost = job.getComputeHours() + job.getTrainingCost();
        		total = baseCost + 800;
        	}
        	else if (job.getModelType().equals("Speech")) {
        		baseCost = job.getComputeHours() + job.getTrainingCost();
        		total = baseCost + 600;
        	}
        	else {
        		baseCost = job.getComputeHours() + job.getTrainingCost();
        		total = baseCost + 400;
        	}
        }
        return total;
    }
}

```
