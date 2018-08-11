---
layout: post
title: "Custom shadows for Android Views"
date: 2018-08-11
---
Android elements (especially lower than API 21) does not support shadows, except if using [CardView](https://developer.android.com/guide/topics/ui/layout/cardview) While CardView gets the `elevation` attribute, if the requirement is to  customize or control the shadow, this does not do the trick.

Let's say our requirement is to have a card with the following shadow attributes (comming from Adobe XD):
* `y = 6`
* `blur = 12`
* `color = #3C000000`

First we create the `drawable/shadow.xml`:
```xml
<shape>
        <!-- set the shadow color here -->
        <stroke
            android:width="2dp"
            android:color="#7000" />

        <!-- setting the thickness of shadow (positive value will give shadow on that side) -->

        <padding
            android:bottom="2dp"
            android:left="2dp"
            android:right="-1dp"
            android:top="-1dp" />

        <corners android:radius="3dp" />
    </shape>
```
