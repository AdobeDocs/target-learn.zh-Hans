---
title: 功能标记
seo-title: 功能标记
description: Adobe Target可用于试验颜色、副本、按钮、文本和图像等UX功能，并将这些功能提供给特定受众。
seo-description: Adobe Target可用于试验颜色、副本、按钮、文本和图像等UX功能，并将这些功能提供给特定受众。
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---


# 功能标记

移动应用程序产品所有者需要灵活地在其应用程序中推出新功能，而无需投资于多个应用程序版本。 他们可能还希望逐步将功能推广到用户群的一定比例，以测试有效性。 Adobe Target可用于试验颜色、副本、按钮、文本和图像等UX功能，并将这些功能提供给特定受众。

在本课中，我们将创建一个“功能标志”优惠，它可用作启用特定应用程序功能的触发器。

## 学习目标

在本课程结束时，您将能够：

* 在批预回迁请求中添加新位置
* 创建 [!DNL Target] 活动，其优惠将用作功能标志
* 加载并验证应用程序中的功能标志优惠

## 将新位置添加到“预回迁”请求到主活动

在我们先前课程的演示应用程序中，我们将在“主页”活动的预回迁请求中添加一个名为“wetravel_feature_flag_recs”的新位置，并使用新的Java方法将其加载到屏幕。

>[!NOTE] 使用预回迁请求的好处之一是，添加新请求不会增加任何额外的网络开销或导致额外的负载工作，因为该请求被打包在预回迁请求中

首先，验证wetravel_feature_flag_recs常数是否添加在Constant.java文件中：

![添加功能标志常数](assets/feature_flag_constant.jpg)

下面是代码：

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

现在，将位置添加到预回迁请求并加载一个名为： `processFeatureFlags()`

![功能标志代码](assets/feature_flag_code.jpg)

下面是完整更新的代码：

```java
public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();

    Map<String, Object> params1;
    params1 = new HashMap<String, Object>();
    params1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");

    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_feature_flag_recs, params1));

    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    engageMessage();
                    processFeatureFlags();
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}

public void processFeatureFlags() {
    Target.loadRequest(Constant.wetravel_feature_flag_recs, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Feature Flags : " + s);
                            if(s != null && !s.isEmpty()) {
                                //enable or disable features
                            }
                        }
                    });
                }
            });
}
```

### 验证功能标志请求

添加代码后，在“主页”活动上运行模拟器并观看日志以获取更新的响应：

![验证功能标志位置](assets/feature_flag_code_logcat.jpg)

## 创建功能标志JSON优惠

我们现在将创建一个简单的JSON优惠，充当特定受众的标志或触发器——该受众将在其应用程序中接收功能推出。 在界 [!DNL Target] 面中，创建新优惠:

![创建功能标志JSON优惠](assets/feature_flag_json_offer.jpg)

我们将它命名为“功能标志v1”，其值为{“enable”:1}

![feature_flag_v1 JSON优惠](assets/feature_flag_json_name.jpg)

## 创建活动

现在，让我们使用该活动创建A/B测试优惠。 有关创建活动的详细步骤，请参阅上一课。 此活动只需要一个受众。 在实时场景中，您可能希望构建特定功能推广的特定自定义受众，然后将活动设置为使用这些受众。 在此示例中，我们只会将流量分配为50/50(50%给将看到功能更新的访客,50%给将看到标准体验的访客)。 以下是活动的配置：

1. 将活动命名为“功能标志”
1. 选择“wetravel_feature_flag_recs”位置
1. 将内容更改为“功能标志v1”JSON优惠

   ![功能标志活动配置](assets/feature_flag_activity.jpg)

1. 单击 **[!UICONTROL 添加体验]** ，以添加体验B。
1. 保留“wetravel_feature_flag_recs”位置
1. 保留 **[!UICONTROL 内容的默]** 认内容
1. Click **[!UICONTROL Next]** to advance to the [!UICONTROL Targeting] screen

   ![功能标志活动配置](assets/feature_flag_activity_2.jpg)

1. 在“定 [!UICONTROL 位] ”屏幕上，验证“流量 [!UICONTROL 分配] ”方法是否设置为默认设置（手动），以及每个体验是否具有默认的50%分配。 选择 **[!UICONTROL 下一]** 步以前进 **[!UICONTROL 到目标和设置]**。

   ![功能标志活动配置](assets/feature_flag_activity_3.jpg)

1. 将主要目 **[!UICONTROL 标设置为]** “转 **[!UICONTROL 化”]**。
1. 将操作设置为“ **[!UICONTROL 已查看Mbox”]**。 我们将使用“wetravel_context_dest”位置（因为该位置位于“确认”屏幕上，因此我们可以使用它来查看新功能是否导致更多转换）。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。

   ![功能标志活动配置](assets/feature_flag_activity_4.jpg)

激活活动.

## 验证功能标志活动

现在，使用模拟器来观察请求。 由于我们将定位设置为50%的用户，因此50%的用户将看到功能标志响应包含该 `{enable:1}` 值。

![功能标志验证](assets/feature_flag_validation.jpg)

如果您看不到价 `{enable:1}` 值，这意味着您没有成为体验的目标。 作为临时测试，为了强制显示优惠，您可以：

1. 取消激活活动。
1. 根据新功能体验将流量分配更改为100%。
1. 保存并重新激活。
1. 在模拟器上擦除数据，然后重新启动应用程序。
1. 优惠现在应返回 `{enable:1}` 值。

在实时场景中，响 `{enable:1}` 应可用于在应用程序中启用更多自定义逻辑，以显示要显示目标受众的特定功能集。

## 结论

干得好！ 您现在具备向特定用户受众推出功能所需的技能。
