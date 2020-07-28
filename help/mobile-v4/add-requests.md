---
title: 添加Adobe Target请求
description: 'AdobeMobile Services SDK(v4)提供Adobe Target方法和功能，使您能够为不同的用户提供不同的体验来个性化您的应用程序。   '
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---


# 添加Adobe Target请求

AdobeMobile Services SDK(v4)提供Adobe Target方法和功能，使您能够为不同的用户提供不同的体验来个性化您的应用程序。 通常，从应用程序向Adobe Target发出一个或多个请求，以检索个性化内容并衡量该内容的影响。

在本课中，您将通过实施请求来准备We.Travel应用程序以实现个 [!DNL Target] 性化。

## 先决条件

请务必下 [载并更新示例应用程序](download-and-update-the-sample-app.md)。

## 学习目标

在本课程结束时，您将能够：

* 使用批 [!DNL Target] 预取请求缓存多个优惠（即个性化内容）
* 加载预取的 [!DNL Target] 位置
* 实时 [!DNL Target] 加载位置（未预取）
* 从缓存中清除预取的位置
* 验证预取和实时请求

## 术语

下面是我们将在本教程的其余部分中使用的一些关键目标术语。

* **请求：**  向Adobe Target服务器发出网络请求
* **优惠:**  在用户界面（或使用API）中定义的代码片 [!DNL Target] 段或其他基于文本的内容，在响应中提供。 通常，在本 [!DNL Target] 机移动应用程序中使用JSON。
* **位置：**  给定给请求的用户定义名称，用于将优惠 [!DNL Target] 与特定请求关联
* **批请求：**  包含多个位置的单个请求
* **预回迁请求：**  一个请求，它检索优惠并将其缓存到内存中以供将来在应用程序中使用
* **批预取请求：**  预取多个位置优惠的单个请求
* **受众:**  在界面中定义或从其 [!DNL Target] 他访客应用程 [!DNL Target] 序(例如， “iPhone X访客”、“加利福尼亚州的访客”、“首个应用程序打开”)
* **活动:**  在用 [!DNL Target] 户界面(或通过 [!DNL Target] API)中定义的构建，它链接位置、优惠和受众以创建个性化体验

## 添加批预回迁请求

我们将在We.Travel中实施的第一个请求是批预取请求，主屏幕上 [!DNL Target] 有两个位置。 在稍后的课程中，我们将为这些位置配置显示消息的优惠，以帮助指导新用户完成预订过程。

预取请求通过 [!DNL Target] 缓存Adobe Target服务器响应(优惠)来尽可能少地获取内容。 批处理预取请求检索并缓存多个优惠，每个数据与不同位置相关联。 所有预取的位置都缓存在设备上，以供将来在用户会话中使用。 通过预取主屏幕上的多个位置，我们可以检索优惠以在访客导航应用程序时稍后使用。 有关预回迁方 [法的更](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html) 多详细信息，请参阅预回迁文档。

### 添加批预回迁请求

让我们更新HomeActivity控制器（主屏幕的源代码），它位于app > main > java > com.wetravel > Controller下。 我们将添加以红色显示的两个代码块：

我们将与HomeActivity控制器（主屏幕的源代码）进行开始，它位于app > main > java > com.wetravel > Controller下。

我们将添加以红色显示的两个代码块：

![HomeActivity预取代码](assets/homeactivity.jpg)

向下滚动到HomeActivity代码的末尾，在函数后面添加下面提供的代码 `setHeader()` 并替 *换当* 前函 `onResume()` 数：

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

您的IDE可能会警告您文件中 [!DNL Target] 没有导入的类。 请务必在HomeActivity [!DNL Target] 控制器顶部导入类，如下面的红色所示：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![导入目标类](assets/import.jpg)

您可能还会看到“找不到符号变量wetravel_engage_home”和“找不到符号变量wetravel_engage_search”的错误。 将这些内容添 `Constant.java` 加到文件中（在“应用程序”>“src”>“主”>“java”>“com”>“wetravel”>“Utils”）:

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![将位置名称添加到Constant.java文件](assets/constants.jpg)

### 批预取请求代码说明

| 代码 | 描述 |
|--- |--- |
| `targetPrefetchContent()` | 用户定义的函数（不是SDK的一部分），它使用 [!DNL Target] 方法检索和缓存两个 [!DNL Target] 位置。 |
| `prefetchContent()` | 发送 [!DNL Target] 预回迁请求的SDK方法 |
| `Constant.wetravel_engage_home` | 预取 [!DNL Target] 的位置名称，该名称将在主屏幕上显示其优惠内容 |
| `Constant.wetravel_engage_search` | 预取 [!DNL Target] 的位置名称，该名称将在搜索结果屏幕上显示其优惠内容。 由于这是预回迁中的第二个位置，因此此预回迁请求称为“预回迁批请求”。 |
| setUp() | 在预取优惠后呈现应用程序主屏幕的用户定 [!DNL Target] 义函数 |

### 关于异步与同步

使用我们刚刚实现的代码，预回迁请求将作为同步阻塞调用发出，就在主屏幕呈现之前。 当我们将新代码粘贴到HomeActivity控制器中时，我们将函数 `setUp()` 执行从函数移 `onResume()` 动到目标请求后。 在您希望在应用程序首次打开时个性化内容的情况下，这会很有用，因为它可确保来自目标服务器的个性化内容在第一个屏幕呈现之前已返回（或超时）。 要允许请求异步加载（在后台），只需在函数 `setUp()` 中调 `onCreate()` 用即可。

### 验证批预回迁请求

重新构建应用程序并打开Android模拟器。 （以下截屏使用Android Q版本9+上的Pixel 2,API级别29）。 预回迁响应应读取“收到预回迁响应”:

当主屏幕呈现时，应加载预回迁请求。 使用Logcat，筛选以 [!DNL "Target"] 查看请求和响应：

![在主屏幕上验证请求](assets/prefetch_validation.jpg)

如果未看到成功响应，请验证文件中的设置 `ADBMobileConfig.json` 和HomeActivity文件中的代码语法。

现在将两个位置缓存到设备。 位置名称将很快延迟加载到界 [!DNL Target] 面中，当您在活动中使用时，可以在各种下拉菜单中选择它们。

### 为每个缓存位置添加加载请求

现在，位置已预取并且其响应已缓存到设备，现在，让我们添加从缓存中检 `Target.loadRequest()` 索优惠内容的方法，以便您可以使用它更新应用程序。 我们将添加一个名为的新自定 `engageMessage()` 义方法，它将随预回迁请求一起运行。 `engageMessage()` 会打电话 `Target.loadRequest()`的。 `engageMessage()` 运行之 `setUp()` 前，以确保在设置屏幕之前调用加载请求。

首先，在 `engageMessage()` HomeActivity中添加wetravel_engage_home位置的调用和方法：

![添加第一个加载请求](assets/wetravel_engage_home_loadRequest.jpg)

下面是更新的代码：

```java
    public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();
        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();
                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

现在， `engageMessage()` 在SearchBusActivity中添加wetravel_engage_search位置的调用和方法。 请注意， `engageMessage()` 调用在调用之前 `onResume()` 在方法中设置， `setUpSearch()` 因此在设置屏幕之前运行：

![添加第二个加载请求](assets/wetravel_engage_search_loadRequest.jpg)

下面是更新的代码：

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

由于您刚刚向SearchBusActivity添加了目标方法，请务必导入 [!DNL Target] 类：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## 添加实时请求

我们将向应用程序添加的下一个请求将是感谢屏幕上的实时请求。 “实时”是指请求和响应都将立即应用（以后不缓存）。 在稍后的课程中，我们将使用此请求构建一个个性化的体验，该体验适合用户的旅行目的地。

因此，让我们在感谢屏幕上添加实时请求。 在ThankYouActivity文件中，我们将以红色显示更改：
![在感谢屏幕上添加实时位置](assets/thankyou.jpg)

滚动到ThankYouActivity文件的末尾。 注释掉函数中的三 `getRecommandations()` 行，并添加函数调 `targetLoadRequest()` 用：

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

将此代码行添加到函 `getRecommandations()` 数：

```java
targetLoadRequest(recommandation.recommandations);
```

现在，我们需要定义函 `targetLoadRequest()` 数：
![在感谢屏幕上添加实时位置](assets/thankyou2.jpg)

在函数之后添加此代码 `filterRecommendationBasedOnOffer()` 块：

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
            try {
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        AppDialogs.dialogLoaderHide();
                        filterRecommendationBasedOnOffer(recommandations, response);
                        recommandationbAdapter.notifyDataSetChanged();
                    }
                });
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    });
}
```

由于您刚刚向ThankYouActivity添加了目标方法，请务必导入目标类：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest()代码说明

| 代码 | 描述 |
|--- |--- |
| `targetLoadRequest()` | 用户定义的函数（不是SDK的一部分），它 `Target.loadRequest()` 将触发加载并显示wetravel_context_dest位置 |
| `Target.loadRequest()` | 向目标服务器发出请求的SDK方法 |
| Constant.wetravel_context_dest | 在界面中构建活动时，我们稍后将使用的分配给请求的位置名 [!DNL Target] 称 |
| `filterRecommendationBasedOnOffer()` | 应用程序中的用户定义函数，从目标响应中获取位置优惠并决定应用程序如何根据优惠的内容进行更改 |
| `recommandations.addAll()` | 应用程序中的用户定义函数，该函数在加载感谢屏幕时默认执行，但现在在收到目标响应并由 `filterRecommendationBasedOnOffer()` |

这是我们对应用程序进行的更复杂的更新，随后我们向主屏幕添加了请求，因此，让我们花点时间回顾一下我们所做的工作：

1. 通过注释掉代码行，我们中断了应用程序之前显示三个默认促销的行为
1. 我们告诉应用程序执行一个新函数，我们任意命名该函数为targetLoadRequest
1. 我们定义了 `targetLoadRequest` 函数，使用目标.loadRequest方法对目标进行请求，并在收到优惠响应 `filterRecommendationBasedOnOffer()` 时立即执行 [!DNL Target] 该函数。
1. 该函 `filterRecommendationBasedOnOffer()` 数解释响应并决定应将哪些促销应用到屏幕

这是在移动应用程序中使用时非常 [!DNL Target] 常见的使用模式。  它的功能非常强大，因为您可以在移动App的几乎任何方面进行个性化。 它还需要应用程序代码与稍后在界面中定义的优惠之间的 [!DNL Target] 协调。 由于这种协调，某些个性化使用案例可能要求您更新应用程序在App商店中以启动活动。

### 验证实时请求

打开Android模拟器并完成预订行程的所有步骤： “主页”>“总线搜索结果”>“席位选择”、“付款选项”（任何含空数据的付款选项均有效）。

在最后的“感谢您”屏幕上，观看Logcat以获得响应。 响应应应为“wetravel_context_dest”返回默认内容：

![在感谢屏幕上添加实时位置](assets/thankyou_validation.jpg)

## 清除从缓存预取的位置

在某些情况下，在会话期间可能需要清除预取的位置。 例如，在进行预订时，清除缓存位置是合理的，因为用户现在“参与”并了解预订过程。 如果他们在会话期间预订了另一次旅行，则他们不需要主屏幕和搜索结果屏幕上的原始位置来指导预订。 从缓存中清除位置并预取新优惠，以便进行折扣的第二次预订或其他相关的预订。 如果在会话期间发生预订，则可以将逻辑添加到主屏幕和搜索结果屏幕以预取新位置。

对于此示例，我们将在预订进行时清除会话的预取位置。 通过调用函数来完 `Target.clearPrefetchCache()` 成。 在函数中设置函 `targetLoadRequest()` 数，如下所示：

```java
Target.clearPrefetchCache()
```

![清除从缓存预取的位置](assets/clearPrefetch.jpg)

恭喜！ 您的应用程序现在具有个性化框架。 在下一课中，我们将通过向这些位置添加参数来增强我们的个性化功能。

**[下一个： &quot;添加参数&quot; >](add-parameters.md)**
