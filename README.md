# Kotline to Java / Decompile Results
Describes some Kotlin declarations and the resulting compiled Java code result (*.class). The result has been decompiled to show whats going on. This has been tested with IntelliJ 2019.2, OpenJdk 11 and the decompilers JD, procyon and CFR (some do no understand all kotlin-compiled constructs, see [Java Decompilers](http://www.javadecompilers.com/)).

1.) [Object / Class](object-class.md)

2.) [Member Variables](member-variables.md)

3.) [Constructors](constructors.md)

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

## Other Kotlin internal classes
The package kotlin.jvm.internal constains some classes that are required at runtime, as they are compiled into the resulting
class files. Some of the mostly seen are:

The Intrinsics class [kotlin.jvm.internal.Intrinsics](https://github.com/JetBrains/kotlin/blob/master/libraries/stdlib/jvm/runtime/kotlin/jvm/internal/Intrinsics.java) contains the some sanity check logic used for example for not-null properties (without ?) and other constraint-checks.

The DefaultConstructorMarker class [kotlin.jvm.internal.DefaultConstructorMarker](https://github.com/JetBrains/kotlin/blob/master/libraries/stdlib/jvm/runtime/kotlin/jvm/internal/DefaultConstructorMarker.java) is just an empty class that gets added as last parameter to constructors with default-value logic.


