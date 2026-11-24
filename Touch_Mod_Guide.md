# MarcoTV Touch Edition 修改指南

本指南包含了为 Facebook Portal Plus、平板或车机适配触摸屏所需的核心代码替换片段。

## 1. 修改 AndroidManifest.xml
路径: `app/src/main/AndroidManifest.xml`

**修改或添加特性声明：**
```xml
<!-- 移除电视专用的 Leanback 限制 -->
<uses-feature android:name="android.software.leanback" android:required="false" />
<!-- 强制声明触摸屏支持 -->
<uses-feature android:name="android.hardware.touchscreen" android:required="true" />
```

**解除强行横屏 (适配 Portal Plus 可选竖屏)：**
找到主 `Activity`，将 `android:screenOrientation="landscape"` 改为：
```xml
android:screenOrientation="fullUser" 
```

## 2. 修改卡片点击与触摸反馈
路径: `app/src/main/res/layout/` 目录下（如 `item_app.xml`、`item_card.xml` 等列表卡片）

在每个 Item 的根节点中补充以下属性，确保手指点按直接生效，并自带波纹反馈：
```xml
android:clickable="true"
android:focusable="true"
android:foreground="?android:attr/selectableItemBackground"
```

## 3. 解除列表滑动拦截 (Java/Kotlin)
在 Android Studio 或 GitHub 网页端搜索 `setOnTouchListener`。
如果出现拦截滑动事件的代码（通常是为了纯靠遥控器移动），例如：
```kotlin
recyclerView.setOnTouchListener { _, _ -> true }
```
请将其直接**注释掉或删除**。
