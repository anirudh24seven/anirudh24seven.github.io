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

3. A Google search for integrating Robotium with Android Studio led me to this Stack Overflow question: [http://stackoverflow.com/questions/23275602/robotium-with-android-studio](http://stackoverflow.com/questions/23275602/robotium-with-android-studio). But the answer wasn't very helpful. So I decided to figure things out on my own and find a solution.

##Experiments

1. I peered through the contents of the Robotium website more carefully and found that the project owners had provided PDF files for the Tutorials, instead of displaying them directly. But I was not still clear about creating tests in Android Studio.

2. Now that I wanted to know how to create tests in Android Studio, I searched for it specifically, I came upon this answer: [http://stackoverflow.com/a/20348909/568169](http://stackoverflow.com/a/20348909/568169)

3. I followed the steps in the above answer and created a test file. I then copy-pasted my recorded test case from Robotium Recorder and ran it. It ran successfully.

##Summary:
1. In your app module, create an **androidTest/java** package under the **src**  folder.
2. Open that module's **build.gradle** and add the below lines:

        android {
          
          sourceSets {
            
            androidTest {
              java.srcDirs = ['androidTest/java']
            }
            
          }
        }

3. Sync the Project. You should now see a folder named "java" in a green color.
4. Create your Robotium test file. For example, in a test file called ExampleTest.java, add the below code:

        import android.test.ActivityInstrumentationTestCase2;
        import com.robotium.solo.Solo;

        @SuppressWarnings("rawtypes")
        public class ExampleTest extends ActivityInstrumentationTestCase2 {
          private Solo solo;
          
          private static final String LAUNCHER_ACTIVITY_FULL_CLASSNAME = "com.example.ExampleActivty";
          
          private static Class<?> launcherActivityClass;
          static{
            try {
              launcherActivityClass = Class.forName(LAUNCHER_ACTIVITY_FULL_CLASSNAME);
              } catch (ClassNotFoundException e) {
                throw new RuntimeException(e);
              }
            }
            
            @SuppressWarnings("unchecked")
            public ExampleTestTest() throws ClassNotFoundException {
              super(launcherActivityClass);
            }
            
            public void setUp() throws Exception {
              super.setUp();
              solo = new Solo(getInstrumentation());
              getActivity();
            }
            
            @Override
            public void tearDown() throws Exception {
              solo.finishOpenedActivities();
              super.tearDown();
            }
            
            public void testRun() {
              //Wait for activity: 'com.example.ExampleActivty'
              solo.waitForActivity("ExampleActivty", 2000);
              //Clear the EditText editText1
              solo.clearEditText((android.widget.EditText) solo.getView("editText1"));
              solo.enterText((android.widget.EditText) solo.getView("editText1"), "This is an example text");
            }
          }
          
{% include twitter_plug.html %}
