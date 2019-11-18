---
id: espresso
title: Espresso UI Testing
---

# Espresso UI Testing

## Introduction
This tutorial follows on from the [first one where you built a cookie clicker](cookie-clicker-java). If you worked on that tutorial already, follow along using the code you wrote previously.

## What is UI testing?
To make sure your software works properly you need to test it whenever you make a change that you want to release to your users. To do this manually for even a small app this is a boring, repetitive, and time-consuming job. That's precisely the sort of thing which we use computers for! Automated tests are pieces of code which test that your software is working correctly. You can set them up to run regularly and on many devices so you don't have to manually test your app every time you make a change. Plus they're usually simple and fun to create!

We are going to write some UI tests for our cookie clicker app. A UI test is also known as a "functional test" as it is testing the functionality of the app. There are other types of tests such as "unit tests" which you may have come across in the Javascript, Ruby, or Python tutorials.

A UI test will take a set of instructions about what to click on and checks that the application responds correctly. For example, on a sign in screen you might have an espresso test to check that an error appears if you enter an email address with the wrong format. UI tests are doing the same thing as if you were clicking on and testing the app manually, but they can do it much quicker, and they don't get bored when they have to do it for the 100th time!

First, we need to set up our testing framework.

## Setting up Espresso
We are going to be using a testing framework called [Espresso](https://google.github.io/android-testing-support-library/docs/espresso/index.html) to interact with our app and test that it is working correctly. This is a tool provided by Google themselves.

First, we need to make sure the libraries are installed correctly.

In Android Studio, expand the `Gradle Scripts` section at the bottom of the project explorer on the left. Then double click to open the `build.gradle (Module: app)` file. Make sure it's the `Module: app` one and not the `Project: CookieClicker` one. This is the file which describes how to build and run our Android application. We need to make sure everything is set up correctly here to let us use Espresso.

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

Also, make sure that this line is in your `android.defaultConfig` section:

```groovy
testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
```

The complete file should look something like this (_Don't copy this as some of your settings will need to be left as they were before. Also, don't worry if yours has some extra bits. Ask your coach if you aren't sure if you have done it correctly_):

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

Press the *Sync Now* button in the golden yellow bar which has appeared along the top of the code editor window. If the bar disappears after syncing, then everything is set up correctly! If the bar shows and error message and a *Try Again* button then something has gone wrong. Take a look at the error at the bottom of the screen to see if you can fix it, or ask your coach for help.

## Writing our first test
Now we have everything set up; we can write our first test!

In the project navigator on the left panel of Android Studio, navigate through `app -> java -> <package name> (androidTest)` where `<package name>` is the name you used when you set up the project. Right click on the `(androidTest)` line and choose `New -> Java Class`. In the window which pops up, give it a name of `CookieClickerTest` and then press `OK`. This will create and open a file which looks like this:

```java
package io.codebar.cookieclicker;

public class CookieClickerTest {
}
```

Above the `public class` line, add in this line:

```java
@RunWith(AndroidJUnit4.class)
```

Remember to use the autocomplete as much as possible as it will also add in some `import` lines above for you. This line tells Android how to run the tests we are about to write.

Inside the `class` add the following line:

```java
@Rule
public ActivityTestRule<MainActivity> activityTestRule = new ActivityTestRule<>(MainActivity.class);
```

This is a "test rule" and test Espresso which activity (part of our app) we want to test. We have chosen the `MainActivity`. This rule will make Espresso open this activity before running our test so we can see the cookie clicker and test it is working.

We now need to actually write some test code. Inside the `class`, create a new method called `totalStartsAtZero`. It should look like this:

```java
@Test
public void totalStartsAtZero() throws Exception {

}
```

We will be writing one of these methods for each test that we want to perform. As you can guess from the name, we are first going to check that the counter starts off at zero.

Inside the method, write the following code:

```java
onView(withId(R.id.lblTotal))
    .check(matches(withText("0")));
```

So what are we doing here? The first line (`onView`) is finding the view which matches the requirements we have given to it. We have asked for the view with the id of `lblTotal` using `withId(R.id.lblTotal)`. Remember that this is the id we gave to our `TextView` in the first tutorial in the `activity_main.xml` layout file. The second line is checking that the view matches some conditions. We are checking that the view has the text `"0"` using `withText("0")`.

This pattern of getting the view with a set of requirements and then checking something with it forms the basis of how Espresso tests work.

The completed test file should now look like this (_remember, don't copy this directly as some of your code (such as the package name) need to be different. As your coach if you are not sure_):

```java
package io.codebar.cookieclicker;

import android.support.test.rule.ActivityTestRule;
import android.support.test.runner.AndroidJUnit4;

import org.junit.Rule;
import org.junit.Test;
import org.junit.runner.RunWith;

import static android.support.test.espresso.Espresso.onView;
import static android.support.test.espresso.assertion.ViewAssertions.matches;
import static android.support.test.espresso.matcher.ViewMatchers.withId;
import static android.support.test.espresso.matcher.ViewMatchers.withText;

@RunWith(AndroidJUnit4.class)
public class CookieClickerTest {
    @Rule
    public ActivityTestRule<MainActivity> activityTestRule = new ActivityTestRule<>(MainActivity.class);

    @Test
    public void totalStartsAtZero() throws Exception {
        onView(withId(R.id.lblTotal))
                .check(matches(withText("0")));
    }
}

```

Let's run our test to make sure the app is working correctly. Press the "play" button to the left of the method and pick your Android device or emulator to run the tests on. This might take a short amount of time but the app should appear and then quickly disappear, and Android Studio should show a "Tests passed" message. This might even be too quick to see, and that's the advantage of using automated tests! Run it a few times if you want to test it is working all the time.

![Test passing](assets/espresso/test_passing.png)

Just to see what happens when a test fails, change the check to look for `"1"` and run the test again. You should see an error message saying what happened and some hints on how to fix it. There's a lot of information there, but there's normally enough to know what went wrong.

![Test failing](assets/espresso/test_failing.png)

Change you test back to check for `"0"` so that it passes again.

## Tapping on the cookie
We should now do something a little more interesting with our tests. We are going to test that pressing on the cookie increases our total counter.

Create a new method called `totalIncreasesWhenCookieClicked`. Inside this method add the following code:

```java
onView(withId(R.id.imgCookie))
        .perform(click());
```

This looks similar to the code before, except this time we are performing an action rather than checking something. The first line finds the view with the id `imgCookie` (take a look at your `activity-main.xml` file if you can't remember which view this was). The second line then performs a click action on it. This will call our `OnClickListener` in our `MainActivity.java` file and should update the total label. We now need to write a check for that.

To do this, add in these lines to the new test method:

```java
onView(withId(R.id.lblTotal))
        .check(matches(withText("1")));
```

This is almost exactly the same as the code we wrote for our `totalStartsAtZero` test, but we're instead checking to see that it is now `"1"`.

Our completed test should now look like this:

```java
@Test
public void totalIncreasesWhenCookieClicked() throws Exception {
    onView(withId(R.id.imgCookie))
            .perform(click());

    onView(withId(R.id.lblTotal))
            .check(matches(withText("1")));
}
```

Let's run this new test using the play icon next to the `totalIncreasesWhenCookieClicked` method line. This test should take just long enough for you to see the 1 on the screen, but it's still so fast that you might blink and miss it!

<div class="aside idea">
<p class="aside-title">Aside: Breakpoints</p>

<p>If the test is running too fast and you would like to see what is happening clearly, you can try using a _breakpoint_. A breakpoint is a marker which tells the application to pause at a particular line of code so you can see what it is doing. They are very useful for debugging your apps!</p>

<p>To set a breakpoint, click in the margin to the left of the line of code you would like the test to stop on. The first line of the <code>totalIncreasesWhenCookieClicked</code> method is a good place. Then, use the "debug run" button (the one with the bug and play icon to the right of the "play" button you used before).</p>

<p>Now when the test runs, it should stop on that line and show the "debugger" panel at the bottom of the Android Studio window. You can use the buttons in that panel to "step" between lines or to continue running. Hover over the buttons to see a tooltip for what they do and ask your coach if you are unsure.</p>
</div>

## Getting a high score!
We've now tested all the functionality of our app, so now let's do something just for fun: let's make Espresso click loads of times on the cookie and get a high score!

Create a new method called `achieveHighScore`. Copy the code for the click test you just wrote and wrap the code to click on the cookie image into a for-loop from 0 to 100. You then need to check that the total counter has reached `"100"` after the for-loop has completed. Ask your coach, if you're not sure how to do this, or take a peek at the code below:

```java
@Test
public void achieveHighScore() throws Exception {
    for (int i = 0; i < 100; i++) {
        onView(withId(R.id.imgCookie))
                .perform(click());
    }

    onView(withId(R.id.lblTotal))
            .check(matches(withText("100")));
}
```

If you run this test it should take long enough that you can see what's going on.

As well as running the tests one by one, you can run all your apps tests by pressing on the "double play" icon next to the `public class CookieClickerTest` line. This will run all the tests in this file one by one and let you know which ones pass and fail.

![All tests passing](assets/espresso/all_tests_passing.png)

## Further information
You have now tested your cookie clicker app!

You can read more about Android testing using the links below:

* [Espresso documentation](https://google.github.io/android-testing-support-library/docs/espresso/index.html).
* [Android testing documentation](https://developer.android.com/studio/test/index.html).
* [Using the Espresso test recorder](https://developer.android.com/studio/test/espresso-test-recorder.html).

## Possible extension
You can try extending your cookie clicker and tests by adding an [`EditText`](https://developer.android.com/reference/android/widget/EditText.html) to enter your name, and a button to submit your score. Make sure you write some tests for it too!
