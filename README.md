# Phonograph
[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://github.com/kabouzeid/Phonograph/blob/master/LICENSE.txt)

**A material designed local music player for Android.**

![Screenshots](./art/art.jpg?raw=true)

[<img src="https://play.google.com/intl/en_us/badges/images/generic/en-play-badge.png"
     alt="Get it on Google Play"
     height="80">](https://play.google.com/store/apps/details?id=com.kabouzeid.gramophone)
[<img src="https://fdroid.gitlab.io/artwork/badge/get-it-on.png"
     alt="Get it on F-Droid"
     height="80">](https://f-droid.org/packages/com.kabouzeid.gramophone/)

# Description
The forked project disable the pro version check for Phonograph.

# License
Under the GPLv3 License, users are allowed to modify and redistribute this software.  

# Download
You can compile this project using Android Studio, IntelliJ IDEA, any IDE support gradle build system or even gradle wrapper script.  
Alternatively, you can download a compiled, signed APKs from [here](https://github.com/rikkaneko/Phonograph/releases/tag/v1.3.5-pro).

# Pro version
You need to edit the `App.java` in `app/src/main/java/com/kabouzeid/gramophone`  
**1. Disable the purchase check**  
Comment the content of `isProVersion()` and set to always return true
```java
public static boolean isProVersion() {
    //return BuildConfig.DEBUG || app.billingProcessor.isPurchased(PRO_VERSION_PRODUCT_ID);
    return true;
}
```
**2. Disable the automatic refresh of purchases status from Google Play**  
Comment the content of three methods in `LoadOwnedPurchasesFromGoogleAsyncTask` class:
`onPreExecute():`
```java
@Override
protected void onPreExecute() {
     //sPro = App.isProVersion();
}
```
`doInBackground():`  
**Be awarded, `Void` is not `void`**
```java
@Override
protected Void doInBackground(Void... params) {
     //llingProcessor billingProcessor = billingProcessorWeakReference.get();
     // (billingProcessor != null) {
          // The Google billing library has it's own cache for about 8 - 12 hours.
          // The following only updates the billing processors cache if the Google billing library returns a value.
          // Therefore, even if the user is longer than 8 - 12 hours without internet the purchase is cached.
          //llingProcessor.loadOwnedPurchasesFromGoogle();
     //}
     return null;
}
```
`onPostExecute():`
```java
@Override
protected void onPostExecute(Void aVoid) {
     //if (wasPro != App.isProVersion()) {
          //App.notifyProVersionChanged();
     //}
}
```
# If you like this app, please consider support the original authors :)
