# WebKit

```
dependencies {
  implemetation "androidx.webkit:webkit:1.0.0-alpha1"
}
```

### Enabling safe browsing
API Level 21 以上

```
if (WebViewFeature.isFeatureSupported(WebViewFeature.START_SAFE_BROWSING)) {
  WebViewCompat.startSafeBrowsing(context) { initialized -> 
    if (initialized) {
      // We are now safe browsing
    }
  }
}
```

### Browser library
android.support.customtabs -> andridx.browser

### Browser actions
Web へのアクションメニューを表示させる

[Example](https://github.com/NUmeroAndDev/BrowserActionsExample-android)

```
implementation 'androidx.browser:browser:1.0.0-alpha1'
```

* Simple
```
BrowerActionsIntent.openBrowserAction(context, uri)
```

* Custom Actions
メニューへ独自にアクションを追加できる
```
val openLinkIntent = Intent(Intent.ACTION_VIEW, uri)
val pendingIntent = PendingIntent.getActivity(context, 0, openLinkIntent, 0)
val myAction = BrowerActionItem("My Custom Action!", pendingIntent, R.drawable.ic_hoge)
val items = arrayListOf(myAction)

BrowerActionsIntent.openBrowserAction(context, uri, BrowserActionsIntent.URL_TYPE_NONE, items, defaultAction)
```

* With Receiver
メニューから何か選択された時の監視ができる
```
val defaultIntent = Intent().apply {
  setClass(applicationContext, BrowserActionReceiver::class.java)
}
val defaultAction = PendingIntent.getBroadcast(context, 0, defaultIntent, 0)

BrowerActionsIntent.openBrowserAction(context, uri, BrowserActionsIntent.URL_TYPE_NONE, arrayListOf(), defaultAction)

```
