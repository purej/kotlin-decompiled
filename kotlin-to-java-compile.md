# Kotline to Java (Compiles To)
Describes some common Kotlin declarations and the resulting compiled Java code result. This has been tested with IntelliJ 2019.2, OpenJdk 11 and the JD decompiler.

## Kotlin Metadata
The Kotlin compiler adds a ``@Metadata`` annotation to every class file. This annotation contains alot of additional information, see [Metadata.kt](https://github.com/JetBrains/kotlin/blob/master/libraries/stdlib/jvm/runtime/kotlin/Metadata.kt). This is the reason, why Kotlin compiled class files are about 30% bigger in size then plain Java compiled classes.

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
public final class A {
}
```

</td></tr>
</table>


## Kotlin @NotNull
The Kotlin compiler might also add a ``@NotNull`` annotation to fields or methods which should never contain/return null values. Unfortunately the [JSR-305](https://jcp.org/en/jsr/detail?id=305) was never properly released, so Kotlin uses the IntelliJ specific ``org.jetbrains.annotations.NotNull`` class, which feels kind of murky but cannot be changed. The retention-policy is CLASS only, so the annotation cannot be read using reflection and thus the org.jetbrains [annotations.jar](https://search.maven.org/search?q=g:org.jetbrains%20AND%20a:annotations&core=gav) is not necessarily required at runtime.


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


### const val

<table>
<tr><td>Kotlin</td><td>Java</td></tr>

<tr><td>

```kotlin
object A {
  const val S1 = "s1"
  internal const val S2 = "s2"
  private const val S3 = "s3"
}
```

</td><td>

```java
@Metadata(...)
public final class A {
  @NotNull
  public static final String S1 = "s1";
  @NotNull
  public static final String S2 = "s2";
  private static final String S3 = "s3";
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
class A {
 companion object {
   const val S1 = "s1"
   internal const val S2 = "s2"
   private const val S3 = "s3"
 }
}
```

</td><td>

```java
@Metadata(...)
public final class A {
  @NotNull
  public static final String S1 = "s1";
  @NotNull
  public static final String S2 = "s2";
  private static final String S3 = "s3";
  public static final Companion Companion;
  static {
    Companion = new Companion(null);
  }
  @Metadata(...)
  public static final class Companion {
    private Companion() {}
  }
}
```
</td></tr>

</table>



### val

<table>
<tr><td>Kotlin</td><td>Java</td></tr>

<tr><td>

```kotlin
object A {
  val S1 = "s1"
  internal val S2 = "s2"
  private val S3 = "s3"

  @JvmField
  val S4 = "s4"
  @JvmField
  internal val S5 = "s5"
}
```

</td><td>

```java
@Metadata(...)
public final class A {
  @NotNull
  private static final String S1 = "s1";
  @NotNull
  private static final String S2 = "s2";
  private static final String S3 = "s3";
  @JvmField
  @NotNull
  public static final String S4 = "s4";
  @JvmField
  @NotNull
  public static final String S5 = "s5";

  public static final A INSTANCE;

  @NotNull
  public final String getS1() {
    return S1;
  }

  @NotNull
  public final String getS2$kotlin_v1() {
    return S2;
  }

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
class A {
 val S1 = "s1"
 internal val S2 = "s2"
 private val S3 = "s3"
 @JvmField
 val S4 = "s4"
 @JvmField
 internal val S5 = "s5"
}
```

</td><td>

```java
@Metadata(...)
public final class A {
  @NotNull
  private final String S1 = "s1";
  @NotNull
  private final String S2 = "s2";
  private final String S3 = "s3";
  @JvmField
  @NotNull
  public final String S4 = "s4";
  @JvmField
  @NotNull
  private final String S5 = "s5";

  @NotNull
  public final String getS1() {
    return this.S1;
  }

  @NotNull
  public final String getS2$kotlin_v1() {
    return this.S2;
  }
}
```
</td></tr>

</table>


### var

<table>
<tr><td>Kotlin</td><td>Java</td></tr>

<tr><td>

```kotlin
class B {
  var S1 : String =  "s1"
  var S2 : String? = null
  lateinit var S3 : String
}
```

</td><td>

```java
@Metadata(...)
public final class A {
  @NotNull
  private String s1;
  @Nullable
  private String s2;
  @NotNull
  public String s3;

  public A() {
    this.s1 = "s1";
  }

  @NotNull
  public final String getS1() {
    return this.s1;
  }

  public final void setS1(@NotNull final String <set-?>) {
    Intrinsics.checkParameterIsNotNull((Object)<set-?>, "<set-?>");
    this.s1 = <set-?>;
  }

  @Nullable
  public final String getS2() {
    return this.s2;
  }

  public final void setS2(@Nullable final String <set-?>) {
    this.s2 = <set-?>;
  }

  @NotNull
  public final String getS3() {
    final String s3 = this.S3;
    if (s3 == null) {
        Intrinsics.throwUninitializedPropertyAccessException("S3");
    }
    return s3;
  }

  public final void setS3(@NotNull final String <set-?>) {
    Intrinsics.checkParameterIsNotNull((Object)<set-?>, "<set-?>");
    this.s3 = <set-?>;
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

