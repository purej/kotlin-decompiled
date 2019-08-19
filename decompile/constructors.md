Kotline to Java-Compile Results

# Constructors
Describes some Kotlin declarations and the resulting compiled Java code result (*.class). The result has been decompiled to show whats going on. This has been tested with IntelliJ 2019.2, OpenJdk 11 and the decompiler JD and procyon.



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


</table>


