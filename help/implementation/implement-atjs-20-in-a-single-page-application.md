---
title: 在单页应用程序中实施Adobe Target的at.js 2.0(SPA)
seo-title: 在单页应用程序中实施Adobe Target的at.js 2.0(SPA)
description: 最新版本的 at.js 提供了丰富的功能集，使您的企业能够在下一代客户端技术上实现个性化。这个新版本着重升级了 at.js 以与单页应用程序 (SPA) 进行良性的交互。
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 8%

---


# 在单页应用程序中实施Adobe Target的at.js 2.0(SPA)

`at.js`的最新版本提供丰富的功能集，使您的企业能够基于下一代客户端技术进行个性化。 此新版本侧重于升级`at.js`以与单页应用程序(SPA)实现和谐的交互。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中实施at.js 2.0

* 在单页应用程序的&lt;head>中实施`at.js` 2.0。
* 只要SPA中视图发生更改，就实施`adobe.target.triggerView()`函数。 可采用各种方法来实现此目的，如监听URL哈希更改、监听SPA触发的自定义事件，或将`triggerView()`代码直接嵌入应用程序。 您应选择最适合特定单页应用程序的选项。
* 视图名是`triggerView()`函数的第一个参数。 使用简单、清晰和唯一的名称，在目标的视觉体验书写器中轻松进行选择。
* 您可以在较小的视图更改以及非SPA上下文（如半向下无限滚动页面）中触发视图。
* `at.js` 2.0，可 `triggerView()` 以通过标签管理解决方案实现，如Adobe Experience Platform Launch。

## at.js 2.0限制

升级之前，请注意`at.js` 2.0的以下限制：

* `at.js` 2.0中不支持跨域跟踪
* `at.js` 2.0中不支持mboxOverride.browserIp和mboxSession URL参数
* `at.js` 2.0中已弃用旧版函数mboxCreate、mboxDefine和mboxUpdate。将显示默认内容，不会发出网络请求。

## 视频中使用的库页脚代码

在视频过程中，以下代码已添加到`at.js`库的“库页脚”部分。 应用程序首次加载时将触发，然后在应用程序中进行任何哈希更改时触发。 它使用哈希的清理版本作为视图名，当哈希为空时使用“home”。 请注意，要识别SPA，代码会在URL中查找“react/”文本，该文本很可能需要在您的网站上进行更新。 同样要记住，SPA将`triggerView()`从自定义事件中触发或直接将代码嵌入到应用程序中可能更合适。

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## 其他资源

* [了解at.js 2.0的工作原理（架构图）](understanding-how-atjs-20-works.md)
* [将Adobe Target的可视体验书写器用于单页应用程序(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [从at.js 1.x升级到at.js 2.0文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)