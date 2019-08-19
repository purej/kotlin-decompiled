Kotline to Java-Compile Results

# Variables Declarations
Describes some common Kotlin member variable declarations and the resulting compiled Java code result (*.class). The result has been decompiled to show whats going on. This has been tested with IntelliJ 2019.2, OpenJdk 11 and the decompiler JD and procyon.



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
object A {
  var S1 = "s1"
  internal var S2 = "s2"
  private var S3 = "s3"
  @JvmField
  var S4 = "s4"
  @JvmField
  internal var S5 = "s5"
}
```

</td><td>

```java
@Metadata(...)
public final class A {
  @NotNull
  private static String S1;
  @NotNull
  private static String S2;
  private static String S3;
  @JvmField
  @NotNull
  public static String S4;
  @JvmField
  @NotNull
  public static String S5;
  public static final A INSTANCE;

  static {
    INSTANCE = new A();
    A.S1 = "s1";
    A.S2 = "s2";
    A.S3 = "s3";
    A.S4 = "s4";
    A.S5 = "s5";
  }

  private A() {
  }

  @NotNull
  public final String getS1() {
    return A.S1;
  }

  public final void setS1(@NotNull final String <set-?>) {
    Intrinsics.checkParameterIsNotNull((Object)<set-?>, "<set-?>");
    A.S1 = <set-?>;
  }

  @NotNull
  public final String getS2$kotlin_v1() {
    return A.S2;
  }

  public final void setS2$kotlin_v1(@NotNull final String <set-?>) {
    Intrinsics.checkParameterIsNotNull((Object)<set-?>, "<set-?>");
    A.S2 = <set-?>;
  }
}
```

</td></tr>

<tr><td>

```kotlin
class A {
  var s1 = "s1"
  internal var s2 = "s2"
  private var s3 = "s3"
  @JvmField
  var s4 = "s4"
  @JvmField
  internal var s5 = "s5"
}
```

</td><td>

```java
public final class A {
  @NotNull
  private String s1;
  @NotNull
  private String s2;
  private String s3;
  @JvmField
  @NotNull
  public String s4;
  @JvmField
  @NotNull
  public String s5;

  public A() {
    this.s1 = "s1";
    this.s2 = "s2";
    this.s3 = "s3";
    this.s4 = "s4";
    this.s5 = "s5";
  }

  @NotNull
  public final String getS1() {
    return this.s1;
  }

  public final void setS1(@NotNull final String <set-?>) {
    Intrinsics.checkParameterIsNotNull((Object)<set-?>, "<set-?>");
    this.s1 = <set-?>;
  }

  @NotNull
  public final String getS2$kotlin_v1() {
    return this.s2;
  }

  public final void setS2$kotlin_v1(@NotNull final String <set-?>) {
    Intrinsics.checkParameterIsNotNull((Object)<set-?>, "<set-?>");
    this.s2 = <set-?>;
  }
}
```

</td></tr>


<tr><td>

```kotlin
class A {
  var s1 : String? = null;
  internal var s2 : String? = null;
  private var s3 : String? = null;
  @JvmField
  var s4 : String? = null;
  @JvmField
  internal var s5 : String? = null;
}
```

</td><td>

```java
public final class A {
  @Nullable
  private String s1;
  @Nullable
  private String s2;
  private String s3;
  @JvmField
  @Nullable
  public String s4;
  @JvmField
  @Nullable
  public String s5;

  @Nullable
  public final String getS1() {
    return this.s1;
  }

  public final void setS1(@Nullable final String <set-?>) {
    this.s1 = <set-?>;
  }

  @Nullable
  public final String getS2$kotlin_v1() {
    return this.s2;
  }

  public final void setS2$kotlin_v1(@Nullable final String <set-?>) {
    this.s2 = <set-?>;
  }
}
```

</td></tr>



</table>

