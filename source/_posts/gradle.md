---
title: Gradle configuration in Andorid
date: 2019-03-24 10:43:23
tags:
---

## Difference between implementation and compile in Gradle

After updating to Android Studio 3.0 and creating a new project, I noticed that in build.gradle there is a new way to add new dependencies instead of compile there is implementation and instead of testCompile there is testImplementation.
 
 ---

Just replace:

* compile with implementation
* testCompile with testImplementation
* debugCompile with debugImplementation
* androidTestCompile with androidTestImplementation

compileOnly is still valid. It was added in 3.0 to replace provided and not compile. (provided introduced when Gradle didn't have a configuration name for that use-case and named it after Maven's provided scope.)
It is one of the breaking changes coming with Gradle 3.0 that Google announced at IO17.

The compile configuration is now deprecated and should be replaced by implementation or api

From the Gradle documentation:

> dependencies {
>    api 'commons-httpclient:commons-httpclient:3.1'
>    implementation 'org.apache.commons:commons-lang3:3.5'
> }
> Dependencies appearing in the api configurations will be transitively exposed to consumers of the library, and as such will appear on the compile classpath of   consumers.

> Dependencies found in the implementation configuration will, on the other hand, not be exposed to consumers, and therefore not leak into the consumers' compile classpath. This comes with several benefits:

> dependencies do not leak into the compile classpath of consumers anymore, so you will never accidentally depend on a transitive dependency
faster compilation thanks to reduced classpath size
less recompilations when implementation dependencies change: consumers would not need to be recompiled
cleaner publishing: when used in conjunction with the new maven-publish plugin, Java libraries produce POM files that distinguish exactly between what is required to compile against the library and what is required to use the library at runtime (in other words, don't mix what is needed to compile the library itself and what is needed to compile against the library).
The compile configuration still exists, but should not be used as it will not offer the guarantees that the api and implementation configurations provide.

Note: if you are only using a library in your app module -the common case- you won't notice any difference.
you will only see the difference if you have a complex project with modules depending on each other, or you are creating a library.