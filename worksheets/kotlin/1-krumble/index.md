---
layout: page
title: Introduction to Kotlin by building a cookie themed tinder
---

The aim of this tutorial is to build a dating like app for cookies! We'll have a list of cookies to either like or dislike!

![Imgur](https://i.imgur.com/3u9ATGZ.png)

Before starting, please ensure you have Android Studio installed and setup correctly.

Also, feel free to pick a different topic than cookies if you prefer. You could pick animals, fruit, or even different little green robots.


*****

## 1 Starting a new Android Studio Project

Firstly we want to create a new app!

![Imgur](https://i.imgur.com/7a8hL4R.png)

On the first screen select a good **name** for your app. This is what people will see when they install your app. I went for crumble because it's similar to bumble but cookie themed.

Next we have a field called **namespace** - this is how Google sandboxes your app. You want to ensure this is unique. *Talk to your coach about what sandboxing means if you're not sure.*

Finally on this screen we need to ensure the most important checkbox is ticked for this workshop! **Enable Kotlin support!**

On the proceeding screens, you want to set a Min SDK - this is the minimum version of Android we want to support. You can click on the version number to get more information and see exactly how many people in the world who could install your app!

*Speak to your coach about what version they have to use at work and the fun they have involved with that!*

Next, we want to create an Empty Activity. I'd keep the default names of `MainActivity` and `activity_main`.

Finally you can click finish! This might take some time to actually create everything needed for your shiny new app ✨

*Take some time to look at the different buttons with your coach - where are the different files located in the project? How do you run your app in an emulator or on your device?*

## 2 Layout

If you feel confident with layouts already, or would prefer to focus on purely kotlin this time. Copy paste the code in this file <https://gist.github.com/daniellevass/aa6d4042b950aaf6c0f2345530e4baa4> into your layout. This will give you all the layout elements we'll use later!

Next, we want to open our layout file. On the left find the res folder and open layout. You should be able to double click on the activity_main.xml and open it.

Layouts open in 'design' mode. This gives you some tools to make layouts with a graphical interface, but it's more common to write layouts by hand using the text editor. If you're familiar with Dreamweaver, it's a similar “What you see is what you get” (WYSIWYG) vs code situation.

We're going to be dealing with the XML directly in this tutorial, so find the 'text' tab in the bottom left corner of the design window.

Now you should see some code that looks familiar-ish! Android layouts using XML, which is very very similar to HTML. You should see already we have a `<RelativeLayout>` and a `<TextView>` tag, with some attributes already there. The thing that looks weird is that all the attributes currently are prefixed with the word android or app.

At the moment Android Studio creates a constraint layout by default. These are bit more complicated to start with. So let's delete everything that's there and put this instead:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
</RelativeLayout>
```

One of the most important features of our cookie clicker will be our cookie - we can create an `<ImageView>`, you will need to provide a height and a width. We also need to provide it an id so we can connect to it later.

```xml
<ImageView
    android:id="@+id/imgCookie"
    android:layout_width="200dp"
    android:layout_height="200dp"/>
```
> id’s need to start with @+id/ - the plus symbol means it assigns the variable name to the current ImageView

In Android we don't use pixels, but instead use `dp` which is a Density-independent Pixel. 1 point might be 1 pixel on a really low resolution device, but might be 4 pixels, or even 8 pixels on a newer device. Take a look at this handy guide Android wrote for more information <https://developer.android.com/guide/practices/screens_support.html>, you can also check out this stack overflow post <https://stackoverflow.com/a/2025541>


Because we have a RelativeLayout parent this means we can do some special things to position our cookie on our screen. We can provide an attribute like android:layout_centerHorizontal="true".

Now that we have our cookie image in position, we want to allow people to see it's name and maybe it's story. Let's create two `<TextView>`'s for this. Make sure you position them, and give them an id.

Finally, we can add two buttons. These are `<Button>`'s. Again remember to position them and give them an id. How about we have a look at styling these red and green to make them easier for people to click?

We can change the background colour by changing the property `android:background="#A0D468"` and we can provide it a hex value. If you want some inspiration for hex colours check out https://material.io/guidelines/style/color.html

![Imgur](https://i.imgur.com/mvEHFov.png)
> my final layout code 😎

*Ask your coach what other special things RelativeLayout can do? Do you know any other alternative parent layouts? Take a look at https://developer.android.com/guide/topics/ui/layout/relative.html for more information.*

*****

## 3 Displaying a cookie

Next, we're going to look at the other file that was created `MainActivity.kt`. Find the function `onCreate` - talk to your coach about when this will get called. You can also take a look at the other android lifecycle methods here <https://developer.android.com/training/basics/activity-lifecycle/index.html>.

Inside our onCreate, we want to connect to our interface elements. Below is what you'll need to type to connect to our ImageView imgCookie. Have a go at writing the connections for our TextViews for lblName and lblStory.

```
var imgCookie:ImageView = findViewById(R.id.imgCookie)
```

> val and var
> You'll notice we created a var for our imgCookie. Var is short for variable, which is something that can change. If our thing is never going to change we can make it a val which is short for value.

Next we can set some values up for our cookie. This is called hardcoding, where we're writing up values into our code. We're going to make this better soon!

 For the image, you can either google for a cookie image that's free to use, or use ours that we found earlier = http://imgur.com/a/9BXV4 . You need to save it inside your project folder using Windows Explorer or Mac OSX Finder and navigate to the following -> app -> src -> main -> res . You need to create a folder called drawable-xhdpi and place your cookie image in here! *Speak to your coach about the why there are so many different folders*

![Imgur](https://i.imgur.com/OMHYp9V.png)

Make sure you run this on either an emulator or your own device to see it working!

*****

## 4 Cookie Class

So we've now determined that our cookie has a set of properties. We can create a class to hold these values for us.

```
data class Cookie(val name: String, val image: Int, val story: String)
```

> Do you notice how we're using val here now. This is because once we create the properties on our cookie object, we don't want to let people change them!

Next, we can create our first cookie object:

```
 val cookie = Cookie("Mr Peanut", R.drawable.peanut_cookie,
                "Loves taking long walks on the beach.")
```

We now need to make sure we're using the values from our cookie:

![Imgur](https://i.imgur.com/LM0Xwyv.png)

We can look at refactoring this a bit. We can create a function to show a Cookie, where we can pass a cookie to show as a parameter. This will make it a lot easier to show a different cookie when we make more!

![Imgur](https://i.imgur.com/oTmEthx.png)

However, we have a problem! We're currently creating those outlets everytime. There's a better way! let's set them up as variables we can use anywhere in the class. We also need to set them up as `lateinit`. This is because kotlin doesn't like null, or something that doesn't exist yet. We're telling our Activity these things do exist, but later! They'll exist by the time we want to use them.

![Imgur](https://i.imgur.com/GXi16fg.png)

*****

## 5 Liking and Disliking

Next, we want to allow people either express their love or hatred for our cookie!

Let's set up some outlets for our buttons. We can create a toast message, the little messages that pop up from the bottom of your screen. Run it on your device or emulator to see it working.

![Imgur](https://i.imgur.com/27dpVts.png)

How about, let's extend our cookie class to contain what the cookie might say for either of the options.

![Imgur](https://i.imgur.com/qoVjN9W.png)

Let's test this out on our emulator or real device to make sure our project still works.

*****

## 6 More Cookies!

Firstly we're going to create a new function to generate and return us a list of cookies. We can then use those generated cookies in our Activity. We can also delete our hard coded cookie, and just use the first cookie in our list. Lists starts at 0 in Kotlin (as in Java too). Much like how we number building floors in the UK; where ground is 0, floor 1 goes next etc.

![Imgur](https://i.imgur.com/RqF5uEv.png)

Next we can set up a val to point to the current index, which starts at 0. We can then increment it everytime we like or dislike our cookie, and show our new cookie.

![Imgur](https://i.imgur.com/EfuWhlu.png)

However, what happens when we get to the last cookie and you like or dislike it? Run it on an emulator or your device to see what happens.

It sadly crashes :( This definitely isn't what we wanted! We want to start our cookies back at the beginning.

![Imgur](https://i.imgur.com/KmZuIPq.png)

*****

## 7 Finishing

You managed to get to the end of the tutorial! congratulations 🏆 !!!

We think there's tonnes of things you could do to make your cookie tinder app truly unique!

If your stuck for more ideas to add to your game:
* ensure you have a diverse set of cookies to chose between (10+ would be great)
* make the UI more friendly - how about a state selector for the button background
* investigate how to animate the picture to tilt out
* look into sorting and filtering your array of cookies