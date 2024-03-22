---
name: Issue with Kotlin spring version upgrade to 3.2.x
about: open-rewrite working on Groovy but not with Kotlin DSL
title: ' '
labels: 'bug'
assignees: ' '
---
## What version of OpenRewrite are you using?
I am using
- OpenRewrite v6.10.0
- Gradle plugin both Groovy and Kotlin DSL
- org.openrewrite.recipe:rewrite-spring:5.7.0
## How are you running OpenRewrite?
I am using the gradle plugin for both Groovy and Kotlin DSL
```xml
plugins {
    id("org.openrewrite.rewrite") version("6.10.0")
}
rewrite {
    activeRecipe("org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_2")
}
repositories {
    mavenCentral()
}
dependencies {
    rewrite("org.openrewrite.recipe:rewrite-spring:5.7.0")
}
```
## What did you expect to see?
While running the above recipe I am expecting spring version update changes in build.gradle.kts / build.gradle. The expected changes take place when the kotlin repo has build.gradle but the expected changes don't take place when kotlin repo has build.gradle.kts.
```xml
# build.gradle.kts 
plugins {
id ("org.springframework.boot") version "3.2.3"
}
```
## What did you see instead?
No changes in build.gradle.kts file.
<!-- A code snippet, or a description of the behavior you saw instead of the above expected result. -->
```xml
# build.gradle.kts 
plugins {
id ("org.springframework.boot") version "3.1.3"
}
```
