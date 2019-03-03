---
title: Setup up reactive native platform
date: 2019-03-03 21:14:12
tags:
---

## Major step

I follow the guide in react offical website, major step is as follow

1. Install Java sdk, python and node.js
2. Install Android studio
3. Install Android SDK
4. Set user variables in environment variables
5. Set Path in environment variables
6. Create Android Virtual Device

I have met one issue, when installing Android Studio, it stunk at install HAXM intel X86 emulator and then whne I try to launch emulator, an error related HAXM happens, I solved the issue using below solution

>  Had the same problem in windows 10, which was solved by disabling Hyper-v and reinstalling HAXM via SDK Manager>SDK Tools>Intel x86 Emulator Accelerator


## Issues when debugging

1. FAILURE: Build failed with an exception.

* Where:
Build file '/home/jose/tmp/react-native-unity-demo/android/app/build.gradle' line: 129

* What went wrong:
A problem occurred evaluating project ':app'.
>Could not get unknown property 'MYAPP_RELEASE_STORE_FILE' for SigningConfig_Decorated{name=release, storeFile=null, storePassword=null, keyAlias=null, keyPassword=null, storeType=null, v1SigningEnabled=true, v2SigningEnabled=true} of type com.android.build.gradle.internal.dsl.SigningConfig.

* I need to generate a signing key for some reason, follow below step and remember generate it using powershell and as administrator 
http://facebook.github.io/react-native/docs/signed-apk-android.html

 I create a key with both password as test11

 2. A problem occurred evaluating project ':react-native-share'.
> Could not find method goole() for arguments [com.facebook.react:react-native:+] on object of type org.gradle.api.internal.artifacts.dsl.dependencies.DefaultDependencyHandler

SOLUTION: I follow this guide of a similar problem with the maps plugin of react.(Link to guide)[https://itnext.io/install-react-native-maps-with-gradle-3-on-android-44f91a70a395]

the following steps are the ones that work for me:

* Modify android/build.gradle

Add google() inside repositories

buildscript {
    repositories {
        jcenter()
        // add google() here
        google()
* Update com.android.tools.build.gradle to 3.1.0

buildscript {
    repositories {
        jcenter()
        google()
    }
    dependencies {
      // classpath 'com.android.tools.build:gradle:2.2.3'
      // update from 2.2.3 to 3.1.0 
      classpath 'com.android.tools.build:gradle:3.1.0'
* Add google() inside repositories after dependencies

buildscript {
    repositories {
        jcenter()
        google()
    }
    dependencies {
      classpath 'com.android.tools.build:gradle:3.1.0'
    }
    allprojects {
      repositories {
        mavenLocal()
        jcenter()
        // add googgle() here
        google()
* Add android.enableAapt2=false to android/gradle.properties

android.enableAapt2=false // < ---  add here
android.useDeprecatedNdk=true
* Update gradle version in android/gradle/wrapper/gradle-wrapper.properties

// from version 2.14.1
distributionUrl=https\://services.gradle.org/distributions/gradle-2.14.1-all.zip
// change to 4.4
distributionUrl=https\://services.gradle.org/distributions/gradle-4.4-all.zip
* Run react-native run-android. (This might take a while since it’ll be downloading the updated gradle version).

3. Execution failed for task ':app:preDebugBuild'. > Android dependency 'com.android.support:appcompat-v7' has different version for the compile (27.1.1) and runtime (28.0.0) classpath. You should manually set the same version via DependencyResolution

I solved by adding
subprojects {
    project.configurations.all {
        resolutionStrategy.eachDependency { details ->
            if (details.requested.group == 'com.android.support'
                    && !details.requested.name.contains('multidex') ) {
                details.useVersion "27.1.1"
            }
        }
    }

 4. No resource found that matches the given name: attr 'android:keyboardNavigationCluster'. 
 

Since I change the useVerison to 27.1.1, then I need to change that in android/app/build.gradle as well
 compileSdkVersion 27
 buildToolsVersion "27.0.3"

 5. error: bundling: UnableToResolveError: Unable to resolve module `rn-fetch-blob` from `C:\PrivateAppDev\React-native\GitterMobile\node_modules\react-native-img-cache\build\index.js`: Module does not exist in the module map or in these directories:
  C:\PrivateAppDev\React-native\GitterMobile\node_modules

This might be related to https://github.com/facebook/react-native/issues/4968
To resolve try the following:
  1. Clear watchman watches: `watchman watch-del-all`.
  2. Delete the `node_modules` folder: `rm -rf node_modules && npm install`.
  3. Reset packager cache: `rm -fr $TMPDIR/react-*` or `npm start -- --reset-cache`.