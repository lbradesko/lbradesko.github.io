---
layout: post
title: "Android: Custom shadows for Views"
date: 2018-08-11
---
Android elements (especially lower than API 21) does not support shadows, except if using [CardView](https://developer.android.com/guide/topics/ui/layout/cardview) While CardView gets the `elevation` attribute, if the requirement is to  customize or control the shadow, this does not do the trick.

Let's say our requirement is to have a card with the following shadow attributes (coming from Adobe XD):
* `y = 6`
* `blur = 12`
* `color = #3C000000`

In theory the `blur` could be re-created with the custom set of XML shapes, but this would take unreasonably big amount of time. 

Better approach is to first generate the `9-patch` image using [online generator](http://inloop.github.io/shadow4android/), and copy it to `drawable/shadow.9.png`

Then create the `drawable/custom_shadow.xml` which consists of the image and a custom background:

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" android:shape="rectangle" >
    <item android:drawable="@drawable/shadow" />

    <item>
        <shape android:shape="rectangle" android:padding="15dp">
            <solid android:color="?attr/card_background_color"/>
        </shape>
    </item>
</layer-list>
```

And finally set the `custom_shadow.xml` as background of the view:
```xml
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@drawable/card_shadow"/>
```
