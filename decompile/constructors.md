Kotline to Java-Compile Results

# Constructors
Describes some Kotlin declarations and the resulting compiled Java code result (*.class). The result has been decompiled to show whats going on. This has been tested with IntelliJ 2019.2, OpenJdk 11 and the decompilers JD, procyon and CFR (some do no understand all kotlin-compiled constructs, see [Java Decompilers](http://www.javadecompilers.com/)).



### Primary Constructors

<table>
<tr><td>Kotlin</td><td>Java</td></tr>

<tr><td>

```kotlin
object A {
}
object A() {
}
object A constructor() {
}
```

</td><td>

```java
@Metadata(...)
public final class A {
}
```
</td></tr>


<tr><td>

```kotlin
class A() {
  init {
    println("hello")
  }
}
```

</td><td>

```java
public final class A {
  public A() {
    System.out.println((Object)"hello");
  }
}
```

</td></tr>



<tr><td>

```kotlin
class A(val a: String) {
}
class A(a: String) {
  val a: String
  init {
    this.a = a;
  }
}
```

</td><td>

```java
public final class A {
  @NotNull
  private final String a;

  public A(@NotNull final String a) {
    Intrinsics.checkParameterIsNotNull((Object)a, "a");
    this.a = a;
  }

  @NotNull
  public final String getA() {
    return this.a;
  }
}

```
</td></tr>


<tr><td>

```kotlin
class A(val a: String) {
  init {
    println("hello")
  }
}
```

</td><td>

```java
public final class A {
  @NotNull
  private final String a;

  @NotNull
  public final String getA() {
    return this.a;
  }

  public A(@NotNull final String a) {
    Intrinsics.checkParameterIsNotNull((Object)a, "a");
    this.a = a;
    System.out.println((Object)"hello");
  }
}
```

</td></tr>


<tr><td>

```kotlin
class A(val a: String = "x", val b: String = "y", val c: String = "z") {
}
```

</td><td>

```java
public final class A {
  @NotNull
  private final String a;
  @NotNull
  private final String b;
  @NotNull
  private final String c;

  public A(@NotNull String a, @NotNull String b, @NotNull String c) {
      Intrinsics.checkParameterIsNotNull((Object)a, (String)"a");
      Intrinsics.checkParameterIsNotNull((Object)b, (String)"b");
      Intrinsics.checkParameterIsNotNull((Object)c, (String)"c");
      this.a = a;
      this.b = b;
      this.c = c;
  }

  public A() {
    this(null, null, null, 7, null);
  }

  public /* synthetic */ A(String string, String string2, String string3, int n, DefaultConstructorMarker defaultConstructorMarker) {
    if ((n & 1) != 0) {
      string = "x";
    }
    if ((n & 2) != 0) {
      string2 = "y";
    }
    if ((n & 4) != 0) {
      string3 = "z";
    }
    this(string, string2, string3);
  }

  @NotNull
  public final String getA() {
      return this.a;
  }

  @NotNull
  public final String getB() {
      return this.b;
  }

  @NotNull
  public final String getC() {
      return this.c;
  }
}
```

</td></tr>


</table>


