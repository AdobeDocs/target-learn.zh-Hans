---
title: 如何在单页应用程序(SPA)中实施at.js 2.0
description: Adobe Target的at.js 2.0提供了丰富的功能集，使您的企业能够在下一代客户端技术上实现个性化。 请按照以下步骤在单页应用程序(SPA)中实施at.js 2.0。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 在单页应用程序(SPA)中实施Adobe Target的at.js 2.0

Adobe Target的`at.js` 2.0提供了丰富的功能集，使您的企业能够在下一代客户端技术上实现个性化。 此版本着重于升级`at.js`，以便与单页应用程序(SPA)进行良性的交互。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中实施at.js 2.0

* 在单页应用程序的&lt;head>中实施`at.js` 2.0。
* 每次在SPA中查看更改时实施`adobe.target.triggerView()`函数。 可以使用各种技术来做到这一点，例如侦听URL哈希更改，侦听SPA触发的自定义事件，或将`triggerView()`代码直接嵌入应用程序。 您应该选择最适合您的特定单页应用程序的选项。
* 视图名称是`triggerView()`函数的第一个参数。 使用简单、清晰且唯一的名称，以便在Target的可视化体验编辑器中轻松选择它们。
* 您可以在较小的视图更改中以及非SPA上下文中触发视图，例如向无限滚动页面中移一半。
* `at.js` 2.0和`triggerView()`可以通过标签管理解决方案(如Adobe Experience Platform Launch)实现。

## at.js 2.0限制

升级之前，请注意以下`at.js` 2.0限制：

* `at.js` 2.0不支持跨域跟踪
* `at.js` 2.0不支持mboxOverride.browserIp和mboxSession URL参数
* 旧版函数mboxCreate、mboxDefine、mboxUpdate在`at.js` 2.0中已弃用。将显示默认内容，并且不会发出任何网络请求。

## 视频中使用的库页脚代码

以下代码已在视频期间添加到`at.js`库的“库页脚”部分。 它会在应用程序首次加载时触发，随后在应用程序中的任何哈希更改时触发。 它使用清除版本的哈希作为视图名称，哈希为空时使用“home”。 请注意，为了识别SPA，代码会在URL中查找文本“react/”，这很可能需要在您的网站上更新。 同时请记住，SPA可能更适合通过自定义事件触发`triggerView()`，或者通过将代码直接嵌入应用程序来触发。

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

* [了解at.js 2.0的工作方式（架构图）](understanding-how-atjs-20-works.md)
* [使用Adobe Target的可视化体验编辑器处理单页应用程序(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
