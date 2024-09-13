DoubleFormat example for section 2.4 (source equivalence)





Here is an explanation for the non-matching source issue we had observed in org/apache/commons/text/numbers/DoubleFormat.java in commons-text-1.11.0.

 

The RH version of the sources does not explicitly initialize some fields, whereas the Maven one does. Example:

 

private int maxPrecision;

private int maxPrecision = 0;

 

The version downloaded from the source repo is

https://github.com/apache/commons-text/archive/refs/tags/rel/commons-text-1.11.0.zip , this contains DoubleFormat.java consistent with the RH version.

The changes were made in this commit:

 

https://github.com/apache/commons-text/commit/d5e8a73e7b9e06f71a5c66576b428e6c34b3c684

 

This is correctly included in https://github.com/apache/commons-text/releases/tag/rel%2Fcommons-text-1.11.0 , however, the version used to build the sources on Maven Central (https://repo1.maven.org/maven2/org/apache/commons/commons-text/1.11.0/commons-text-1.11.0-sources.jar)  must have preceded this. So they used a different commit to deploy.
