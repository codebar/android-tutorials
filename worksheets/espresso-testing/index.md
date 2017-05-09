---
layout: page
title: Espresso UI Testing
---

## Introduction
This tutorial follows on from the [first one where you built a cookie clicker]({{ site.baseurl }}/worksheets/1-introduction/). If you worked on that tutorial already, follow along using the code you wrote previously.

If you didn't work on that tutorial, or you don't have the code anymore, you can download a completed project to follow along with [here](downloads/cookie-clicker.zip). Download the file, unzip it and then open it with Android Studio using the *Open an exisiting Android Studio project* button on the welcome screen.

## What is UI testing?
To make sure you software works properly you need to test it whenever you make a change that you want to release to your users. For something like an app you need to go through all the features of the app and make sure that nothing is broken. For even a small app this is a boring, repetative, and time consuming job. That's exactly the sort of thing which we use computers for! Automated tests are pieces of code which test that your software is working correctly for you.

We are going to write some UI tests for our cookie clicker app. A UI test is also known as a "funcational test" as it is testing the functionality of the app. There are other types of tests such as "unit tests" which you may have come across in the Javascript, Ruby, or Python tutorials.

A UI test will take a set of instrutions about what to click on and checks that the application responds correctly. They are doing the same as if you were clicking on and testing the app manually, but they can do it much quicker and they don't get bored when they have to do it for the 100th time!

First, we need to set up our testing framework.

## Setting up Espresso
We are going to be using a testing framework called [Espresso](https://google.github.io/android-testing-support-library/docs/espresso/index.html) to interact with our app and test that it is working correctly. This is a tool provided by Google themselves.

First, we need to make sure the libraries are installed correctly.

In Android Studio, expand the `Gradle Scripts` section at the bottom of the project explorer on the left. Then double click to open the `bundle.gradle (Module: app)` file. Make sure it's the `Module: app` one and not the `Project: CookieClicker` one. This is the file which describes how to build and run our Android application. We need to make sure everything is set up correctly here to let us use Espresso.

Inside the `dependencies` section, make sure that these two blocks of code are there:

```groovy
androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
    exclude group: 'com.android.support', module: 'support-annotations'
})
```

And:

```groovy
testCompile 'junit:junit:4.12'
```

They might already be there depending on how you created your project. If they aren't, add them in. These lines tell the Android build system which version of the Espresso library to use.

Also, make sure that this line in the your `android.defaultConfig` section:

```groovy
testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
```

The complete file should look something like this (don't worry if yours has some extra bits:

```groovy
apply plugin: 'com.android.application'

android {
    compileSdkVersion 25
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "io.codebar.cookieclicker"
        minSdkVersion 14
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:25.3.1'
    compile 'com.android.support.constraint:constraint-layout:1.0.2'

    testCompile 'junit:junit:4.12'
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
}
```

Press the *Sync Now* button in the bar which has appears along the top. If the bar disappears after syncing then everything is set up correctly! If the bar shows and error message and a *Try Again* button then something has gone wrong. Take a look at the error at the bottom of the screen to see if you can fix it, or ask your coach for help.

## Writing our first test

## Getting a high score!

## Using the test recorder

## Further information
