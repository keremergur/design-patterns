
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

    private final Set<JobObserver> obsSet = new HashSet<>();
    private final Set<String> jobSet = new HashSet<>();

    public void addJob(String job) {
        jobSet.add(job);
        obsSet.forEach(o -> o.newOffer(job));
    }

    public void addObserver(JobObserver o) {
        obsSet.add(o);
    }

    public void removeObserver(JobObserver o) {
        obsSet.remove(o);
    }
}
```
