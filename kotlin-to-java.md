# Kotline to Java (Compiles To)
Describes some common Kotlin declaration and the resultings compiled Java class result.

## Declarations

### Object
<table>
<tr><td>Kotlin</td><td>Java</td></tr>
<tr>
<td>

```kotlin
object A {
}
```
</td>
<td>

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
</td>
</tr>
</table>


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


Kotlin:
```kotlin
class A {
}
```

Java:
```java
public final class A {
  public A() {
  }
}
```
