```java
Map<String, List<TrainingJob>>

// for list sorting
Collections.sort(jobList, new Comparator<TrainingJob>(){
    @Override
    public int compare(TrainingJob a, TrainingJob b) {
      return Double.compare(a.getTrainingCost(), b.getTrainingCost());
    }
});

for (int i = 0; i < n; i++) {
    for (TrainingJob job : jobList) {
      grouped.get(job.getRegion()).add(job);
    }
}
```
