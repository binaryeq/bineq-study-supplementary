# Example difference in class file sets between Maven Central and Google Assured Open Source Software

## Overview

This folder shows the difference in the sets of class files included in the binary jars from 2 copies of the Maven project `org.codehaus.groovy:groovy:2.5.23`, one taken from Maven Central (mvnc) and the other from Google Assured Open Source Software (gaoss), and ignoring compiler-generated classes, multi-release classes and package-info classes.
Each `.diff` file is produced using a command of the form `diff gaoss/X mvnc/X > X.diff`.
The two subdirectories contain the original jars from each provider and relevant files extracted from them, for convenience.

- Maven Central binary jar URL: https://repo1.maven.org/maven2/org/codehaus/groovy/groovy/2.5.23/groovy-2.5.23.jar
- Maven Central source jar URL: https://repo1.maven.org/maven2/org/codehaus/groovy/groovy/2.5.23/groovy-2.5.23-sources.jar
- Google AOSS binary jar path: `org/codehaus/groovy/groovy/2.5.23/groovy-2.5.23.jar`
- Google AOSS source jar path: `org/codehaus/groovy/groovy/2.5.23/groovy-2.5.23-sources.jar`
- `*.md5` files are at the same paths with `.md5` appended

## Summary of differences

Lists of files in each jar were produced using `zipinfo -1 groovy-2.5.23.jar > groovy-2.5.23.jar.filelist`.
These file lists were sorted and duplicates were removed using `sort -u < groovy-2.5.23.jar.filelist > groovy-2.5.23.jar.filelist.uniq`.
`groovy-2.5.23.jar.filelist.uniq.diff` shows that **580 class files in the mvnc jar are missing from the gaoss jar**; none of these files are compiler-generated, multi-release or package-info classes.
All of these files are in top-level directories that appear to result from removing periods from package names.
One additional file, `META-INF/INDEX.LIST`, is also missing from the gaoss jar.

## Duplicate files in tha Google AOSS jar

Surprisingly, in addition to the files missing in gaoss, gaoss contains **two copies** of 409 files.
(It is not clear that this is a valid use of the zip format.)
The list of duplicates in `groovy-2.5.23.jar.filelist.dupes` was produced using `sort < groovy-2.5.23.jar.filelist | uniq -c | grep -v ' 1 ' > groovy-2.5.23.jar.filelist.dupes`.

For 406 of these 409 duplicate filenames, both copies have the same CRC (and thus likely the same content).
But there are **3 files that appear multiple times with different CRCs**.
These are listed in `groovy-2.5.23.jar.filelist.dupes.unequal`, with details on all 6 involved files shown in `groovy-2.5.23.jar.filelist.dupes.unequal.detail`.

These files were produced as follows:

```
# Get all filenames with CRCs prepended
unzip -lv groovy-2.5.23.jar |cut -c49- |grep '\.class$' > groovy-2.5.23.jar.filelist.withcrcs

# Get all filenames that appear with 2 or more distinct CRCs
sort < groovy-2.5.23.jar.filelist.withcrcs | uniq | cut -c11- | sort | uniq -d > groovy-2.5.23.jar.filelist.dupes.unequal

# Get the metadata (size, CRC, etc.) for all appearances of these filenames in the zip
unzip -lv groovy-2.5.23.jar|grep -Ff groovy-2.5.23.jar.filelist.dupes.unequal > groovy-2.5.23.jar.filelist.dupes.unequal.detail
```

## Obtaining Google AOSS files

After first [setting up Google Assured Open Source Software access](https://cloud.google.com/assured-open-source-software/docs/enable) for a [Google Cloud Platform](https://cloud.google.com/) account, and ensuring a valid service account access token is in the file `service-account-access-token`, GAOSS files can be downloaded using the following command, replacing `$P` with the path in question:

```
gcloud artifacts files download --location=us --project=cloud-aoss --repository=cloud-aoss-java $P --access-token-file=service-account-access-token
```
