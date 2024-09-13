# Example source-level difference between Maven Central and RedHat Earliest

## Overview

This folder compares source code for 2 copies of the class `org.apache.commons.text.numbers.DoubleFormat` from the Maven project `org.apache.commons:commons-text:1.11.0`, one taken from Maven Central (mvnc) and the other from RedHat Earliest (rh1).
Each `.diff` file is produced using a command of the form `diff mvnc/X rh1/X > X.diff`.
The two subdirectories contain the original source jars from each provider and relevant files extracted from them, for convenience.

- File path within both source jars: `org/apache/commons/text/numbers/DoubleFormat.java`
- Maven Central source jar URL: https://repo1.maven.org/maven2/org/apache/commons/commons-text/1.11.0/commons-text-1.11.0-sources.jar
- RedHat source jar URL: https://maven.repository.redhat.com/ga/org/apache/commons/commons-text/1.11.0.redhat-00001/commons-text-1.11.0.redhat-00001-sources.jar
- GitHub repo source jar at tag `rel/commons-text-1.11.0` URL: https://github.com/apache/commons-text/archive/refs/tags/rel/commons-text-1.11.0.zip
- `*.md5` files are at the same URLs with `.md5` appended

## Summary of differences

The 2 source files differ by manual changes which leave them behaviourally equivalent, though this cannot be easily verified with a simple syntactic comparison.
Specifically, the RedHat version of the sources does not explicitly initialise some fields, whereas the Maven one does.
Example:
 
```
366c366
<         private int maxPrecision = 0;
---
>         private int maxPrecision;
```

## Maven Central source disagrees with source repo

The [version downloaded from the GitHub source repo with tag `rel/commons-text-1.11.0`](https://github.com/apache/commons-text/archive/refs/tags/rel/commons-text-1.11.0.zip) contains `DoubleFormat.java` consistent with the RedHat version.

The explicit initialisations were removed in https://github.com/apache/commons-text/commit/d5e8a73e7b9e06f71a5c66576b428e6c34b3c684, which is included in https://github.com/apache/commons-text/releases/tag/rel%2Fcommons-text-1.11.0.
This indicates that the version used to build the sources on Maven Central must have preceded this.




