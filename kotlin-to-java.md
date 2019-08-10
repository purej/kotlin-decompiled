# Kotline to Java (Compiles To)
Describes some common Kotlin declaration and the resultings compiled Java class result.

## Declarations

### Object
<table>
<tr><td>Kotlin</td><td>Java</td></tr>

<tr><td>

```kotlin
object A {
}
internal object A {
}
```

</td><td>

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
</td></tr>

<tr><td>

```kotlin
private object A {
}
```
</td><td>

```java
final class A {
  private A() {
  }
  public static final A INSTANCE;
  static {
    A a = new A();
    INSTANCE = a;
  }
}
```
</td></tr>

</table>




### Class
<table>
<tr><td>Kotlin</td><td>Java</td></tr>
<tr><td>

```kotlin
class A {
}
internal class A {
}
```
</td><td>

```java
public final class A {
  public A() {
  }
}
```
</td></tr>
<tr><td>

```kotlin
private class A {
}
```
</td><td>

```java
final class A {
  public A() {
  }
}
```
</td></tr>

</table>



Bla bla...
