
# Singleton

When a class is expected to have only one instance. e.g. Runtime

Considered anti-pattern by some, since:

- violation of single responsibility
- increased coupling

## Basic

```java
public class MyClass {

    private static MyClass instance;

    private MyClass() {}

    public static getInstance() {
        if(instance == null) {
            instance = new MyClass();
        }
        return instance;
    }
}
```

- Con: concurrent access may cause two instances

## Concurrent

```java
public class MyClass {

    private static MyClass instance;

    private MyClass() {}

    public static synchronized getInstance() {
        if(instance == null) {
            instance = new MyClass();
        }
        return instance;
    }
}
```

- Pro: will not create two instances
- Con: method locked for each get call

## Double Checking

```java
public class MyClass {

    private static MyClass instance;

    private MyClass() {}

    public static getInstance() {
        if(instance == null) {
            synchronized(MyClass.class) {
                if(instance == null) {
                    instance = new MyClass();
                }
            }
        }
        return instance;
    }
}
```

- Pro: method not locked each time
- Con: may get after not-null but before complete

## Volatile

```java
public class MyClass {

    private static volatile MyClass instance;

    private MyClass() {}

    public static getInstance() {
        if(instance == null) {
            synchronized(MyClass.class) {
                if(instance == null) {
                    instance = new MyClass();
                }
            }
        }
        return instance;
    }
}
```

- Pro: will be completed before get

## Early Instantanation

```java
public class MyClass {

    private static MyClass instance = new MyClass();

    private MyClass() {}

    public static getInstance() {
        return instance;
    }
}
```

## Redundancy Removed

```java
public class MyClass {

    public static MyClass instance = new MyClass();

    private MyClass() {}
}
```

# Extra [Untested]

## Static Block

```java
public class MyClass {

    public static MyClass instance;

    static {
        instance = new MyClass();
    }

    private MyClass() {}
}
```

