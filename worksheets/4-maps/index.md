---
title: Codebar Android Workshop Google Maps Lesson
layout: page
---


# Google Maps Lesson
This tutorial won’t assume too much about your familiarity with Android or Android Studio.
You will need Android Studio installed, and you’ll need a Google account (a gmail account, or the google account you use for your phone will be fine).

This tutorial takes you through the steps on https://developers.google.com/maps/documentation/android-api/start, explaining and illustrating the process of getting an application up and running that displays a Google Maps view, ready to extend to do whatever map-related things you may want to do!


## Create a new project

Android Studio provides a handy template to quick-start you making an app that focuses on Google Maps.  We are going to take advantage of this, get it running, and then see what we can do with it.

1. Create a new project.  You can choose whatever name and domain you like, but I’d suggest to target API 19 as the minimum SDK level (it’s selected by default at the time of writing) - selecting lower levels may throw up little issues in the tutorial, and you don’t want to have to worry about that right now! Selecting a higher level can avoid one particular issue the tutorial deals with, but it’s helpful to know about that anyway!
2. Select the Google Maps Activity when presented with the choice.  You can recreate everything that this template provides you with yourself, but this saves us some time.  There’s nothing special about this Activity itself, it just comes set up with a Map Fragment, ready to get started with.
https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487880192702_Screen+Shot+2017-02-23+at+19.54.45.png

3. Choose a name for your Activity and its layout; it doesn’t matter what names you choose, but this tutorial will call the Activity “MapsActivity” and the layout “activity_maps”.


## What do we have here?

You’ll be presented with a screen like this, which contains some instructions:

https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487880369756_Screen+Shot+2017-02-23+at+20.05.12.png


It looks like we’ll need a “Google Maps API key”!  This is our google_maps_api.xml; it’s where hold the key we’ll use to access Google Maps’ API.  On the left you can also see the activity_maps.xml layout and MapsActivity class; we’ll be coming back to those later.


## Getting an API Key

Aside:
An API is what’s used by apps and websites (or the servers behind them) to talk to each other.  Sometimes these APIs are free and open - anyone (anyapp?) can talk to them and get information from them.  Google’s Maps API, which allows us to ask it for map data, is free, but it requires a key connected to a Google account.  Essentially, this allows them to stop you from abusing their API, say by spamming it, and allows them to charge businesses for extras. That won’t be a problem for us!

Keys are linked to an app; essentially we’ll register our app’s key with Google Maps and they’ll give us an API key that our app uses when it makes a request.  

1. Copy the link suggested into your web browser; you should see a screen like this (perhaps once you’ve logged into/created your Google account):


https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487881543251_Screen+Shot+2017-02-23+at+20.15.51.png

2. Make sure “Create a project” is selected and continue.
3. Give it a minute to do its thing and be rewarded with this screen:
https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487881768198_Screen+Shot+2017-02-23+at+20.26.52.png

4. Keys to the kingdom!  Click “Create API key” and you’ll be presented with something like this (hopefully with a string of characters instead of a black box though!)
https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487881920458_Screen+Shot+2017-02-23+at+20.29.51.png

5. Copy the key, switch back to Android Studio, and paste it over where it says “YOUR_KEY_HERE” back at the bottom of google_maps_api.xml.
6. You’ve now given your app the key it needs, but we should finish up on the website. Go back to the “API key created” window and click “Restrict Key”.
https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487882213929_Screen+Shot+2017-02-23+at+20.33.19.png


Here we can give our key a name (so that later we can remember that we used this on our maps tutorial app) - you can probably come up with something better than “API key 1”.  We’re going to restrict this to Android apps, though it’s worth noting that you can use a similar process for other platforms too.
The certificate fingerprint and the package name at the end are automagically filled for us because they were part of the initial link we copied, but if you were doing it manually you would be able to get this information from your project. This prevents the key from being used by apps that aren’t listed here, but also allows you to share the same key between multiple apps if you want to.

https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487882669814_Screen+Shot+2017-02-23+at+20.42.32.png


Ok, we’re done with the website now!


## Nice! Web-stuff Done!

Have a drink or something if you feel like; next up we’re going to fix Google’s code! :D


## It Just Works™ (or “how I learnt to stop worrying and love dex method count”)

Connect your phone to your machine, make sure development mode is enabled and that you can push apps over via usb, and try running the app with the green “play” button at the top of the screen:

https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487883650043_Screen+Shot+2017-02-23+at+20.59.27.png


You’ll see this at the bottom, showing that a build is happening:

https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487883705889_Screen+Shot+2017-02-23+at+21.01.19.png


Then (if Google doesn’t fix this at some point) you’ll get a delightfully cryptic message like this:

https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1487883737373_Screen+Shot+2017-02-23+at+20.58.01.png


Well.

What’s happened is that Google’s included all of their support library code and services code, for all sorts of things that we’re not using, and there’s so much of this that it would break a limit on the number of methods allows in a single app!

(This is the bit that may not happen if you’re targeting Android SDK 21 or above, because it handles dex limits differently, but your app will still be bloated with unnecessary code so this is still best practice.)

It’s easy enough to fix this but only including the maps service we need. Go to your app’s build.gradle (there are two - one for the project and one for the module.  Most of the changes you make in an Android app will be in the module build.gradle) and look for the dependencies block that looks like this:

https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1492331383538_Screen+Shot+2017-04-16+at+09.29.11.png


(Don’t worry if your version numbers don’t match the ones if the picture - they get updated pretty often!)
The yellow highlighted line is the important one right now; instead of all of play-services we want play-services-maps; you can find a list of all the other play service components and their current versions on this page: https://developers.google.com/android/guides/setup


# Let’s do this!

Hit the play button at the top again and you should be rewarded with the app launching and pointing at Sydney!

https://d2mxuefqeaa7sj.cloudfront.net/s_ACC90D09233A53E485AF629987F27DF866A7AA6BAE5C1ABA6BC69EB9EA2F3726_1492549387863_Screenshot_20170418-220138.png

# Taking stock and next steps

So, right now you can take this in several directions.  

You can experiment with making changes to what happens when onMapReady() is called in MapsActivity, for instance changing the location from Sydney to your favourite spot (try something like http://www.latlong.net/ to look up latitude and longitude values!)

If you have an idea then try bouncing it off your coach and see what you can make!

Alternatively, Google has some suggestions for next steps, such as changing the map’s styling (https://developers.google.com/maps/documentation/android-api/styling) or finding your current location and points of interest nearby (https://developers.google.com/maps/documentation/android-api/current-place-tutorial).  You can also draw regions and lines onto the map (https://developers.google.com/maps/documentation/android-api/polygon-tutorial) - have a look down the sidebar on that website to see a menu of things to try out!
