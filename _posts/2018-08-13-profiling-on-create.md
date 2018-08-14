---
layout: post
title: "Android: Profiling onCreate()"
date: 2018-08-13
---

While there is a lot of information on how ot use Android Studio's profiler (`Run-> Profile App`, then `record`) to measure where the execution time is spend in yor app, this cannot really measure cold start time (first `onCreate()`), since you cannot press record before it is actually started.

To do this, the easiest and most accurate aproach seems to be tu use the `Debug.startMethodTracing()` and `Debug.stopMethodTracing()`. Example:
```Java
 @Override
protected void onCreate(Bundle savedInstanceState) {
    Debug.startMethodTracing("main");
    //do some work
    Debug.stopMethodTracing();
}
```

When you compile and run this, the tracer will create a `/sdcard/app-package/main.trace` file. To get the file, you need to have adb in your `PATH` env, then pull it to your current folder:
```bash
adb pull /sdcard/yourapppackage/main.trace
```

If you cannot find the file, you can `"ssh"` into the system and find it:
```bash
adb shell
cd sdcard/
find | grep .trace
```
This will give you the exact location of the file.

Once you have the file, simply open it with Android Studio: `File->Open`, sort it by Inclusive Time and expore.
