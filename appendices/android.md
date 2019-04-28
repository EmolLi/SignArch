# Android Framework

As an Android client application, Signal Android builds on the following key elements from the Android Framework.

## Activities

An **[Activity](https://developer.android.com/reference/android/app/Activity.html)** represents a single screen in the android app with which the user can perform a single, focused task such as dialing the phone, taking a photo, sending an email, or viewing a map. Activities are usually presented to the user as full-screen windows.

An application usually consists of multiple activities that are loosely bound to each other. Typically, one activity in an application is specified as the “main” activity, which is presented to the user when the app is launched. Each activity can then indicate to the upper layer to transition to a new activity in order to perform different actions.

Each time a new activity starts, the previous activity is paused, and the system preserves the activity in a stack (the “back stack”). The new activity is pushed onto the back stack and takes user focus. When the user is done with the current activity or presses the Back button, that current activity is popped from the stack (and stopped) and the previous activity resumes.

## Intents

**[Intent](https://developer.android.com/reference/android/content/Intent.html)** is a class that encapsulates a message. It is used for a wide variety of purposes, such as indicating to the Android Framework the expected control flow of the application, sending or requesting information between components, or starting services.

For example, when an activity needs to indicate to Android to switch to another activity, it can call one of its own inherited methods, such as `startActivity(Intent)`, which will be captured by the Android Framework, and the latter will handle the transition between activities.

## Broadcast Receivers

Android applications can send or receive broadcast messages (in the form of intents) from the Android operating system and other applications. These broadcasts are sent when an event of interest occurs, for example when the system boots up or the device starts charging. Applications can also send custom messages, for example, to notify other applications that new data has been downloaded.

To receive these messages, applications register to specific broadcasts using **[BroadcastReceivers](https://developer.android.com/reference/android/content/BroadcastReceiver)**. When a broadcast is sent, the system automatically routes broadcasts to apps that have subscribed to receive that particular type of broadcast.