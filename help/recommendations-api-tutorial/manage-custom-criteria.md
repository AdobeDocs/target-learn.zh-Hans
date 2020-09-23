---
title: 管理自定义条件
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target·Recommendations包含一组专用的API，允许您管理推荐产品和／或内容目录； 管理推荐算法和活动; 并在JSON、HTML或XML对象中提供推荐，以便在Web、移动、电子邮件、物联网和其他渠道中显示。
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 78b30bc0018527f9d8b2a5b50edee86e877d14c7
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# 管理自定义条件

有时，提供的 [!DNL Recommendations] 算法无法显示您希望提升的特定项目。 在这种情况下，自定义条件为您提供了一种为给定关键项目或类别提供一组特定推荐项目的方式。 定义关键项或类别与推荐项之间的映射，并将该映射作为自定义条件导入。 自定义标准文档中对此 [过程进行了说明](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)。 如该文档中所述，您可以通过用户界面(UI)创建、编辑和删除 [!DNL Target] 自定义条件。 但是， [!DNL Target] 还提供一组自定义条件API，允许对自定义条件进行更详细的管理。

>[!IMPORTANT]
>
>按照以下使用准则自定义标准：
>
> 使用API针对给定的自定义条件执行所有操作（创建、编辑、删除），或者使用UI执行所有操作（创建、编辑、删除）。 通过UI和API的组合管理自定义条件可能会导致信息冲突或意外结果。 例如，在UI中创建自定义条件，然后通过API编辑该条件不会反映您在UI中的更新，即使它将在后端更新（通过API可见）。

## 创建自定义条件

要使用“创建自定义条 [件”API创建自定义条件](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)，语法为：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>如本练习所述，使用“创建自定义条件API”创建的自定义条件将显示在UI中，它们将一直存在。 您将无法在UI中编辑或删除它们。 您可以通过API编辑或 **删除它们**，但无论采用哪种方式，它们都将继续显示在 [!DNL Target] UI中。 要保持在UI中进行编辑或删除的选项，请根据文档使用UI创 [建自定义条件](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)，而不是使用创建自定义条件API。

只有在您阅读上面的警告，并且习惯于创建新的自定义条件后，才能继续使用本教程，这些条件随后无法从UI中删除。

1. 验证 `TENANT_ID` 和 `API_KEY` 创建自定 **义条件引** 用先前建立的邮递员环境变量。 请使用下图进行比较。

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. 将您的 **Body** 添 **加为** 定义自定义条件CSV文件位置的原始JSON。 将“创建自定义条 [件API”文档中提供的](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) “示例”用作模板，根据需要 `environmentId` 提供您和其他值。 在本例中，我们使用LAST_PURCHASED作为密钥。

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. 发送请求并观察响应，该响应包含您刚刚创建的自定义条件的详细信息。

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. 要验证已创建自定义条件，请在Adobe Target内导 **[!UICONTROL 航到]“[!UICONTROL Recommendations]** ”>“条件 **”并按名称搜索条件，或在下一步** 中使用列表自定义条件API。

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

在这种情况下，我们有一个错误。 让我们使用列表自定义条件API更仔细地检查自定义条件， **以调查错误**。

## 列表自定义条件

要检索所有自定义条件的列表以及每个条件的详细信息，请使用 [列表自定义条件API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)。 语法为：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. 验证 `TENANT_ID` 并 `API_KEY` 像以前一样发送请求。 在响应中，请注意自定义条件ID以及前面提到的错误消息的详细信息。
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

在这种情况下，由于服务器信息不正确，导致出 [!DNL Target] 错，这意味着无法访问包含自定义条件定义的CSV文件。 让我们编辑自定义条件以更正此问题。

## 编辑自定义条件

要更改自定义条件定义的详细信息，请使 [用编辑自定义条件API](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)。 语法为：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 像 `TENANT_ID` 以 `API_KEY`前一样验证和。
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. 指定要编辑的（单个）自定义条件的条件ID。
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. 在正文中，提供更新的JSON以及正确的服务器信息。 （对于此步骤，指定对可访问的服务器的FTP访问。）
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. 发送请求并记录响应。
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

让我们使用“获取自定义标准API”验证更新的自 **定义标准是否成功**。

## 获取自定义条件

要视图特定自定义条件的自定义条件详细信息，请使 [用“获取自定义条件API](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)”。 语法为：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定要获取其详细信息的自定义条件的条件ID。 发送请求，并查看响应。
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. 验证成功。 （在本例中，请确认没有其他FTP错误。）
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. （可选）验证更新是否在UI中正确反映。
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## 删除自定义条件

使用前面提到的条件ID，使用删除自定义条件API [删除您的自定义条件](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)。 语法为：

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定要删除的（单个）自定义条件的条件ID。 单击&#x200B;**发送**。
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. 验证是否已使用“获取自定义条件”删除该条件。
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)在这种情况下，预期的404错误表示找不到已删除的条件。

>[!NOTE]
>作为提醒，即使删除了该条件，也 [!DNL Target] 不会从UI中删除该条件，因为它是使用“创建自定义条件”API创建的。

恭喜！ 您现在可以使用API创建、列表、编辑、删除和获取有关自定义条件的详细 [!DNL Recommendations] 信息。 在下一节中，您将使用 [!DNL Target] 投放API检索推荐。

[下一个“使用服务器端投放API获取Recommendations”>](fetch-recs-server-side-delivery-api.md)