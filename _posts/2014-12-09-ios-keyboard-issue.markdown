---
layout: post
title:  "iOS keyboard issue"
date:   2014-12-09 21:00:00
categories: devlog
comments: True
---
I have been looking at [this issue in HelpStack iOS](https://github.com/happyfoxinc/helpstack/issues/20). 

There seem to be 4 keyboard-related observers:

* UIKeyboardWillShowNotification
* UIKeyboardDidShowNotification
* UIKeyboardWillHideNotification
* UIKeyboardDidHideNotification

However, I could find very little first-party documentation about these observers. Only found the below two:

* [Text Programming Guide for iOS](https://developer.apple.com/library/ios/documentation/StringsTextFonts/Conceptual/TextAndWebiPhoneOS/KeyboardManagement/KeyboardManagement.html)
* [UIWindow Notifications](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/c/data/UIKeyboardWillShowNotification)

Sadly, they don't seem to be very explanatory.

This [StackOverflow question](http://stackoverflow.com/questions/1126726/how-to-make-a-uitextfield-move-up-when-keyboard-is-present) seems to have a lot of responses. But most of them don't seem to be the complete fix. (Go ahead. Upvote [the question](http://stackoverflow.com/questions/1126726/how-to-make-a-uitextfield-move-up-when-keyboard-is-present).) Looks like Apple hasn't provided enough documentation around this.

So far, I have made whatever changes I could and created a pull request [here](https://github.com/happyfoxinc/helpstack/pull/33). Planning to fix the iPad issue first. The source file for the iPad Ticket Detail ViewController is at [/Classes/UI/HSTicketDetailViewControlleriPad.m](https://github.com/happyfoxinc/helpstack/blob/master/Classes/UI/HSTicketDetailViewControlleriPad.m). I am sure that spending more time with this file will help me understand.

Hope to fix all the problems soon.
