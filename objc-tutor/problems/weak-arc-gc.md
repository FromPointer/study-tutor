#About Problem: @synthesize of ‘weak’ property is only allowed in ARC or GC mode

## 1. Solution 1
    `assign` instead of `weak` keyword

#####This solution is not good, so we need to find a more method.

##2. Solution 2
###2.1 Commond line
    For Error `file`, we add compiler option in compiler.
    clang -fobjc-arc -c main.m -o main.o
    ######or
    clang -fojbc-gc -c main.m -o main.o



###2.2 In xcode Tool

#####In Project configuration file -> Build Phrases -> Compiler Sources ,
Find Error Source `file`(use `weak` file), double click the file, and then 
write `-fobjc-arc` or `-fobjc-gc`

