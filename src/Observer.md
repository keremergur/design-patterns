
# Observer

Get informed about a state change.

Publish/subscribe principle (newsletter)

```java
public interface JobObserver {
    void newOffer(String job);
}
```
```java
public class JobMarket {

    private final List<JobObserver> obsList = new ArrayList<>();
    private final List<String> jobList = new ArrayList<>();

    public void addJob(String job) {
        jobList.add(job);
        obsList.forEach(o -> o.newOffer(job));
    }

    public void addObserver(JobObserver o) {
        obsList.add(o);
    }

    public void removeObserver(JobObserver o) {
        obsList.remove(o);
    }
}
```
