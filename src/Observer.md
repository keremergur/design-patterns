
# Observer

Get informed about a state change.

## Publish / Subscribe Principle (newsletter)

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

## Multiple Provider

```java
public interface JobProvider {
    public void addJob(String job);
    public void addObserver(JobObserver o);
    public void removeObserver(JobObserver o);
}
```

## Variations

- Push method: notify observer and pass information.
- Pull method: only notify observer, observer may fetch the information itself.

## Standard Library

```scala
java.util.Observer (interface) [deprecated]
java.util.Observable (class) [deprecated]
java.util.concurrent.Flow.Processor (interface)
java.util.concurrent.Flow.Publisher (interface)
java.util.concurrent.Flow.Subscriber (interface)
java.util.concurrent.Flow.Subscription (interface)

helper:
java.util.concurrent.Executor
java.util.concurrent.CompletableFuture
javafx.collections.ObservableList
java.util.EventObject
java.util.EventListener
```
