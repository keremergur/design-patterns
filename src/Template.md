
# Template Method

## Low Quality

```java
public class Uppercase {

    public final void run() {
        final var input = textEnter();
        final var converted = convert(input);
        System.out.println(converted);
    }

    private String textEnter() {
        return JOptionPane.showInputDialog("Text:");
    }

    private String convert(String input) {
        return input.toUpperCase();
    }
}

public class Lowercase {/* ... */}
```

## Abstract Method

```java
public class Input {

    public final void run() {
        final var input = textEnter();
        final var converted = convert(input);
        System.out.println(converted);
    }

    private String textEnter() {
        return JOptionPane.showInputDialog("Text:");
    }

    private abstract String convert(String input);
}

public class Uppercase extends Input {
    @Override
    private String convert(String input) {
        return input.toUpperCase();
    }
}
public class Lowercase extends Input {/* ... */}
```

- Abstract class with abstract method
- Must be overridden in subclass

```java
// Hollywood principle
public class Client {
    public static void main(String[] args) {
        Input in = new Uppercase();
        in.run();
    }
}
```

Superclass calls the method of subclass.  
"Don't call us, we'll call you"

`var` will not work since the type must cover both cases.

## Hook Methods

```java
public class Input {

    public final void run() {
        final var input = textEnter();
        final var converted = convert(input);
        System.out.println(converted);
    }

    private String textEnter() {
        return JOptionPane.showInputDialog("Text:");
    }

    protected String convert(String input) {
        return input.toLowerCase();
    }
}

public class Uppercase extends Input {
    @Override
    protected String convert(String input) {
        return input.toUpperCase();
    }
}
```

- Abstract class with defined method
- Can be overridden in subclass if needed

> Private methods are final, cannot be overridden