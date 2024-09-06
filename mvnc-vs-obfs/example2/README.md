# Example bytecode-level difference between Maven Central and Oracle Build-From-Source

## Overview

This folder shows differences at several equivalence levels between 2 copies of the class `ch.qos.logback.access.net.AccessEventPreSerializationTransformer` from the Maven project `ch.qos.logback:logback-access:1.3.11`, one taken from Maven Central (mvnc) and the other from Oracle Build-From-Source (obfs).
In particular, it shows that **the main difference is not normalised away by JNorm, even with maximum normalisation turned on.**

Each `.diff` file is produced using a command of the form `diff mvnc/X obfs/X > X.diff`:
- `AccessEventPreSerializationTransformer.javap.diff`: disassemblies (produced using `javap -c -p`, `disassembly` in the paper)
- `AccessEventPreSerializationTransformer.jnorm.jimple.diff`: Jimple (bytecode normalised using JNorm with default settings, `jnorm` in the paper)
- `AccessEventPreSerializationTransformer.jnorm2.jimple.diff`: Jimple (bytecode normalised aggressively using JNorm with `-o -n -s -a -p` flags, `jnorm2` in the paper)

The two subdirectories contain the original jars from each provider and relevant files extracted from them, for convenience.

- File path within both binary jars: `ch/qos/logback/access/net/AccessEventPreSerializationTransformer.class`
- Maven Central binary jar URL: https://repo1.maven.org/maven2/ch/qos/logback/logback-access/1.3.11/logback-access-1.3.11.jar
- Maven Central source jar URL: https://repo1.maven.org/maven2/ch/qos/logback/logback-access/1.3.11/logback-access-1.3.11-sources.jar
- Oracle Build-From-Source binary jar URL: https://github.com/binaryeq/bfs-dataset/blob/main/maven-artifacts/ch/qos/logback/logback-access/1.3.11/logback-access-1.3.11.jar
- Oracle Build-From-Source source jar URL: https://github.com/binaryeq/bfs-dataset/blob/main/maven-artifacts/ch/qos/logback/logback-access/1.3.11/logback-access-1.3.11-sources.jar
- `*.md5` files are at the same URLs with `.md5` appended
- `MANIFEST.MF` files are extracted from the respective binary jars

## Summary of differences

The `AccessEventPreSerializationTransformer.java` source files are identical except for line endings. The `MANIFEST.MF` files have different `Build-Jdk-Spec` fields: 17 for obfs, 20 for mvnc, as well as other small differences (in `Export-Package`, `Import-Package` and `Require-Capability`, and the presence of `Originally-Created-By: Apache Maven Bundle Plugin 5.1.8` in mvnc which is absent in obfs). Both `AccessEventPreSerializationTransformer.class` files have major version 52, minor version 0 (JDK 8).

The main difference is how the expression `event.getClass()` on line 29 of `AccessEventPreSerializationTransformer.java` is compiled:

```
            throw new IllegalArgumentException("Unsupported type " + event.getClass().getName());
```

The OBFS bytecode calls `getClass()` using an `invokevirtual` instruction, while the Maven Central version uses `invokeinterface` instead.
This difference results from [a change made to `javac` in JDK18](https://github.com/openjdk/jdk/pull/5165) to reflect the fact that interfaces do not inherit from `java.lang.Object`, but instead have "mirrors" of the public methods of `java.lang.Object` ([JLS 9.2](https://docs.oracle.com/javase/specs/jls/se18/html/jls-9.html#jls-9.2)). Since `IAccessEvent` is an interface, calling `event.getClass()` is technically calling the mirror method on the interface, not the method on `java.lang.Object`.

There is also some constant pool reordering affecting indices used in the remaining bytecode.
