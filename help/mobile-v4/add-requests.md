---
title: 添加Adobe Target请求
description: 'AdobeMobile Services SDK(v4)提供了Adobe Target方法和功能，使您能够为不同的用户提供不同的体验，从而将您的应用程序个性化。   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 88a5be3f-d61f-43e7-997a-574ef56122ed
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# 添加Adobe Target请求

AdobeMobile Services SDK(v4)提供了Adobe Target方法和功能，使您能够为不同的用户提供不同的体验来个性化您的应用程序。 通常，会从应用程序向Adobe Target发出一个或多个请求，以检索个性化内容并衡量该内容的影响。

在本课程中，您将通过实施[!DNL Target]请求来准备We.Travel应用程序以进行个性化。

## 先决条件

请确保[下载并更新示例应用程序](download-and-update-the-sample-app.md)。

## 学习目标

在本课程结束时，您将能够：

* 使用批量预取请求缓存多个[!DNL Target]选件（即个性化内容）
* 加载预取的[!DNL Target]位置
* 实时加载[!DNL Target]位置（未预取）
* 清除从缓存中预取的位置
* 验证预取和实时请求

## 术语

下面是我们将在本教程的其余部分中使用的一些关键Target术语。

* **请求：**  对Adobe Target服务器的网络请求
* **选件：**  在用户界面（或使用API）中定义的代码 [!DNL Target] 片段或其他基于文本的内容，将在响应中交付。在本机移动设备应用程序中使用[!DNL Target]时，通常为JSON。
* **位置：**  为请求提供的用户定义的名称，用于将选件与 [!DNL Target] 特定请求关联
* **批量请求：**  包含多个位置的单个请求
* **预取请求：**  一个请求，用于检索选件并将其缓存到内存中，以供将来在应用程序中使用
* **批量预取请求：**  一个请求，用于预取多个位置的选件
* **受众：**  在界面中定义或从其 [!DNL Target] 他Adobe应 [!DNL Target] 用程序(例如，“iPhone X访客”、“加利福尼亚的访客”、“首次应用程序打开”)
* **活动：**  构建， [!DNL Target] 在用户界面中定 [!DNL Target] 义（或使用API），用于链接位置、选件和受众以创建个性化体验

## 添加批量预取请求

我们将在We.Travel中实施的第一个请求是批量预取请求，主屏幕上有两个[!DNL Target]位置。 在稍后的课程中，我们将为这些显示消息的位置配置选件，以帮助指导新用户完成预订过程。

预取请求通过缓存Adobe Target服务器响应（选件）来尽可能少地获取[!DNL Target]内容。 批量预取请求可检索和缓存多个选件，每个选件与一个不同的位置关联。 所有预取的位置都会缓存在设备上，以供将来在用户会话中使用。 通过预取主屏幕上的多个位置，我们可以检索选件，以便在访客在应用程序中导航时稍后使用。 有关预取方法的更多详细信息，请参阅[预取文档](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=en)。

### 添加批量预取请求

让我们更新HomeActivity控制器（主屏幕的源代码），它位于应用程序>主> java > com.wetravel >控制器下。 我们将添加以红色显示的两个代码块：

我们将从HomeActivity控制器（主屏幕的源代码）开始，它位于应用程序>主> java > com.wetravel >控制器下。

我们将添加以红色显示的两个代码块：

![HomeActivity预取代码](assets/homeactivity.jpg)

向下滚动到HomeActivity代码的末尾，并在`setHeader()`函数和&#x200B;*替换*&#x200B;当前`onResume()`函数之后添加下面提供的代码：

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

IDE可能会警告您文件中没有导入[!DNL Target]类。 确保在HomeActivity控制器顶部导入[!DNL Target]类，如下红色所示：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![导入目标类](assets/import.jpg)

您可能还会看到“无法找到符号变量wetravel_engage_home”和“无法找到符号变量wetravel_engage_search”的错误。 将这些内容添加到`Constant.java`文件中（在应用程序> src >主> java > com > wetravel >实用工具中）：

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![将位置名称添加到Constant.java文件](assets/constants.jpg)

### 批量预取请求代码说明

| 代码 | 描述 |
|--- |--- |
| `targetPrefetchContent()` | 用户定义的函数（不是SDK的一部分），该函数使用[!DNL Target]方法检索和缓存两个[!DNL Target]位置。 |
| `prefetchContent()` | 发送预取请求的[!DNL Target] SDK方法 |
| `Constant.wetravel_engage_home` | 预取了[!DNL Target]位置名称，该名称将在主屏幕上显示其选件内容 |
| `Constant.wetravel_engage_search` | 预取了[!DNL Target]位置名称，该名称将在搜索结果屏幕上显示其选件内容。 由于这是预取中的第二个位置，因此此预取请求称为“预取批处理请求”。 |
| setUp() | 用户定义的函数，在预取[!DNL Target]选件后呈现应用程序的主屏幕 |

### 关于异步与同步

使用我们刚刚实施的代码，在主屏幕呈现之前，预取请求将作为同步的阻止调用进行。 将新代码粘贴到HomeActivity控制器后，我们将`setUp()`函数的执行从`onResume()`函数移至Target请求之后。 如果您希望在应用程序首次打开时对内容进行个性化，这样可能会有所帮助，因为它可确保来自Target服务器的个性化内容在首次屏幕呈现之前返回（或超时）。 要允许异步加载请求（在后台），只需在`onCreate()`函数中调用`setUp()`即可。

### 验证批量预取请求

重新构建应用程序并打开Android模拟器。 （以下屏幕截图使用Android Q版本9+ API级别29上的Pixel 2）。 预取响应应为“收到预取响应”：

当主屏幕呈现时，应会加载预取请求。 使用Logcat，筛选[!DNL "Target"]以查看请求和响应：

![在主屏幕上验证请求](assets/prefetch_validation.jpg)

如果未看到成功响应，请验证`ADBMobileConfig.json`文件中的设置和HomeActivity文件中的代码语法。

现在，有两个位置已缓存到设备中。 在[!DNL Target]界面中，位置名称会很快延迟加载，在该界面中，当您在活动中使用位置名称时，可以在各种下拉菜单中选择它们。

### 为每个缓存位置添加加载请求

现在，已预取位置并将其响应缓存到设备中，接下来让我们添加`Target.loadRequest()`方法，该方法从缓存中检索选件内容，以便您可以使用它更新应用程序。 我们将添加一个名为`engageMessage()`的新自定义方法，该方法将随预取请求一起运行。 `engageMessage()` 将调用 `Target.loadRequest()`。`engageMessage()` 运行之 `setUp()` 前，以确保在设置屏幕之前调用加载请求。

首先，在HomeActivity中为wetravel_engage_home位置添加`engageMessage()`调用和方法：

![添加第一个加载请求](assets/wetravel_engage_home_loadRequest.jpg)

以下是更新的代码：

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

现在，为SearchBusActivity中的wetravel_engage_search位置添加`engageMessage()`调用和方法。 请注意，在`onResume()`方法中设置了`engageMessage()`调用后，再调用`setUpSearch()`，这样该调用便会在屏幕设置之前运行：

![添加第二个加载请求](assets/wetravel_engage_search_loadRequest.jpg)

以下是更新的代码：

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

由于您刚刚将Target方法添加到SearchBusActivity，因此请务必导入[!DNL Target]类：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## 添加实时请求

我们将向应用程序添加的下一个请求将是感谢屏幕上的实时请求。 “实时”是指将发出请求并立即应用响应（不会在以后缓存）。 在稍后的课程中，我们将使用此请求构建一个体验，该体验将个性化到用户的旅行目的地。

因此，让我们在感谢屏幕上添加实时请求。 在ThankYouActivity文件中，我们将以红色进行更改：
![在感谢屏幕上添加实时位置](assets/thankyou.jpg)

滚动到ThankYouActivity文件的结尾。 注释`getRecommandations()`函数中的三行，并添加`targetLoadRequest()`函数的调用：

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

将此代码行添加到`getRecommandations()`函数中：

```java
targetLoadRequest(recommandation.recommandations);
```

现在，我们需要定义`targetLoadRequest()`函数：
![在感谢屏幕上添加实时位置](assets/thankyou2.jpg)

在`filterRecommendationBasedOnOffer()`函数后面添加此代码块：

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

由于您刚刚向ThankYouActivity中添加了Target方法，因此请务必导入Target类：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest()代码说明

| 代码 | 描述 |
|--- |--- |
| `targetLoadRequest()` | 用户定义的函数（不是SDK的一部分），该函数触发`Target.loadRequest()`，该函数加载并显示wetravel_context_dest位置 |
| `Target.loadRequest()` | 向Target服务器发出请求的SDK方法 |
| Constant.wetravel_context_dest | 在[!DNL Target]界面中构建活动时，为稍后将使用的请求分配的位置名称 |
| `filterRecommendationBasedOnOffer()` | 应用程序中用户定义的函数，用于从Target响应中获取位置选件，并根据选件的内容决定应用程序应如何更改 |
| `recommandations.addAll()` | 应用程序中用户定义的函数，该函数在默认情况下加载ThankYou屏幕时执行，但现在在收到Target响应并由`filterRecommendationBasedOnOffer()`解析后执行 |

这是我们对应用程序进行的更复杂的更新，之后我们向主屏幕中添加了请求，因此，让我们花些时间回顾一下我们所做的工作：

1. 我们通过注释掉代码行来中断应用程序之前显示三次默认促销活动的行为
1. 我们告知应用程序执行一个新函数，该函数可任意命名为targetLoadRequest
1. 我们定义了`targetLoadRequest`函数以使用Target.loadRequest方法向Target发出请求，并在收到[!DNL Target]选件响应时立即执行`filterRecommendationBasedOnOffer()`函数
1. `filterRecommendationBasedOnOffer()`函数解释响应并决定应将哪些促销活动应用于屏幕

在移动设备应用程序中使用[!DNL Target]时，这是一种非常常见的使用模式。  它功能非常强大，因为您几乎可以对移动设备应用程序的任何方面进行个性化。 此外，还需要在应用程序代码与选件之间进行协调，我们稍后将在[!DNL Target]界面中定义这些选件。 由于这种协调，某些个性化用例可能需要您在应用商店中更新应用程序才能启动活动。

### 验证实时请求

打开Android模拟器并完成所有步骤以预订行程：首页>总线搜索结果>座位选择、付款选项（任何包含空白数据的付款选项均可使用）。

在最后的“谢谢您”屏幕上，观看Logcat的响应。 响应应应为“Wetravel_context_dest”返回默认内容：

![在感谢屏幕上添加实时位置](assets/thankyou_validation.jpg)

## 清除从缓存预取的位置

在某些情况下，可能会需要在会话期间清除预取的位置。 例如，在进行预订时，清除缓存位置是明智的，因为用户现在“参与”并了解预订过程。 如果他们在会话期间预订了另一次旅行，则无需在主屏幕和搜索结果屏幕上显示原始位置来指导预订。 从缓存中清除位置并预取新选件（可能是折扣第二次预订或其他相关情景）更合理。 如果会话期间发生预订，则可以将逻辑添加到主屏幕和搜索结果屏幕中以预取新位置。

对于此示例，我们将在预订进行时清除会话的预取位置。 这可通过调用`Target.clearPrefetchCache()`函数来完成。 在`targetLoadRequest()`函数内设置函数，如下所示：

```java
Target.clearPrefetchCache()
```

![清除从缓存预取的位置](assets/clearPrefetch.jpg)

恭喜！ 您的应用程序现在具有个性化框架。 在下一课程中，我们将通过向这些位置添加参数来增强我们的个性化功能。

**[下一步：&quot;添加参数&quot; >](add-parameters.md)**
