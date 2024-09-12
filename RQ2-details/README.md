# RQ2 Details


## Bitwise Equality

Number of artifacts with some .class files that are included in binary jars from both providers, but those files have non-equivalent contents. Strict bitwise equivalence comparison is used. The total number of such pairs is **3,750**.


|       | mvnc  | gaoss | rh1   | rh2   | obfs |
|-------|-------|-------|-------|-------|------|
| mvnc  | 0     | 400   | 1,490 | 1,467 | 45   |
| gaoss | -     | 0     | 54    | 54    | 9    |
| rh1   | -     | -     | 0     | 214   | 8    |
| rh2   | -     | -     | -     | 0     | 9    |
| obfs  | -     | -     | -     | -     | 0    |

## Disassembled Equivalence

Number of artifacts with some .class files that are included in binary jars from both providers, but those files have non-equivalent contents. Equivalence is based in same disassembly (javap -p -c). The total number of such pairs is **2,776**.

|       | mvnc  | gaoss | rh1   | rh2   | obfs |
|-------|-------|-------|-------|-------|------|
| mvnc  | 0     | 361   | 1,077 | 1,055 | 32   |
| gaoss | -     | 0     | 47    | 46    | 7    |
| rh1   | -     | -     | 0     | 134   | 8    |
| rh2   | -     | -     | -     | 0     | 9    |
| obfs  | -     | -     | -     | -     | 0    |



## Decompiled Equivalence

Number of artifacts with some .class files that are included in binary jars from both providers, but those files have non-equivalent contents. Equivalence is based on decompilation (using fernflower). The total number of such pairs is **2,366**.

|       | mvnc                       | gaoss                     | rh1                        | rh2                        | obfs                      |
|-------|----------------------------|---------------------------|----------------------------|----------------------------|---------------------------|
| mvnc  | 0                          | 316 	err: 10 | 871 err: 70 | 850 err: 72 | 18 err: 17 |
| gaoss | -           | 0                         | 17 err: 6   | 16 err: 6   | 7                         |
| rh1   | -           | -          | 0                          | 69 err: 10  | 5                         |
| rh2   | -           | -          | -      | 0                          | 6                         |
| obfs  | -           | -          | -                             | -                           | 0    




## JNorm-Based Equivalence

Number of artifacts with some .class files that are included in binary jars from both providers, but those files have non-equivalent contents. Equivalence is based in same jnorm representation. The total number of such pairs is **2,231**.

|       | mvnc                       | gaoss                     | rh1                        | rh2                        | obfs                     |
|-------|----------------------------|---------------------------|----------------------------|----------------------------|--------------------------|
| mvnc  | 0                          | 314 	err: 28 | 810 err: 80 | 781 err: 77 | 32 err: 1 |
| gaoss | -  | 0                         | 15                         | 15                         | 7                        |
| rh1   | -  | -                         | 0                          | 44 err: 16  | 5                        |
| rh2   | -  | -                         | -   | 0                          | 6                        |
| obfs  | -  | -                         | -                           | -                          | 0                        |



## JNorm2-Based Equivalence

Number of artifacts with some .class files that are included in binary jars from both providers, but those files have non-equivalent contents. Equivalence is based in same jnorm representation (using aggressive normalisation ("-o -n -s -a -p")). The total number of such pairs is **1,932**.

|       | mvnc                        | gaoss                      | rh1                         | rh2                         | obfs                     |
|-------|-----------------------------|----------------------------|-----------------------------|-----------------------------|--------------------------|
| mvnc  | 0                           | 151 	err: 131 | 555 err: 215 | 536 err: 207 | 24 err: 8 |
| gaoss | -       | 0                          | 9 err: 8     | 8 err: 9     | 1 err: 3  |
| rh1   | -       | -     | 0                           | 31 err: 30   | 1 err: 2  |
| rh2   | -       | -     | -    | 0                           | 1 err: 2  |
| obfs  | -       | -     | -    | -     | 0                        |


## TLSH10-Based Equivalence

Number of artifacts with some .class files that are included in binary jars from both providers, but those files have non-equivalent contents. Equivalence is based on tlsh10. The total number of such pairs is **3,397**.

|       | mvnc  | gaoss | rh1   | rh2   | obfs |
|-------|-------|-------|-------|-------|------|
| mvnc  | 0     | 386   | 1,361 | 1,342 | 43   |
| gaoss | -  | 0     | 51    | 51    | 9    |
| rh1   | -  | -     | 0     | 141   | 6    |
| rh2   | -  | -     | -     | 0     | 7    |
| obfs  | -  | -     | -     | -     | 0    |


## TLSH100-Based Equivalence


Number of artifacts with some .class files that are included in binary jars from both providers, but those files have non-equivalent contents. Equivalence is based on tlsh100. The total number of such pairs is **2,012**.


|       | mvnc | gaoss | rh1 | rh2 | obfs |
|-------|------|-------|-----|-----|------|
| mvnc  | 0    | 306   | 785 | 774 | 20   |
| gaoss | -    | 0     | 25  | 23  | 7    |
| rh1   | -    | -     | 0   | 63  | 4    |
| rh2   | -    | -     | -   | 0   | 5    |
| obfs  | -    | -     | -   | -   | 0    |













