# Filtering of Maven property property project.parent.basedir does not work withuin IntelliJ

IntelliJ IDEA does not recognize Maven property `project.parent.basedir` during filtering although it does filter properties `project.basedir` or `project.parent.artifactId` in the same file correctly.

I set up a minimal repo for reproduction at https://github.com/akloeber/intellij-filtering-bug.

Upon (re)building the project in IntelliJ, file `application.properties` gets filtered to `child/target/classes/application.properties` with the following content:
```properties
foo1=/Users/aske/Repos/intellij-filtering-bug/child
foo2=${project.parent.basedir}
foo3=parent
```

Running Maven from the command line via `mvn resources:resources` produces:
```properties
foo1=/Users/aske/Repos/intellij-filtering-bug/child
foo2=/Users/aske/Repos/intellij-filtering-bug
foo3=parent
```

##Environment:

IntelliJ IDEA 2018.2.4 (Ultimate Edition)
Build #IU-182.4505.22, built on September 18, 2018
Licensed to GFT Technologies SE / Andreas Klöber
Subscription is active until June 12, 2019
JRE: 1.8.0_152-release-1248-b8 x86_64
JVM: OpenJDK 64-Bit Server VM by JetBrains s.r.o
macOS 10.13.6- maven 3.5.2
maven-resources-plugin 3.1.0

