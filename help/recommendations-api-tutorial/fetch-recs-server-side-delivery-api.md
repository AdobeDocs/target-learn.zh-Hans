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


# 使用投放API获取[!DNL Recommendations]

Adobe Target和Adobe Target[!DNL Recommendations] API可用于对网页做出响应，但也可用于非HTML体验，包括应用程序、屏幕、控制台、电子邮件、报亭和其他显示设备。 换言之，当[!DNL Target]库和JavaScript无法使用时，**[!DNL Target]投放API**&#x200B;仍允许我们访问所有[!DNL Target]功能，以提供个性化体验。

>[!NOTE]
>
> 请求包含实际推荐（推荐产品或项目）的内容时，请使用[!DNL Target]投放API。

要检索推荐，请发送包含相应上下文信息的Adobe Target投放APIPOST调用，该信息可能包括用户ID(用于用户档案特定的推荐，如用户最近查看的项目)、相关mbox名称、mbox参数、用户档案参数或其他属性。 响应将包括JSON或HTML格式的推荐entity.id（并可能包括其他实体数据），随后可在设备中显示。

Adobe Target的[投放API](https://developers.adobetarget.com/api/delivery-api/)公开标准[!DNL Target]请求提供的所有现有功能。

>[!NOTE]
>投放API:
>* 使您能够以REST风格的方式检索位置和受众的体验或优惠。
>* 无需身份验证。
>* 仅开机自检。
>* 不处理cookie或重定向调用。
>* 不需要或识别“用户角色”。 它只需获取内容或向[!DNL Target]边缘服务器报告事件。


要使用投放API提供[!DNL Target]体验（包括建议），请执行以下步骤：

1. 使用基于表单的书写器（而非可视体验书写器）创建[!DNL Target]活动（A/B、XT、AP或[!DNL Recommendations]）。
2. 使用投放API获取对您刚刚创建的[!DNL Target]活动生成的请求的响应。

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 使用基于表单的体验书写器创建推荐

要创建可与投放API一起使用的推荐，请使用[基于表单的书写器](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)。

1. 首先，创建并保存一个基于JSON的设计以用于您的推荐。 有关JSON示例以及配置基于表单的活动时如何返回JSON响应的背景信息，请参阅[创建推荐设计](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html)中的文档。 在本例中，设计名称为&#x200B;*Simple JSON。*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. 在[!DNL Target]中，导航到&#x200B;**[!UICONTROL 活动] > [!UICONTROL 创建活动] > [!UICONTROL Recommendations]**，然后选择&#x200B;**[!UICONTROL 表单]**。

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. 选择属性，然后单击&#x200B;**[!UICONTROL 下一步]**。
4. 定义您希望用户接收推荐响应的位置。 以下示例使用名为&#x200B;*api_charter*&#x200B;的位置。 选择您以前创建的基于JSON的设计，名称为&#x200B;*简单JSON。*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 保存并激活推荐。 它将产生结果。 [结果准备就绪后](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html)，您可以使用投放API检索它们。

## 使用投放API

[投放API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API)的语法为：

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 请注意，客户端代码是必需的。 作为提醒，您可以通过导航至&#x200B;**[!UICONTROL Recommendations] > [!UICONTROL 设置]**&#x200B;在Adobe Target找到您的客户端代码。 请注意&#x200B;**[!UICONTROL 推荐API令牌]**&#x200B;部分中的&#x200B;**[!UICONTROL 客户端代码]**值。
   ![client-code.png](assets/client-code.png)
1. 获得客户代码后，构建投放API调用。 以下示例以[投放API邮件收藏集](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)中提供的&#x200B;**[!UICONTROL Web批量Mboxes投放API调用]**&#x200B;开头，进行相关修改。 例如：
   * **浏览器**&#x200B;和&#x200B;**地址**&#x200B;对象已从&#x200B;**Body**&#x200B;中删除，因为非HTML用例不需要这些对象
   * *api_* charteris作为此示例中的位置名称列出
   * 指定entity.id，因为此建议基于内容相似性，该相似性要求将当前项密钥传递给[!DNL Target]。
      ![server-side-投放-API-call.png记住](assets/server-side-delivery-api-call2.png)
正确配置查询参数。例如，请务必指定 
根据需要`{{CLIENT_CODE}}`。<!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![客户端代码3](assets/client-code3.png)
1. 发送请求。 此操作针对&#x200B;*api_charter*&#x200B;位置执行，该位置上运行有一个活动的推荐，该推荐由您的JSON设计定义，将输出一列表推荐实体。
1. 接收基于JSON设计的响应。
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
png响应包括密钥ID以及建议实体的实体ID。

以此方式将投放API与[!DNL Recommendations]一起使用使您能够在向非HTML设备上的访客显示建议之前执行其他步骤。 例如，您可以从投放API进行响应，在显示最终结果之前从其他系统（如CMS、PIM或电子商务平台）对实体属性详细信息（库存、价格、评级等）执行额外的实时查找。

使用本教程中介绍的方法，您可以让任何应用程序利用[!DNL Target]的响应来提供个性化的建议！

## 实施示例

以下资源提供了各种非HTML重点实现的示例。 请记住，由于涉及的系统和设备，每个实施都是独一无二的。

| 资源 | 详细信息 |
| --- | --- |
| [在AEM中使用RESTful API](https://helpx.adobe.com/experience-manager/using/restful-services.html) | 如何创建和部署Adobe Experience ManagerOSGi捆绑包，它消费来自第三方RESTful Web服务的数据。 |
| [Adobe Target无处不在——在物联网中实施服务器端](https://expleague.azureedge.net/labs/L733/index.html) | Adobe峰会2019实验室，它为利用Adobe Target服务器端API的React应用程序提供实际操作体验。 |
| [Adobe Target无AdobeSDK移动应用程序](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 本指南向您展示如何在移动应用程序中设置Adobe Target，而不安装AdobeSDK。 此解决方案使用Tealium SDK Web视图和远程命令模块发送和接收请求至Adobe访客API(Experience Cloud)和Adobe TargetAPI。 |
| [Adobe Target如何在移动应用中发挥作用](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | [!DNL Target]如何与Mobile SDK一起使用 |
| [配 [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] 置API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | 在Experience Platform Launch中配置[!DNL Target]扩展、将[!DNL Target]扩展添加到应用程序并实施[!DNL Target] API以请求活动、预取优惠和进入可视预览模式的步骤。 |
| [Adobe Target节点客户端](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 开放源[!DNL Target] Node.js SDK v1.0 |
| [服务器端概述](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | 有关Adobe Target服务器端投放API、服务器端批处理投放API、Node.js SDK和Adobe Target[!DNL Recommendations] API的信息。 |
| [Adobe Campaign内容Recommendations在电子邮件中](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | 描述如何在Adobe Campaign通过Adobe Target和Adobe I/O Runtime通过电子邮件利用内容推荐的博客。 |

## 使用API管理[!DNL Recommendations]设置

大多数时间，推荐是在Adobe TargetUI中配置的，然后通过[!DNL Target] API使用或访问，原因如上面各节所述。 此UI-API协调很常见。 但是，有时用户可能希望通过API执行所有操作，包括设置和结果的使用。 尽管不常见，但用户完全可以使用API配置、执行&#x200B;*和*&#x200B;来充分利用推荐结果。

我们在前面的[一节](manage-catalog.md)中学习了如何管理Adobe TargetRecommendations实体并在服务器端交付它们。 同样，Adobe I/O允许您管理标准、促销、集合和设计模板，无需登录Adobe Target。 [此处](http://developers.adobetarget.com/api/recommendations/)可找到所有[!DNL Recommendations] API的完整列表，但此处是供参考的摘要。

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
