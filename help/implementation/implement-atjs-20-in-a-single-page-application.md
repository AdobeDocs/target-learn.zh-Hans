---
title: 如何在单页应用程序(SPA)中实施at.js 2.0
description: Adobe Target的at.js 2.0提供了丰富的功能集，使您的企业能够在下一代客户端技术上实现个性化。 按照以下步骤在单页应用程序(SPA)中实施at.js 2.0。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# 在单页应用程序(SPA)中实施Adobe Target的at.js 2.0

Adobe Target的 `at.js` 2.0提供了丰富的功能集，使您的企业能够在下一代客户端技术上实现个性化。 此版本侧重于升级 `at.js` 与单页应用程序(SPA)进行协调的交互。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中实施at.js 2.0

* 实施 `at.js` 2.0中的 &lt;head> 单页应用程序的URL路径。
* 实施 `adobe.target.triggerView()` SPA函数。 可以使用各种技术来做到这一点，例如侦听URL哈希更改、侦听SPA触发的自定义事件或嵌入 `triggerView()` 代码直接放入您的应用程序中。 您应该选择最适合您的特定单页应用程序的选项。
* 视图名称是 `triggerView()` 函数。 使用简单、清晰且唯一的名称，以便在Target的可视化体验编辑器中轻松选择它们。
* 您可以在较小的视图更改中以及在非SPA上下文中触发视图，例如向无限滚动页面中移一半。
* `at.js` 2.0和 `triggerView()` 可以通过标签管理解决方案(如Adobe Experience Platform Launch)实现。

## at.js 2.0限制

请注意以下限制 `at.js` 2.0升级前：

* 中不支持跨域跟踪 `at.js` 2.0
* 不支持mboxOverride.browserIp和mboxSession URL参数 `at.js` 2.0
* 旧版函数mboxCreate、mboxDefine、mboxUpdate在中已弃用 `at.js` 2.0.将显示默认内容，不会发出任何网络请求。

## 视频中使用的库页脚代码

以下代码已添加到的“库页脚”部分 `at.js` 库播放视频。 它会在应用程序首次加载时触发，并在应用程序中的任何哈希更改时触发。 它使用哈希的清理版本作为视图名称，当哈希为空时使用“home”。 请注意，为了识别SPA，代码会在URL中查找文本“react/”，这很可能需要在您的网站上更新。 另请注意，可能更适合您的SPA触发 `triggerView()` 关闭自定义事件或通过将代码直接嵌入到应用程序中。

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
* [使用Adobe Target的可视化单页应用程序体验编辑器(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
