Android app skeleton [![Build Status](https://travis-ci.org/fs/android-base.png)](https://travis-ci.org/fs/android-base)
================================================
##Prerequisites
* JDK 7 and 8 (you need both)
* Android SDK tools 22.6
* Android build tools 19.0.3
* `JAVA7_HOME` pointing to your jdk7
* `JAVA8_HOME` pointing to your jdk8
* `ANDROID_HOME` pointing to your android sdk

##What's included:
* *Crittercism* configuration
* *Google Analytics* configuration with [`Fragment` tracking helper method][1]
* Logger configuration [supporting *Crittercism* `Exception` logging][2]
* [Java 8 lambdas support and configuratiuon][3]
* [Robolectric support and configuration][4]
* `Application` subclass with an application-wide `ObjectGraph`
* `Activity` subclass with configured UI-wide `ObjectGraph` and a root `Fragment`
* Default `Menu` with *Settings* `MenuItem`
* `Preferences` interface for the `SharedPreferences` boilerplate reduction
* `PreferenceFragment` with default Preferences xml added to a `MainFragment`'s *Settings* `MenuItem`
* *Android Lint* configuration
* *TestFairy* upload script
* *Travis CI* build script:
    * Downloading an *Android SDK*
    * Building
    * Running *Android Lint*
    * Running *Robolectric* tests
    * Uploading a successful build to the *TestFairy*
* Release build signing and naming configuration

##[Bundled dependencies][5]

##Setup
 1. Clone application as new project with original remote named "android-base"

    	git clone git://github.com/fs/android-base.git --origin android-base [MY-NEW-PROJECT]

 2. Create your new repository on the GitHub and push master into it. Make sure master branch is tracking origin repo.

        cd [MY-NEW-PROJECT]
    	git remote add origin git@github.com:[MY-GITHUB-ACCOUNT]/[MY-NEW-PROJECT].git
    	git push -u origin master

 3. Import the project into your IDE (only [Android Studio][6] and [IntelliJ IDEA 13][7] are supported at the moment).
Just select the root `build.gradle` and your IDE will do the rest.
It will ask you to change the language level - do it, we're using Java 8 now

##Configuration
There're things that need to be configured (such as app tokens and so on)

1. At the [analytics.xml][8] change your Google Analytics `ga_trackingId` appropriately, and uncomment [these lines in `MainActivity.java`][9]
2. At the [tokens.xml][10] change `crittercism_app_id`, and uncomment [this line in `App.java`][11]
3. At the [AndroidManifest.xml][12] change the `package` field to the desired one
4. Last but not least, don't forget to change an [app icon][13] and an [app name][14]

###Uploading to the TestFairy
You need to add your API key and the tester groups to the [upload script][15]
###Making a release build
You need to uncomment [these lines in `build.gradle`][16] and also add your keystore credentials to the [`gradle.properties`][17]
##Notes on ProGuarding
Currently [Dagger][18] doesn't work with ProGuard at all, but there's a project that solves the problem, and we need to somehow make it work on gradle: https://github.com/idamobile/dagger-proguard-helper


  [1]: app/src/main/java/com/flatsoft/base/App.java?source=c#L41-L45
  [2]: app/src/main/java/com/flatsoft/base/utils/TimberCrashReportingTree.java
  [3]: app/build.gradle?source=c#L59-L64
  [4]: app/build.gradle?source=c#L101-L105
  [5]: DEPENDENCIES.md
  [6]: http://developer.android.com/sdk/installing/studio.html
  [7]: http://www.jetbrains.com/idea/
  [8]: app/src/main/res/values/analytics.xml
  [9]: app/src/main/java/com/flatsoft/base/MainActivity.java#L55-L63
  [10]: app/src/main/res/values/tokens.xml
  [11]: app/src/main/java/com/flatsoft/base/App.java#L30
  [12]: app/src/main/AndroidManifest.xml
  [13]: app/src/main/res/drawable-xhdpi/ic_launcher.png
  [14]: app/src/main/res/values/strings.xml#L3
  [15]: testfairy-upload.sh#L4-L5
  [16]: app/build.gradle#L33-L50
  [17]: app/gradle.properties
  [18]: https://github.com/square/dagger