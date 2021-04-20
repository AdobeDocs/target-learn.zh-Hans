---
title: 如何使用投放 API获取Recommendations
description: 本教程的这一部分将指导开发人员完成使用Adobe Target 投放 API获取推荐内容所需的步骤。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: 2c371ea17ce38928bcf3655a0d604a69e29963a0
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---


# 使用投放 API获取[!DNL Recommendations]

Adobe Target和Adobe Target [!DNL Recommendations] API可用于向网页提供响应，但也可用于非HTML体验，包括应用程序、屏幕、控制台、电子邮件、报亭和其他显示设备。 换句话说，当无法使用[!DNL Target]库和JavaScript时，**[!DNL Target]投放 API**&#x200B;仍允许我们访问所有[!DNL Target]功能，以提供个性化体验。

>[!NOTE]
>
> 当请求包含实际推荐（推荐产品或项目）的内容时，请使用[!DNL Target]投放API。

要检索推荐，请发送包含相应上下文信息的Adobe Target 投放 APIPOST调用，该信息可能包括用户ID(用于用户档案特定的推荐，如用户最近查看的项目)、相关mbox名称、mbox参数、用户档案参数或其他属性。 响应将包括JSON或HTML格式的推荐entity.ids（并可能包括其他实体数据），随后可在设备中显示。

适用于Adobe Target的[投放API](https://developers.adobetarget.com/api/delivery-api/)公开标准[!DNL Target]请求提供的所有现有功能。

>[!NOTE]
>投放API:
>* 使您能够以RESTful的方式检索位置和受众的体验或优惠。
>* 不需要身份验证。
>* 仅开机自检。
>* 不处理Cookie或重定向调用。
>* 不需要或识别“用户角色”。 它只需将内容或报告事件读取到[!DNL Target]边缘服务器。


要使用投放 API提供[!DNL Target]体验（包括推荐），请执行以下步骤：

1. 使用基于表单的书写器（而非可视体验书写器）创建[!DNL Target]活动（A/B、XT、AP或[!DNL Recommendations]）。
2. 使用投放 API可以获取对您刚刚创建的[!DNL Target]活动生成的请求的响应。

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 使用基于表单的体验编辑器创建推荐

要创建可与投放 API一起使用的建议，请使用[基于表单的书写器](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)。

1. 首先，创建并保存一个基于JSON的设计，以便在您的推荐中使用。 有关示例JSON以及在配置基于表单的活动时如何返回JSON响应的背景信息，请参阅[创建推荐设计](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html)中的文档。 在此示例中，设计名为&#x200B;*Simple JSON。*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. 在[!DNL Target]中，导航到&#x200B;**[!UICONTROL 活动] > [!UICONTROL 创建活动] > [!UICONTROL Recommendations]**，然后选择&#x200B;**[!UICONTROL 表单]**。

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. 选择一个属性，然后单击&#x200B;**[!UICONTROL 下一步]**。
4. 定义您希望用户接收推荐响应的位置。 以下示例使用名为&#x200B;*api_charter*&#x200B;的位置。 选择您之前创建的基于JSON的设计，名称为&#x200B;*简单JSON。*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 保存并激活推荐。 它将产生结果。 [结果准备就绪后](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html)，您可以使用投放 API检索它们。

## 使用投放 API

[投放API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API)的语法为：

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 请注意，客户端代码是必需的。 作为提醒，您可以在Adobe Target中找到您的客户端代码，方法是导航到&#x200B;**[!UICONTROL Recommendations] > [!UICONTROL 设置]**。 请注意&#x200B;**[!UICONTROL 推荐API令牌]**&#x200B;部分中的&#x200B;**[!UICONTROL 客户端代码]**值。
   ![client-code.png](assets/client-code.png)
1. 获得客户端代码后，构建投放API调用。 以下示例以[投放API邮件收藏集](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)中提供的&#x200B;**[!UICONTROL Web批Mboxes投放API调用]**&#x200B;开头，进行相关修改。 例如：
   * **browser**&#x200B;和&#x200B;**address**&#x200B;对象已从&#x200B;**Body**&#x200B;中删除，因为非HTML用例不需要这些对象
   * *api_* charteris作为此示例中的位置名
   * 已指定entity.id，因为此建议基于内容相似性，该相似性要求将当前项密钥传递给[!DNL Target]。
      ![server-side-投放-API-call.png请记](assets/server-side-delivery-api-call2.png)
住正确配置查询参数。例如，请务必指定 
`{{CLIENT_CODE}}`。<!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. 发送请求。 此操作针对&#x200B;*api_charter*&#x200B;位置执行，该位置上运行一个活动的建议，该建议由您的JSON设计定义，将输出一列表推荐实体。
1. 接收基于JSON设计的响应。
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
png响应包括键ID以及建议实体的实体ID。

以这种方式将具有[!DNL Recommendations]的投放 API用于使您能够在向非HTML设备上的访客显示建议之前执行其他步骤。 例如，您可以从投放 API中做出响应，在显示最终结果之前，从其他系统（如CMS、PIM或电子商务平台）对实体属性详细信息（库存、价格、评级等）执行额外的实时查找。

使用本教程中概述的方法，您可以让任何应用程序利用[!DNL Target]的响应来提供个性化的推荐！

## 实施示例

以下资源提供了各种非HTML重点实现的示例。 请记住，由于涉及系统和设备，每个实施都是独一无二的。

| 资源 | 详细信息 |
| --- | --- |
| [在AEM中使用REST风格的API](https://helpx.adobe.com/experience-manager/using/restful-services.html) | 如何创建和部署Adobe Experience Manager OSGi捆绑包，该捆绑包使用来自第三方RESTful Web服务的数据。 |
| [Adobe Target Everywhere — 在IoT中实施服务器端](https://expleague.azureedge.net/labs/L733/index.html) | Adobe峰会2019实验室，它为利用Adobe Target服务器端API的React应用程序提供实际操作体验。 |
| [Adobe Target在移动应用程序中的应用程序，无需Adobe SDK](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 本指南向您展示如何在移动应用程序中设置Adobe Target，而不安装Adobe SDK。 此解决方案使用Tealium SDK web视图和远程命令模块向Adobe 访客 API(Experience Cloud)和Adobe Target API发送和接收请求。 |
| [Adobe Target在移动应用程序中的工作方式](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | [!DNL Target]如何与Mobile SDK一起使用 |
| [配 [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] 置API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | 在Experience Platform Launch中配置[!DNL Target]扩展、向应用程序添加[!DNL Target]扩展以及实施[!DNL Target] API以请求活动、预取优惠和进入可视预览模式的步骤。 |
| [Adobe Target节点客户端](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 开源[!DNL Target] Node.js SDK v1.0 |
| [服务器端概述](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | 有关Adobe Target服务器端投放API、服务器端批处理投放API、Node.js SDK和Adobe Target [!DNL Recommendations] API的信息。 |
| [Adobe Campaign内容Recommendations在电子邮件中](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | 描述如何在Adobe Campaign中通过Adobe Target和Adobe I/O Runtime在电子邮件中利用内容推荐的博客。 |

## 使用API管理[!DNL Recommendations]设置

大多数情况下，推荐是在Adobe Target UI中配置的，然后通过[!DNL Target] API使用或访问，原因如下面各节中所述。 此UI-API协调很常见。 但是，有时用户可能希望通过API执行所有操作，包括设置和结果的使用。 尽管不常见，但用户可以绝对配置、执行、*和*&#x200B;使用完全使用API的推荐结果。

我们在[前面的部分](manage-catalog.md)中学习了如何管理Adobe Target Recommendations实体并在服务器端提供它们。 同样，Adobe I/O允许您管理标准、促销、集合和设计模板，而无需登录Adobe Target。 [此处](http://developers.adobetarget.com/api/recommendations/)可找到所有[!DNL Recommendations] API的完整列表，但此处是供参考的摘要。

| 资源 | 详细信息 |
| --- | --- |
| [收藏集](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | 列表、创建、获取、编辑和删除集合。 |
| [标准](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 列表并获取标准。 |
| [设计](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | 列表、创建、获取、编辑、删除和验证设计。 |
| [实体](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | 保存、删除和获取实体。 |
| [Promotions](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 列表、创建、获取、编辑和删除促销活动。 |
| [类别条件](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 列表、创建、获取、编辑和删除类别条件。 |
| [自定义条件](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 列表、创建、获取、编辑和删除自定义条件。 |
| [项目标准](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 列表、创建、获取、编辑和删除项目条件。 |
| [人气标准](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 列表、创建、获取、编辑和删除人气标准。 |
| [用户档案属性条件](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 列表、创建、获取、编辑和删除用户档案属性条件。 |
| [最近的标准](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 列表、创建、获取、编辑和删除最近使用的条件。 |
| [序列条件](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 列表、创建、获取、编辑和删除序列条件。 |

## 参考文档

* [Adobe Target API文档](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target 投放 API](https://developers.adobetarget.com/api/delivery-api/)
* [与电子 [!DNL Recommendations] 邮件集成](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 摘要和审阅

恭喜！ 完成本教程后，您学习了如何：
* [使用Recommendations API管理目录](manage-catalog.md)
* [使用Recommendations API管理自定义条件](manage-custom-criteria.md)
* [将投放 API与Recommendations结合使用](fetch-recs-server-side-delivery-api.md)
