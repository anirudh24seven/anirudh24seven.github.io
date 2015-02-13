---
layout: post
title:  "Robotium in Android Studio"
date:   2014-02-13 12:53:33
categories: devlog
comments: True
---

I wanted to run UI tests within my Android app and I decided to go ahead with Robotium. I went through the project pages of [Robotium](https://code.google.com/p/robotium/) and [Robotium recorder](http://robotium.com/) and noticed that they seemed a little outdated. Most importantly, I couldn't find information easily on how to run Robotium with Android Studio. Robotium Recorder, on the other hand, provided a plugin for Android Studio and you can find more info about it here: [robotium.com/pages/user-guide-android-studio](http://robotium.com/pages/user-guide-android-studio).


##Problem:
Install and run Robotium in Android Studio.

##Observations:

1. [Gradle, please](http://gradleplease.appspot.com/) provided a hit when I searched for Robotium. Robotium is indeed available as a Gradle dependency.

        dependencies {
          compile 'com.jayway.android.robotium:robotium-solo:5.2.1'
        }


2. I downloaded and installed Robotium Recorder out of curiosity. It worked perfectly. It recorded my actions, allowed me to run my recorded test and also save it. The generated file was a .class though, instead of .java. This meant that I couldn't edit the test once it was generated. I understood that it would be a non-free feature and moved on.

3. A Google search for integrating Robotium with Android Studio led me to this Stack Overflow question: [http://stackoverflow.com/questions/23275602/robotium-with-android-studio](http://stackoverflow.com/questions/23275602/robotium-with-android-studio) But the answer wasn't very helpful. So I decided to figure things out on my own and find a solution.

##Experiments

{% include twitter_plug.html %}
