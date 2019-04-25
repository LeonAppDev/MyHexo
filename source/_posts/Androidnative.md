---
title: Android native development
date: 2019-04-01 09:44:51
tags:
---

## Issues I met when running UMAndroidSdkDemo from android studio

1. NDK not configured

Tape 
```
ctrl+shift+a
``` 
and input 
```
project structure
```
and download Android NDK from pop-up window.

2. Gradle structure need update

Follow the instruction by android studio and update

3. The SourceSet 'instrumentTest' is not recognized by the Android Gradle Plugin

instrumentTest has been deprecated and does not work with modern Gradle versions - which you probably updated in your project when upgrading Android Studio.

Replace instrumentTest with androidTest(In all app) and it'll work.

4. The minSdk version should not be declared in the android manifest file

Inside your manifest there must be inside which minsdkversion might have been written. Just remove 

```
<uses-sdk>....</uses-sdk>
```

5. Could not find com.android.tools.build:aapt2:3.3.1-5013011.

Beginning with Android Studio 3.2 Canary 11, the source for AAPT2 (Android Asset Packaging Tool 2) is Google's Maven repository. To use AAPT2, make sure that you have a google() dependency in your build.gradle file, as shown here:

```
buildscript {
  repositories {
      google() // here
      jcenter()
  }
  dependencies {
      classpath 'com.android.tools.build:gradle:3.2.0-alpha12'
  }
} 
allprojects {
  repositories {
      google() // and here
      jcenter()
  }
}

```
For me, I just add buildscript and then it works

6. Could not find com.android.tools.build:aapt2:3.2.0

This is also related with configuration, I follow the instruction 
buildscript {
  repositories {
      google() // here
      jcenter()
  }
  dependencies {
      classpath 'com.android.tools.build:gradle:3.2.0-alpha12'
  }
} 
allprojects {
  repositories {
      google() // and here
      jcenter()
  }
}

7. org.gradle.internal.UncheckedException: com.android.build.api.transform.TransformException: java.lang.RuntimeException: java.lang.RuntimeException: com.android.builder.dexing.DexArchiveMergerException: Error while merging dex archives: 

This seems an error opening a project developed by old version of Android studio(2.x) when using new version of Android studio(3.x) 

There are several sources describing about this issue as well as collecting information for debug, below is the two pages

!(org.gradle.api.tasks.TaskExecutionException)[https://www.jianshu.com/p/e83b2aa15965]
!(DexArchiveMergerException)[https://www.jianshu.com/p/a08d49f3bf8b]

## Run app in a real device

Follow developers guide, first you need to solve all build error, then you could select a Deployment Target.