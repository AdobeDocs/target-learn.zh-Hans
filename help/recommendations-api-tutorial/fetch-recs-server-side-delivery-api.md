---
title: 使用投放API获取Recommendations
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target·Recommendations包含一组专用的API，允许您管理推荐产品和／或内容目录；管理推荐算法和活动;并在JSON、HTML或XML对象中提供推荐，以便在Web、移动、电子邮件、物联网和其他渠道中显示。
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 0%

---


# 使用 [!DNL Recommendations] 投放API获取

Adobe Target和Adobe Target [!DNL Recommendations] 州API可用于提供对网页的响应，但也可用于非基于HTML的体验，包括应用程序、屏幕、控制台、电子邮件、报亭和其他显示设备。 换言之，当无法 [!DNL Target] 使用库和JavaScript时，投放 **[!DNL Target]API** 仍允许我们访问各种功能， [!DNL Target] 以提供个性化体验。

>[!NOTE]
>
> 请求包含实际推荐（推荐产品或项目）的内容时，请使用 [!DNL Target] 投放API。

要检索推荐，请发送包含相应上下文信息的Adobe Target投放APIPOST调用，该信息可能包括用户ID(用于用户档案特定的推荐，如用户最近查看的项目)、相关mbox名称、mbox参数、用户档案参数或其他属性。 响应将包括JSON或HTML格式的推荐entity.id（并可能包括其他实体数据），随后可在设备中显示。

Adobe Target [的投放](https://developers.adobetarget.com/api/delivery-api/) API公开了标准请求提供的所有现 [!DNL Target] 有功能。

>[!NOTE]
>投放API:
>* 使您能够以REST风格的方式检索位置和受众的体验或优惠。
>* 无需身份验证。
>* 仅开机自检。
>* 不处理cookie或重定向调用。
>* 不需要或识别“用户角色”。 它只需将内容或报告事件存储到 [!DNL Target] 边缘服务器。


要使用投放API提供体验( [!DNL Target] 包括推荐)，请执行以下步骤：

1. 使用基 [!DNL Target] 于表单的书写器(而非可视体 [!DNL Recommendations]验书写器)创建活动（A/B、XT、AP或）。
2. 使用投放API获取对您刚刚创建的活动生成的 [!DNL Target] 请求的响应。

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 使用基于表单的体验书写器创建推荐

要创建可与投放API一起使用的推荐，请使用基 [于表单的书写器](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)。

1. 首先，创建并保存一个基于JSON的设计以用于您的推荐。 有关JSON示例以及配置基于表单的活动时如何返回JSON响应的背景信息，请参阅创建推荐 [设计相关文档](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html)。 在此示例中，该设计命名为 *Simple JSON。*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. 在中 [!DNL Target]，导航到 **[!UICONTROL 活动]>创[!UICONTROL 建活动]>[!UICONTROL Recommendations,]**&#x200B;然后选 ****&#x200B;择表。

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. 选择一个属性，然后单击 **[!UICONTROL 下一步]**。
4. 定义您希望用户接收推荐响应的位置。 以下示例使用名为api_charter *的位置*。 选择您的基于JSON的设计，该设计以前创建，名 *为Simple JSON。*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 保存并激活推荐。 它将产生结果。 [结果准备就绪后](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html)，您可以使用投放API检索它们。

## 使用投放API

The syntax for the [Delivery API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) is:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 请注意，客户端代码是必需的。 作为提醒，您可以通过导航至“Adobe Target”>“设置”在Recommendations **[!UICONTROL 找到您]的客[!UICONTROL 户代码]**。 请注意 **[!UICONTROL Recommendation API]** Token部分 **[!UICONTROL 中的Client Code值]** 。
   ![client-code.png](assets/client-code.png)
1. 获得客户代码后，构建投放API调用。 以下示例以投放API邮 **[!UICONTROL 件集合中提供的]** Web批 [量Mbox投放API调用开始](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)，并进行相关修改。 例如：
   * 浏 **览** 器和地 **址对象已从Body中删** 除 ****，因为非HTML用例不需要它们
   * *api_charter* 在此示例中列为位置名称
   * 指定entity.id，因为此建议基于内容相似性，该相似性要求将当前项密钥传递给 [!DNL Target]。
      ![server-side-投放-API-call.png请记](assets/server-side-delivery-api-call2.png)住正确配置查询参数。 例如，请务必`{{CLIENT_CODE}}` 指定。 <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. 发送请求。 此操作会根 *据api_charter* 位置执行，该位置上运行有活动的建议，定义为JSON设计，该设计将输出一列表推荐实体。
1. 接收基于JSON设计的响应。
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)响应包括密钥ID以及建议实体的实体ID。

通过这种方 [!DNL Recommendations] 式使用投放API，您可以在非HTML设备上向访客显示建议之前执行其他步骤。 例如，您可以从投放API进行响应，在显示最终结果之前从其他系统（如CMS、PIM或电子商务平台）对实体属性详细信息（库存、价格、评级等）执行额外的实时查找。

使用本教程中概述的方法，您可以获取任何应用程序来利用响应来 [!DNL Target] 提供个性化的建议！

## 实施示例

以下资源提供了各种非HTML重点实现的示例。 请记住，由于涉及的系统和设备，每个实施都是独一无二的。

| 资源 | 详细信息 |
| --- | --- |
| [在AEM中使用RESTful API](https://helpx.adobe.com/experience-manager/using/restful-services.html) | 如何创建和部署Adobe Experience ManagerOSGi捆绑包，它消费来自第三方RESTful Web服务的数据。 |
| [Adobe Target无处不在——在物联网中实施服务器端](https://expleague.azureedge.net/labs/L733/index.html) | Adobe峰会2019实验室，它为利用Adobe Target服务器端API的React应用程序提供实际操作体验。 |
| [Adobe Target无AdobeSDK移动应用程序](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 本指南向您展示如何在移动应用程序中设置Adobe Target，而不安装AdobeSDK。 此解决方案使用Tealium SDK Web视图和远程命令模块发送和接收请求至Adobe访客API(Experience Cloud)和Adobe TargetAPI。 |
| [Adobe Target如何在移动应用中发挥作用](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | 如 [!DNL Target] 何与Mobile SDK一起使用 |
| [配 [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] 置API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | 在Experience Platform Launch中配 [!DNL Target] 置扩展、将扩展添加 [!DNL Target] 到应用程序以及实现API以请求 [!DNL Target] 活动、预取优惠和进入可视预览模式的步骤。 |
| [Adobe Target节点客户端](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 开放源 [!DNL Target] Node.js SDK v1.0 |
| [服务器端概述](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | 有关Adobe Target服务器端投放API、服务器端批处理投放API、Node.js SDK和Adobe TargetAPI的信 [!DNL Recommendations] 息。 |
| [Adobe Campaign内容Recommendations在电子邮件中](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | 描述如何在Adobe Campaign通过Adobe Target和Adobe I/O Runtime通过电子邮件利用内容推荐的博客。 |

## 使用 [!DNL Recommendations] API管理设置

大多数时间，推荐是在Adobe TargetUI中配置的，然后通过API使 [!DNL Target] 用或访问，原因如上面各节所述。 此UI-API协调很常见。 但是，有时用户可能希望通过API执行所有操作，包括设置和结果的使用。 尽管不常见，但用户完全可以使用API *配置* 、执行和利用推荐结果。

我们在前面的一 [节中学习](manage-catalog.md) ，如何管理Adobe TargetRecommendations实体并在服务器端提供它们。 同样，AdobeI/O允许您管理标准、促销、集合和设计模板，无需登录Adobe Target。 此处可以找到所 [!DNL Recommendations] 有API的完 [整列表](http://developers.adobetarget.com/api/recommendations/)，但此处是供参考的摘要。

| 资源 | 详细信息 |
| --- | --- |
| [收藏集](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | 列表、创建、获取、编辑和删除集合。 |
| [标准](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 列表并获取标准。 |
| [设计](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | 列表、创建、获取、编辑、删除和验证设计。 |
| [实体](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | 保存、删除和获取实体。 |
| [促销](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 列表、创建、获取、编辑和删除促销。 |
| [类别标准](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 列表、创建、获取、编辑和删除类别条件。 |
| [自定义条件](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 列表、创建、获取、编辑和删除自定义条件。 |
| [项目标准](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 列表、创建、获取、编辑和删除项目条件。 |
| [人气标准](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 列表、创建、获取、编辑和删除人气标准。 |
| [用户档案属性条件](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 列表、创建、获取、编辑和删除用户档案属性条件。 |
| [最近的标准](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 列表、创建、获取、编辑和删除最近使用的条件。 |
| [序列条件](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 列表、创建、获取、编辑和删除序列条件。 |

## 参考文档

* [Adobe TargetAPI文档](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target投放API](https://developers.adobetarget.com/api/delivery-api/)
* [与电子 [!DNL Recommendations] 邮件集成](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 摘要和审阅

恭喜！ 完成本教程后，您学习了如何：
* [使用RecommendationsAPI管理目录](manage-catalog.md)
* [使用RecommendationsAPI管理自定义条件](manage-custom-criteria.md)
* [将投放API与Recommendations](fetch-recs-server-side-delivery-api.md)
