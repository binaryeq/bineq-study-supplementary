# Example bytecode-level difference between Maven Central and Oracle Build-From-Source normalised by `javap -c -p`

## Overview

This folder shows a difference at the `bytewiseidentical` equivalence level between 2 copies of the class `module-info` from the Maven project `jakarta.ws.rs:jakarta.ws.rs-api:3.1.0`, one taken from Maven Central (mvnc) and the other from Oracle Build-From-Source (obfs).
This difference is "normalised away" at the `disassembled` equivalence level (running `javap -c -p`), demonstrating the utility of this equivalence level.

Each `.diff` file is produced using a command of the form `diff mvnc/X obfs/X > X.diff`:
- `all.class.md5.diff`: MD5 hashes of class files
- `module-info.javap_cpv.diff`: verbose disassemblies (produced using `javap -c -p -v`)
- `MANIFEST.MF.diff`: manifests

The two subdirectories contain the original jars from each provider and relevant files extracted from them, for convenience.

- File path within both binary jars: `module-info.class`
- Maven Central binary jar URL: https://repo1.maven.org/maven2/jakarta/ws/rs/jakarta.ws.rs-api/3.1.0/jakarta.ws.rs-api-3.1.0.jar
- Maven Central source jar URL: https://repo1.maven.org/maven2/jakarta/ws/rs/jakarta.ws.rs-api/3.1.0/jakarta.ws.rs-api-3.1.0-sources.jar
- Oracle Build-From-Source binary jar URL: https://github.com/binaryeq/bfs-dataset/blob/main/maven-artifacts/jakarta/ws/rs/jakarta.ws.rs-api/3.1.0/jakarta.ws.rs-api-3.1.0.jar
- Oracle Build-From-Source source jar URL: https://github.com/binaryeq/bfs-dataset/blob/main/maven-artifacts/jakarta/ws/rs/jakarta.ws.rs-api/3.1.0/jakarta.ws.rs-api-3.1.0-sources.jar
- `*.md5` files are at the same URLs with `.md5` appended for mvnc; these were generated locally for obfs
- `MANIFEST.MF` files are extracted from the respective binary jars

## Summary of differences

As `all.class.md5.diff` shows, `module-info.class` differs between the two providers (in fact it is the only nonidentical class file present in both binary jars).
`module-info.javap_cpv.diff` shows in more detail that the two class files contain two different version strings.
However, since these strings are stored in the constant pool, which is not output by `javap -c -p`, the `module-info.javap_cp` files in each subdirectory (produced using `javap -c -p`; `disassembled` in the paper) are identical.
This shows the ability of the `disassembled` equivalence level to normalise away such differences, which in practice are often uninteresting.

The obfs binary jar also contains 6 `package-info.class` files that are not present in the mvnc jar.

The `module-info.class` files have the same major and minor versions (55 and 0, respectively -- JDK11).
The manifests have `Build-Jdk` fields that differ only in the patch-level version: `11.0.2` for mvnc, `11.0.22` for obfs, suggesting very similar build environments.
There are also manifest differences in the `Bnd-LastModified` timestamps, `Built-By` and `Export-Package` fields.
