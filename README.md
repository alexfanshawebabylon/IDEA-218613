# IDEA-218613 - intellij can't run single unit test using gradle runner when filter specified in gradle
https://youtrack.jetbrains.com/issue/IDEA-218613

to demonstrate this, run `SecondTest` from intellij.

example output:

```text
Testing started at 18:01 ...
18:01:09: Executing tasks ':cleanTest :test --tests "com.two.SecondTest"'...

> Task :cleanTest
> Task :compileJava UP-TO-DATE
> Task :processResources NO-SOURCE
> Task :classes UP-TO-DATE
> Task :compileTestJava UP-TO-DATE
> Task :processTestResources NO-SOURCE
> Task :testClasses UP-TO-DATE
> Task :test
one
[0K[1mcom.one.FirstTest[m
[0K[1m  Test [22mtestAppHasAGreeting()[32m PASSED[m
two
[0K[1mcom.two.SecondTest[m
[0K[1m  Test [22mname()[32m PASSED[m
[0K[1;32mSUCCESS: [39mExecuted 2 tests in 823ms[m
BUILD SUCCESSFUL in 1s
4 actionable tasks: 2 executed, 2 up-to-date
18:01:10: Tasks execution finished ':cleanTest :test --tests "com.two.SecondTest"'.
```

we see both tests ran.
Goal is to only have SecondTest run.

I believe the problem is the filter in `build.gradle`

```groovy
    filter {
        //only run package one tests
        includeTestsMatching "com.one.*"
    }
```

I added this to my test section as I had a bdd package that I wanted to run after the unit tests.  
this is a demo of that problem.

I hope it is easily solvable.
