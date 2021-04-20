---
title: 如何在单页应用程序中实施at.js 2.0(SPA)
description: Adobe Target的at.js 2.0提供丰富的功能集，使您的企业能够使用下一代客户端技术进行个性化。 按照以下步骤在单页应用程序(SPA)中实施at.js 2.0。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# 在单页应用程序中实施Adobe Target的at.js 2.0(SPA)

Adobe Target的`at.js` 2.0提供丰富的功能集，使您的企业能够使用下一代客户端技术进行个性化。 此版本侧重于升级`at.js`以与单页应用程序(SPA)实现和谐的交互。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中实施at.js 2.0

* 在单页应用程序的&lt;head>中实施`at.js` 2.0。
* 只要SPA中的视图发生更改，就实施`adobe.target.triggerView()`函数。 可以采用各种方法来实现此目的，例如侦听URL哈希更改、侦听SPA触发的自定义事件，或将`triggerView()`代码直接嵌入到您的应用程序中。 您应选择最适合特定单页应用程序的选项。
* 视图名是`triggerView()`函数的第一个参数。 使用简单、清晰和唯一的名称，在目标的视觉体验书写器中轻松进行选择。
* 您可以在较小的视图更改以及非SPA上下文（如向下半无限滚动页面）中触发视图。
* `at.js` 2.0，可 `triggerView()` 以通过标签管理解决方案(如Adobe Experience Platform Launch)实施。

## at.js 2.0限制

升级前，请注意`at.js` 2.0的以下限制：

* `at.js` 2.0中不支持跨域跟踪
* `at.js` 2.0中不支持mboxOverride.browserIp和mboxSession URL参数
* `at.js` 2.0中已弃用旧版函数mboxCreate、mboxDefine和mboxUpdate。将显示默认内容，不会发出网络请求。

## 视频中使用的库页脚代码

在视频过程中，下面的代码已添加到`at.js`库的“库页脚”部分。 应用程序首次加载时，随后在应用程序中的任何哈希更改时触发。 它使用哈希的清理版本作为视图名，当哈希为空时使用“home”。 请注意，为识别SPA，代码会在URL中查找文本“react/”，该文本很可能需要在您的网站上进行更新。 同时，请记住，SPA将`triggerView()`从自定义事件中触发或直接将代码嵌入应用程序可能更合适。

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
* [将Adobe Target的Visual Experience Composer用于单页应用程序(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [从at.js 1.x升级到at.js 2.0文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)