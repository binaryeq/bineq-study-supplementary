# Example bytecode-level difference between Maven Central and Google Assured Open Source Software

## Overview

This folder shows diffs between the disassembly, produced using `javap -c -p`, of 2 copies of the class `com.google.common.jimfs.Handler` from `com.google.jimfs:jimfs:1.2`, one taken from Maven Central (mvnc) and the other from Google Assured Open Source Software (gaoss).
The two subdirectories contain the original jars from each provider and relevant files extracted from them, for convenience.

- File path within both binary jars: `com/google/common/jimfs/Handler.class`
- Maven Central binary jar URL: https://repo1.maven.org/maven2/com/google/jimfs/jimfs/1.2/jimfs-1.2.jar
- Maven Central source jar URL: https://repo1.maven.org/maven2/com/google/jimfs/jimfs/1.2/jimfs-1.2-sources.jar
- Google AOSS binary jar path: `com/google/jimfs/jimfs/1.2/jimfs-1.2.jar`
- Google AOSS source jar path: `com/google/jimfs/jimfs/1.2/jimfs-1.2-sources.jar`
- `*.md5` files are at the same paths with `.md5` appended
- `MANIFEST.MF` files are extracted from the respective binary jars

## Summary of differences

The `Handler.java` source files are identical. Both `MANIFEST.MF` files have `Build-Jdk-Spec: 11`, indicating compilers from the same JDK release. Both `Handler.class` files have major version 51, minor version 0 (JDK 7).

The main difference is how line 68 of `Handler.java` is compiled:

```
      packages += "|" + parentPackage;
```

While the GAOSS bytecode creates a `StringBuilder` using its default constructor and appends the 3 components to it, the Maven Central version first calls `String.length()` twice, computing the length of the final string in order to call the 1-argument version of the `StringBuilder` constructor. The Maven Central version also redundantly calls `String.valueOf()` 3 times (on values already statically known to be `String`s).

There is also some constant pool reordering affecting the bytecode in the last 3 methods (constructor, `openConnection()`, `getHostAddress()`).

## Obtaining Google AOSS files

After first [setting up Google Assured Open Source Software access](https://cloud.google.com/assured-open-source-software/docs/enable) for a [Google Cloud Platform](https://cloud.google.com/) account, and ensuring a valid service account access token is in the file `service-account-access-token`, GAOSS files can be downloaded using the following command, replacing `$P` with the path in question:

```
gcloud artifacts files download --location=us --project=cloud-aoss --repository=cloud-aoss-java $P --access-token-file=service-account-access-token
```
