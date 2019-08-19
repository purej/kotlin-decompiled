Kotline to Java-Compile Results

# Object / Class Declarations
Describes some common Kotlin member variable declarations and the resulting compiled Java code result (*.class). The result has been decompiled to show whats going on. This has been tested with IntelliJ 2019.2, OpenJdk 11 and the decompiler JD and procyon.



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
@Metadata(...)
public final class A {
  public static final A INSTANCE;
  static {
    A a = new A();
    INSTANCE = a;
  }
  private A() {
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
@Metadata(...)
final class A {
  public static final A INSTANCE;
  static {
    A a = new A();
    INSTANCE = a;
  }
  private A() {
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
@Metadata(...)
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
@Metadata(...)
final class A {
  public A() {
  }
}
```
</td></tr>

<tr><td>

```kotlin
open class A {
}
```
</td><td>

```java
@Metadata(...)
public class A {
  public A() {
  }
}
```
</td></tr>


<tr><td>

```kotlin
abstract class A {
}
```
</td><td>

```java
@Metadata(...)
public abstract class A {
  public A() {
  }
}
```
</td></tr>

</table>
