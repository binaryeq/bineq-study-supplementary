# Example bytecode-level difference between Maven Central and Google Assured Open Source Software

## Overview

This folder shows the diff between the disassemblies, produced using `javap -c -p`, of 2 copies of the class `com.squareup.okhttp.Headers` from the Maven project `com.squareup.okhttp:okhttp:2.7.5`, one taken from Maven Central (mvnc) and the other from Google Assured Open Source Software (gaoss).
Each `.diff` file is produced using a command of the form `diff gaoss/X mvnc/X > X.diff`.
The two subdirectories contain the original jars from each provider and relevant files extracted from them, for convenience.
They also each contain a `Headers.javap.noindices` file produced from `Headers.javap` by removing constant pool indices and canonicalising whitespace using `perl -lpe 's/#\d+/#/g; s|\s+//| //|' < Headers.javap > Headers.javap.noindices`.
Note that `javap` leaves the referenced values in comments, which remain in the `*.noindices` files.

- File path within both binary jars: `com/squareup/okhttp/Headers.class`
- Maven Central binary jar URL: https://repo1.maven.org/maven2/com/squareup/okhttp/okhttp/2.7.5/okhttp-2.7.5.jar
- Maven Central source jar URL: https://repo1.maven.org/maven2/com/squareup/okhttp/okhttp/2.7.5/okhttp-2.7.5-sources.jar
- Google AOSS binary jar path: `com/squareup/okhttp/okhttp/2.7.5/okhttp-2.7.5.jar`
- Google AOSS source jar path: `com/squareup/okhttp/okhttp/2.7.5/okhttp-2.7.5-sources.jar`
- `*.md5` files are at the same paths with `.md5` appended

## Summary of differences

Although the two `Headers.javap` differ (see `Headers.javap.diff`), the two `Headers.javap.noindices` files are identical.
This indicates that the classes differ only in the order of constant pool entries.

## Obtaining Google AOSS files

After first [setting up Google Assured Open Source Software access](https://cloud.google.com/assured-open-source-software/docs/enable) for a [Google Cloud Platform](https://cloud.google.com/) account, and ensuring a valid service account access token is in the file `service-account-access-token`, GAOSS files can be downloaded using the following command, replacing `$P` with the path in question:

```
gcloud artifacts files download --location=us --project=cloud-aoss --repository=cloud-aoss-java $P --access-token-file=service-account-access-token
```
