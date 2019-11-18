---
id: cookie-clicker-kotlin
title: Cookie Clicker (Kotlin)
---

# Introduction to Android Development

## 1. Intro

The aim of this worksheet is to create a [cookie clicker game](http://orteil.dashnet.org/cookieclicker/), with a cookie image that can be tapped to increase the score.

To follow this tutorial, you will need to [get set up for Android development]({{ site.baseurl }}/setup). Please note, this involves downloading a large file, so our advice is to run through and install everything before arriving at the workshop. If you have problems, just get as far as you can and a coach can help you finish it off.

Feel free to chose a different topic other than cookies, we really like the popular pokémon Goomy Clicker - <http://joezeng.github.io/goomyclicker> what things do you like?

![The completed application](assets/cookie-clicker-kotlin/1_completed.png)

## 2. Create New Project

Firstly, we want to create an `Empty Activity`

![](assets/cookie-clicker-kotlin/picture1.png)

Next, we want to create our application

![](assets/cookie-clicker-kotlin/picture2.png)

> Set the name of your app, this is what people will see when they install your app. The company name, and the resulting package name, is how Google keeps track of apps - it needs to be unique, so try using something with your name?

Next, we set the SDK level to `21` - If you tap on `help me choose`, it'll give you a chart of how many people are currently running each version. If we want to enable more people we want to target a lower SDK level, however nicer things get added to later SDKs. If you tap a version it'll tell you what things were introduced. Speak to your coach about what minimum sdk level they've had to use in their career.

Finally, we want to make sure our project language is set to `Kotlin`!

click FINISH (this might take some time to create your project and land you on to your code)

Take some time to look at the different buttons with your coach - where are the different files located in the project? How can you run your app in an emulator or on a device?

![](assets/cookie-clicker-kotlin/picture3.png)

## 3. Layouts

Next, we want to open our layout file. On the left find the res folder and open layout. You should be able to double click on the activity_main.xml and open it.

Layouts open in 'design' mode. This gives you some tools to make layouts with a graphical interface, but it's more common to write layouts by hand using the text editor. If you're familiar with Dreamweaver, it's a similar “What you see is what you get” (WYSIWYG) vs code situation.

We're going to be dealing with the XML directly in this tutorial, so find the 'text' tab in the bottom left corner of the design window.

Now you should see some code that looks familiar-ish! Android layouts using XML, which is very very similar to HTML. You should see already we have a `<RelativeLayout>` and a `<TextView>` tag, with some attributes already there. The thing that looks weird is that all the attributes currently are prefixed with the word `android`.

At the moment Android Studio creates a constraint layout by default. These are bit more complicated to start with. So let's delete everything that's there and put this instead:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
</RelativeLayout>
```

One of the most important features of our cookie clicker will be our cookie - we can create an `<ImageView>`, you will need to provide a `height` and a `width`. We also need to provide it an id so we can connect to it later.

```xml
<ImageView
    android:id="@+id/imgCookie"
    android:layout_width="256dp"
    android:layout_height="256dp"/>
```

> id’s need to start with @+id/ - the plus symbol means it assigns the variable name to the current ImageView

In Android we don't use pixels, but instead use `dp` which is a device point. 1 point might be 1 pixel on a really low resolution device, but might be 4 pixels, or even 8 pixels on a newer device. Take a look at this handy guide Android wrote for more information <https://developer.android.com/guide/practices/screens_support.html> .

Next, we want to save the following cookie image into our project. You can either google for a cookie image that's free to use, or use ours that we found earlier = <http://imgur.com/a/9BXV4> . You need to save it inside your project folder using Windows Explorer or Mac OSX Finder and navigate to the following -> app -> src -> main -> res . You need to create a folder called `drawable-xhdpi` and place your cookie image in here!

Because android has different density devices, we usually need to provide different resolution images for all those different devices. If we only provide it in one folder, Android will scale the image for other devices, but this might cause make the image look bad!

![Where to place the cookie image file](assets/cookie-clicker-kotlin/4_cookie_finder.png)

If we want to then use that image in our Android app we can use an attribute `android:src="@drawable/cookie"` - autocomplete will be your friend here!

Because we have a RelativeLayout parent this means we can do some special things to position our cookie on our screen. We can provide an attribute like `android:layout_centerInParent="true"`.

Next, we want to look at having a TextView for to keep track of how many cookies we've clicked. Again you need to provide it a height, width, and id. But we can also provide it some special label things, such as `text`, `textColor`, or `textSize`

Another neat feature of using a RelativeLayout is how we can position things **in relation** to other things. So we can say that this TextView should `appearAbove` the image's id. In order for this to work, the TextView needs to know where the ImageView is, so the code for the TextView needs to go below the ImageView.

![The cookie clicker layout file in Android Studio](assets/cookie-clicker-kotlin/5_android_studio_layout.png)

> this is how our layout code finally looked :smile:

Ask your coach what other special things RelativeLayout can do? Do you know any other alternative parent layouts?  Take a look at <https://developer.android.com/guide/topics/ui/layout/relative.html> for more information.

## 4. Clicking

Next, we want to make it so our cookie actually does something when it's been clicked on!

We want to open our MainActivity.java file and take a look at what's there already. What do you think the `onCreate` method might do? Speak to your coach about what other methods get called in the activity lifecycle. For more information look at <https://developer.android.com/training/basics/activity-lifecycle/index.html> .

Inside the `onCreate` method, below where it sets the layout to the xml file we just finished designing. We want to create a variable called imgCookie and findViewById to hook them up. This is similar to how we would use jQuery in JavaScript to hook up with a HTML element

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)

    val imgCookie: ImageView = findViewById(R.id.imgCookie)
}
```

After, we can set an `onClickListener`, which is again similar to the JavaScript element.click() method. The trick with Android Studio is to let it write as much code as possible, it has an extremely powerful auto completer! When you start typing onClickListener, you should see a suggestion with curly brackets on it. If you press tab at this point, it'll auto complete the entire code that you need!

![](assets/cookie-clicker-kotlin/picture4.png)

Inside our method we're going to put a Toast. These are those little messages at the bottom of the phone that show for a short period of time. They're really good!

![](assets/cookie-clicker-kotlin/picture5.png)

Run your app now, see what happens when you tap on the cookie picture!

## 5. Game Logic

Next, we want to make it so that when the image is clicked we increment a score. We need to create a private variable called currentScore and set initially set it to 0.

When we click on the image, we need to increment the score by 1. For now, we can use our toast to see how much our current score is:

```kotlin
private var currentScore = 0

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)

    val imgCookie: ImageView = findViewById(R.id.imgCookie)

    imgCookie.setOnClickListener {
        currentScore ++
        Toast.makeText(this, "score = $currentScore", Toast.LENGTH_SHORT).show()
    }
}
```

You’ll notice we created a `var` for our score. Var is short for variable, which is something that we can change over time. If our thing is never going to change we can make it a `val` which is short for value. Our `imgCookie` isn't ever going to change so we that's why we use `val`.

Toast messages are super useful for whilst we’re building the app, but all the people you're going to get playing probably don’t want that! Let’s go about hooking it up to our TextView.

Firstly, we need to make a variable called lblTotal and set it to our TextView just like how we set up our ImageView.

Next, inside our imgCookie onClickListener, we can do `lblTotal.text` to display some next. However we can’t do this directly; our currentScore is an `int` (number), and the lblTotal can only display a `String` (text). So we need to use a template to output this, if you use a $ character inside quotes, you can print out our integer!

![](assets/cookie-clicker-kotlin/picture6.png)

## 6. Finishing

Run your app a final time. Make sure that when you tap the button, your score counter is increased by one each time.

Congratulations - you've built an app!

If you stuck with the cookie image, maybe now would be a good time to change your image for something you think is better to click? Maybe there's an emoji that you think would work really good (🌮 clicker anyone?)

Once you've finished polishing your app make sure you take a screen grab (or a video!) and tweet it to us at @codebar!


## 6. Extra Credit

Now is the time to get creative! What other things would make your game yours.

Idea 1: Change the picture when you get to specific numbers using an if statement, e.g. after 10 clicks your cookie picture is changed to a half eaten cookie. You could make this logarithmic so that after 10, 100, 1000 clicks something different happens!

Idea 2: Buttons people can spend clicks on to upgrade your cookie e.g. maybe your cookie picture can change to have golden chocolate chips with 100 clicks.

Idea 3: Time based challenge, allow people 10 seconds to get as many clicks as possible before the button is disabled and you record their high score.

Idea 4: Things you can spend points on to automate getting cookies.
