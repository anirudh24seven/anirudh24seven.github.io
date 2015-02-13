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

1. [Gradle, please](http://gradleplease.appspot.com/) provided a hit when I searched for Robotium. The result was:

dependencies {
  compile 'com.jayway.android.robotium:robotium-solo:5.2.1'
}

Ah. So, Robotium is available as a Gradle dependency.

2. I downloaded and installed Robotium Recorder out of curiosity. It worked perfectly. It recorded my actions, allowed me to run my recorded test and also save it. The generated file was a .class though, instead of .java. This meant that I couldn't edit the test once it was generated. I understood that it would be a non-free feature and moved on.

3. A Google search for integrating Robotium with Android Studio led me to this Stack Overflow question: [http://stackoverflow.com/questions/23275602/robotium-with-android-studio](http://stackoverflow.com/questions/23275602/robotium-with-android-studio)

I have copy-pasted the answer below: [Answer Link](http://stackoverflow.com/a/24156892/568169)

1. Add the following line to the dependencies section of the inner build.gradle file (this file is located at the same level as src folder), change version name if required:

2. androidTestCompile 'com.jayway.android.robotium:robotium-solo:5.2.1'
If for some reason you don't want to let gradle download dependencies for you then you can add them manually: Place robotium.jar into the libs folder. Right click it and select Add as library...

3. In the src folder create another folder androidTest

4. Inside it create java folder
(Optional step, see below) Inside it create a package for the test source with the same name as app’s package name (or add ".tests" to its end.)
5. Place cursor (in the Editor window) at the class name inside one of the files that you want to test (e.g. MainActivity) and press Alt+Enter.
6. Select Create Test. Select the proper superclass for Robotium:    
         
       android.test.ActivityInstrumentationTestCase2
7. Android studio will create a test file and a package (if it wasn’t created in step 6)
8. How to run the test:

UI: as usual using Android Studio Run menu
console: in the terminal enter the following command:

./gradlew connectedAndroidTest
The HTML-reports will be generated at "YourApp/YourApp/build/outputs/reports/androidTests/ connected/index.html"


**Guide:**

1. Add the following line to the **dependencies** section of the inner build.gradle file (this file is located at the same level as **src** folder), change version name if required:

       androidTestCompile 'com.jayway.android.robotium:robotium-solo:5.2.1'

If for some reason you don't want to let gradle download dependencies for you then
you can add them manually: Place robotium.jar into the **libs** folder. Right click it and select **Add as library...**

2. In the **src** folder create another folder **androidTest**
3. Inside it create **java** folder
4. (Optional step, see below) Inside it create a package for the test source with the same name as app’s package name (or add ".tests" to its end.)
5. Place cursor (in the Editor window) at the class name inside one of the files that you want to test (e.g. MainActivity) and press Alt+Enter.
6. Select **Create Test**. Select the proper superclass for Robotium:

       android.test.ActivityInstrumentationTestCase2
7. Android studio will create a test file and a package (if it wasn’t created in step 6)
8.  How to run the test:
  - UI: as usual using Android Studio **Run** menu
  - console: in the terminal enter the following command: 

          ./gradlew connectedAndroidTest

     The HTML-reports will be generated at "YourApp/YourApp/build/outputs/reports/androidTests/
connected/index.html"

{% include twitter_plug.html %}
