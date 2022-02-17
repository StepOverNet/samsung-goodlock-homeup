# Description
- The good people over at <b>Good Lock Labs</b> have created multiple apps that allow for more customization for the <b>One UI</b> users. One of those apps is called <b>Home Up</b>, You have options from Home Screen grid to Task Manager layout type and a bunch of other stuff. I wanted the option of going above limits until the very point before you cause chaos, And so this tutorial will show you how you can do that very thing.
# Heads Up
- <b>I</b> am not responsible for any damages done to your device from doing this tutorial.
# Requirements
- Good Lock APK ( Main App ) - https://galaxystore.samsung.com/detail/com.samsung.android.goodlock
- Home Up APK ( Sub App ) - https://galaxystore.samsung.com/detail/com.samsung.android.app.homestar
- Android Studio ( Developing App ) - https://developer.android.com/studio
- Jadx ( Java Decompiler App ) - https://github.com/skylot/jadx
# Begin
- If you are not familiar with Android Studio you can visit https://developer.android.com/docs to get help on how to start developing on the Android platform. Otherwise create a new project and follow along.
- Now this piece of code will be used in <b>AndroidManifest.xml</b> to declare 2 permissions to access the external values.
```
<uses-permission android:name="android.permission.QUERY_ALL_PACKAGES"/>
<uses-permission android:name="com.samsung.android.app.homestar.permission.HOMESTAR_DATA"/>
```
- This piece of code writes the value to the content provider where the value will be stored for the <b>One UI</b> to use.
```
Bundle bundle = new Bundle();
bundle.putBoolean("enable_grid_pref", true);
bundle.putInt("home_grid_num_cols", 0);
bundle.putInt("home_grid_num_rows", 0);
getContentResolver().call(Uri.parse("content://com.samsung.android.app.homestar.provider/setting"), "pref_key_expandable_home_grid", "pref_key_expandable_home_grid", bundle);
```
- And this one will write the value to the <b>Home Up</b> content provider to show the user the current values.
```
SharedPreferences.Editor editor = getApplicationContext().getSharedPreferences("com.samsung.android.app.homestar_preferences", 0).edit();
editor.putBoolean("home_widget_resize", true);
editor.putInt("home_grid_num_cols", 0);
editor.putInt("home_grid_num_rows", 0);
editor.apply();
getContentResolver().notifyChange(Uri.parse("content://com.samsung.android.app.homestar.provider/setting"), null);
```
- That's it, Now just compile your app and wala. Now if you want to do more searching on your own and see how things work let me explain. Next step is to open up Jadx and import the <b>Home Up</b> apk into it. How I found out what wrote to what was alot of searching, I guess you can also call it a "trial & error" kinda thing. So far ended up finding acouple of things that can be used outside the app. To find what writes to the home screen grid you probably want to search for something along the lines of "setCurrentHomeGrid". At this point you kinda have the sense and knowledge on what to look for.
# Help
- Question : Android Studio keeps showing me errors, How do I fix this?
- <b>Answer</b> : Make sure you have atleast used the Home Up app once, maybe the values are empty since you never used it before.
- Question : I've written the wrong value and now my launcher keeps crashing and or being unresponsive, How do I fix this?
- <b>Answer</b> : You fucked up, Theres nothing I can do about it...Just kidding. <b>Swipe down</b> to bring up the quick settings/notification screen, Once there tap on the <b>Gear</b> icon, Once there scroll down to <b>Apps</b> and look for <b>Good Lock</b> and open it. Now head to the <b>Home Up</b> app and set the value to a working one. If it still does not fix it self then you might have to restart your mobile device. If that doesn't work try installing another launcher and then go back to yours and see what happens. By the way I did alot of trial and error on my personal device and I was able to reset the launcher back to a working state if I wrote the wrong value to it.
# Disclaimer
- I am not affiliated with <b>Samsung</b> or any of their working partners. I am an independent individual who loves the art of programming.
