---
title: 添加Adobe Target请求
description: Adobe Mobile Services SDK (v4)提供了Adobe Target方法和功能，让您能够为不同用户使用不同的体验来个性化您的应用程序。
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 88a5be3f-d61f-43e7-997a-574ef56122ed
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---

# 添加Adobe Target请求

Adobe Mobile Services SDK (v4)提供了Adobe Target方法和功能，可让您为不同用户使用不同的体验来个性化您的应用程序。 通常，应用程序会向Adobe Target发出一个或多个请求，以检索个性化内容并衡量该内容的影响。

在本课程中，您将通过实施[!DNL Target]请求来准备We.Travel应用程序以进行个性化。

## 先决条件

请务必[下载并更新示例应用](download-and-update-the-sample-app.md)。

## 学习目标

在本课程结束时，您将能够：

* 使用批次预取请求缓存多个[!DNL Target]优惠（即个性化内容）
* 加载预获取的[!DNL Target]位置
* 实时加载[!DNL Target]位置（非预获取）
* 从缓存中清除预获取的位置
* 验证预获取的实时请求

## 术语

以下是我们将在本教程的剩余部分中使用的一些关键Target术语。

* **请求：**&#x200B;向Adobe Target服务器发出网络请求
* **选件：**&#x200B;在[!DNL Target]用户界面（或使用API）中定义的代码片段或其他基于文本的内容，将在响应中交付。 在本机移动设备应用程序中使用[!DNL Target]时通常使用JSON。
* **位置：**&#x200B;为请求提供的用户定义的名称，在[!DNL Target]界面中用于将选件与特定请求关联
* **批处理请求：**&#x200B;包含多个位置的单个请求
* **预取请求：**&#x200B;单个请求，该请求会检索选件并将其缓存到内存中以供将来在应用程序中使用
* **批处理预取请求：**&#x200B;预取多个位置选件的单个请求
* **受众：**&#x200B;在[!DNL Target]界面中定义或从其他Adobe应用程序共享给[!DNL Target]的一组访客(例如“iPhone X访客”、“加利福尼亚的访客”、“第一个应用程序打开”)
* **活动：** [!DNL Target]构造，在[!DNL Target]用户界面（或使用API）中定义，用于链接位置、选件和受众以创建个性化体验

## 添加批次预取请求

我们将在We.Travel中实施的第一个请求是批预取请求，主屏幕上具有两个[!DNL Target]位置。 在稍后的课程中，我们将为这些显示消息的位置配置选件，以帮助引导新用户完成预订过程。

预取请求通过缓存Adobe Target服务器响应（选件）尽可能少地获取[!DNL Target]内容。 批量预取请求可检索和缓存多个选件，每个选件都与不同的位置关联。 所有预获取的位置都缓存在设备上，以供将来在用户会话中使用。 通过在主屏幕上预取多个位置，我们可以检索选件以供稍后访客在应用程序中导航时使用。 有关预取方法的更多详细信息，请参阅[预取文档](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=zh-Hans)。

### 添加批次预回迁请求

让我们更新HomeActivity控制器（主屏幕的源代码），该控制器位于app > main > java > com.wetravel > Controller下。 我们将添加两个以红色显示的代码块：

我们将从HomeActivity控制器（主屏幕的源代码）开始，该控制器位于app > main > java > com.wetravel > Controller下。

我们将添加两个以红色显示的代码块：

![HomeActivity预获取代码](assets/homeactivity.jpg)

向下滚动到HomeActivity代码的末尾，并将下面提供的代码添加到`setHeader()`函数和&#x200B;*替换*&#x200B;当前`onResume()`函数之后：

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

IDE可能会警告您文件中没有导入[!DNL Target]类。 请确保导入HomeActivity控制器顶部的[!DNL Target]类，如下面的红色所示：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![导入目标类](assets/import.jpg)

您可能还会看到“找不到符号变量wetravel_engage_home”和“找不到符号变量wetravel_engage_search”的错误。 将它们添加到`Constant.java`文件（位于应用程序> src > main > java > com > wetravel > Utils中）：

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![将位置名称添加到Constant.java文件](assets/constants.jpg)

### 批量预取请求代码说明

| 代码 | 描述 |
|--- |--- |
| `targetPrefetchContent()` | 用户定义的函数(不是SDK的一部分)，它使用[!DNL Target]方法检索和缓存两个[!DNL Target]位置。 |
| `prefetchContent()` | 发送预取请求的[!DNL Target] SDK方法 |
| `Constant.wetravel_engage_home` | 预获取的[!DNL Target]位置名称将在主屏幕上显示其选件内容 |
| `Constant.wetravel_engage_search` | 预获取的[!DNL Target]位置名称将在搜索结果屏幕上显示其选件内容。 由于这是预取中的第二个位置，因此该预取请求称为“预取批处理请求”。 |
| setup() | 用户定义的函数，在预取[!DNL Target]选件后呈现应用程序的主屏幕 |

### 关于异步与同步

使用我们刚刚实施的代码，预取请求将作为同步、阻止调用在主屏幕呈现之前发出。 在将新代码粘贴到HomeActivity控制器中时，我们将`setUp()`函数的执行从`onResume()`函数移动到Target请求之后。 当您想要在应用程序首次打开时个性化内容时，这可能会很有用，因为它可以确保在第一个屏幕呈现之前来自Target服务器的个性化内容已返回（或超时）。 要允许异步加载请求（在后台），只需在`setUp()`函数中调用`onCreate()`即可。

### 验证批处理预取请求

重新构建应用程序并打开Android模拟器。 (以下屏幕截图使用Android Q版本9及更高版本（API级别29）上的像素2。) 预取响应应为“已收到预取响应”：

当主屏幕呈现时，应加载预取请求。 使用Logcat筛选[!DNL "Target"]以查看请求和响应：

![在主屏幕上验证请求](assets/prefetch_validation.jpg)

如果未看到成功的响应，请验证`ADBMobileConfig.json`文件中的设置以及HomeActivity文件中的代码语法。

两个位置现已缓存到设备。 位置名称将很快延迟加载到[!DNL Target]界面中，在活动中使用位置名称时，可在各种下拉菜单中选择这些名称。

### 为每个缓存的位置添加加载请求

现在，位置已预取且其响应已缓存到设备，接下来让我们添加`Target.loadRequest()`方法，该方法将从缓存中检索选件内容，以便您可以使用它来更新应用程序。 我们将添加一个名为`engageMessage()`的新自定义方法，它将随预取请求一起运行。 `engageMessage()`将调用`Target.loadRequest()`。 `engageMessage()`在`setUp()`之前运行，以确保在设置屏幕之前调用加载请求。

首先，为HomeActivity中的wetravel_engage_home位置添加`engageMessage()`调用和方法：

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

现在为SearchBusActivity中的wetravel_engage_search位置添加`engageMessage()`调用和方法。 请注意，`engageMessage()`调用是在调用`onResume()`之前在`setUpSearch()`方法中设置的，因此它在设置屏幕之前运行：

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

由于您刚刚向SearchBusActivity添加了Target方法，因此请务必导入[!DNL Target]类：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## 添加实时请求

我们将添加到应用程序的下一个请求将是“感谢”屏幕上的实时请求。 “实时”是指将发出请求并立即应用响应（以后不缓存）。 在稍后的课程中，我们将使用此请求构建一个体验，该请求将针对用户的旅行目的地进行个性化。

让我们在“感谢”屏幕上添加一个实时请求。 在ThankYouActivity文件中，我们将进行红色显示的更改：
![在感谢屏幕上添加实时位置](assets/thankyou.jpg)

滚动到ThankYouActivity文件的末尾。 注释掉`getRecommandations()`函数中的三行并添加`targetLoadRequest()`函数的调用：

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

将此代码行添加到`getRecommandations()`函数：

```java
targetLoadRequest(recommandation.recommandations);
```

现在，我们需要定义`targetLoadRequest()`函数：
![在感谢屏幕上添加实时位置](assets/thankyou2.jpg)

在`filterRecommendationBasedOnOffer()`函数后添加此代码块：

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

由于您刚刚向ThankYouActivity添加了Target方法，因此请务必导入Target类：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest()代码说明

| 代码 | 描述 |
|--- |--- |
| `targetLoadRequest()` | 用户定义的函数(不是SDK的一部分)，用于触发`Target.loadRequest()`，以加载并显示wetravel_context_dest位置 |
| `Target.loadRequest()` | 向Target服务器发出请求的SDK方法 |
| Constant.wetravel_context_dest | 在[!DNL Target]界面中构建活动时分配给请求的位置名称，我们稍后将使用该名称 |
| `filterRecommendationBasedOnOffer()` | 应用程序中一个用户定义的函数，它从Target响应中获取位置的选件，并根据选件内容决定应用程序应如何更改 |
| `recommandations.addAll()` | 应用程序中的用户定义的函数，以前在加载ThankYou屏幕时默认执行，但现在在`filterRecommendationBasedOnOffer()`收到并解析Target响应后执行 |

这是我们随后使用添加到主屏幕的请求对应用程序进行的更复杂的更新，因此，让我们花些时间回顾一下我们的操作：

1. 我们通过注释掉代码行，中断了应用程序之前显示三个默认促销活动的行为
1. 我们指示应用程序执行一个新函数，我们随意将其命名为targetLoadRequest
1. 我们定义了`targetLoadRequest`函数以使用Target.loadRequest方法向Target发出请求，并在收到`filterRecommendationBasedOnOffer()`优惠响应时立即执行[!DNL Target]函数
1. `filterRecommendationBasedOnOffer()`函数将解释响应并决定应将哪些促销活动应用于屏幕

在移动设备应用程序中使用[!DNL Target]时，这是一种非常常见的使用模式。  两者都非常强大，因为您可以对移动设备应用程序的几乎任何方面进行个性化。 它还需要应用程序代码与我们稍后将在[!DNL Target]界面中定义的选件之间进行协调。 由于这种协调，某些个性化用例可能要求您在应用商店中更新应用程序才能启动活动。

### 验证实时请求

打开Android模拟器并完成预订行程的所有步骤：主页>巴士搜索结果>座位选择、付款选项（任何包含空白数据的付款选项都将有效）。

在最后的“感谢”屏幕上，观看Logcat的响应。 响应应为“为&quot;wetravel_context_dest&quot;返回了默认内容：

![在感谢屏幕上添加实时位置](assets/thankyou_validation.jpg)

## 正在从缓存中清除预获取的位置

在某些情况下，可能需要在会话期间清除预获取的位置。 例如，在发生预订时，清除缓存的位置是有意义的，因为用户现在“参与”并了解预订过程。 如果他们在会话期间再次预订行程，则无需主屏幕和搜索结果屏幕上的原始位置来指导预订。 从缓存中清除位置，并为打折的第二次预订或其他相关方案预取新选件会更明智。 可以将逻辑添加到主屏幕和搜索结果屏幕以预取新位置（如果在会话期间进行了预订）。

对于此示例，我们只会在预订发生时清除会话的预获取位置。 这是通过调用`Target.clearPrefetchCache()`函数完成的。 在`targetLoadRequest()`函数中设置该函数，如下所示：

```java
Target.clearPrefetchCache()
```

![从缓存中清除预获取的位置](assets/clearPrefetch.jpg)

恭喜！您的应用程序现在具有个性化框架。 在下一课程中，我们将通过向这些位置添加参数来增强我们的个性化功能。

**[下一步：“添加参数”>](add-parameters.md)**
