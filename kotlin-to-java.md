# Kotline to Java (Compiles To)
Describes some common Kotlin declaration and the resulting compiled Java class result.

## Declarations

Kotlin:
```kotlin
object A {
}
```

Java:
```java
public final class A {
    private A() {
    }
    public static final A INSTANCE;
    static {
        A a = new A();
        INSTANCE = a;
    }
}
```
