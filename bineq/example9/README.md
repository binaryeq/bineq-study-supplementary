Unsoundness example Base64TestData.class in NEQ1 for section 7.3

The section of `Base64TestData.javap_cpv.diff` showing the unsoundness-revealing difference is:
```
134c134
<     ConstantValue: String 123
---
>     ConstantValue: String 124
```

Such changes can change behaviour when *another* class refers to the field.
For example, if `A.java` defines `static final cmd = "ls";` in one version and this changes to `"rm"` in the next version, another class `B.java` that constructs a Linux command to run from `A.cmd` will have very different behaviour -- but if `cmd` is not referred to within `A.java` itself, this will not be detected by the *disassembled* equivalence since unused constant values are omitted in the output of `java -c -p`.

https://github.com/apache/commons-codec/commit/48b615756d1d770091ea3322eefc08011ee8b113, retrieved 05/09/2024
