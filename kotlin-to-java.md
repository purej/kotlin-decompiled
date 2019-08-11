# Kotline to Java (Compiles To)
Describes some common Kotlin declarations and the resultings compiled Java code result. This has been tested with IntelliJ 2019.2, OpenJdk 11 and the JD decompiler.

## Kotlin Metadata
The Kotlin compiler adds a ``@Metadata`` annotation to EVERY class file. This annotation contains alot of additional information, see [Metadata.kt](https://github.com/JetBrains/kotlin/blob/master/libraries/stdlib/jvm/runtime/kotlin/Metadata.kt). This is the reason, why Kotlin compile class files are about 30% bigger in size then plain Java compile classes.

Example:

<table>
<tr><td>Kotlin</td><td>Java</td></tr>
<tr><td>

```kotlin
package org.myorg.mypackage
class A {
}
```

</td><td>

```java
package org.myorg.mypackage;
@Metadata(mv = {1, 1, 15}, bv = {1, 0, 3}, k = 1,
  d1 = {"\000\f\n\002\030\002\n\002\020\000\n\002\b\002\030\0002\0020\001B\005�\006\002\020\002�\006\003"},
  d2 = {"Lorg/myorg/mypackage/A;", "", "()V", "myproject-name"})
public final class A {}
```

</td></tr>
</table>


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
@Metadata(mv = {1, 1, 15}, bv = {1, 0, 3}, k = 1, d1 = {"...."}, d2 = {"Lpurej/kotlin/A;", "", "()V", "kotlin-v1"})
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


### .tmpl

<table>
<tr><td>Kotlin</td><td>Java</td></tr>
<tr><td>

```kotlin
...
```

</td><td>

```java
...
```

</td></tr>
</table>

