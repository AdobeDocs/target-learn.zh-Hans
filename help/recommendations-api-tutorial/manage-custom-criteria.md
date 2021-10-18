---
title: 如何管理自定义标准
description: 本教程的本部分将指导开发人员完成使用Adobe Target API管理、创建、列表、编辑、获取和删除Adobe Target Recommendations标准所需的步骤。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: ee63bd3e-200a-4c08-b364-9f17a479033b
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 1%

---

# 管理自定义标准

有时，[!DNL Recommendations]提供的算法无法显示您要促销的特定项目。 在这种情况下，自定义标准为您提供了一种为给定关键项目或类别交付一组特定推荐项目的方法。 您可以定义关键项目或类别与推荐项目之间的映射，并将该映射导入为自定义标准。 [自定义标准文档](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en)中介绍了此过程。 如该文档中所述，您可以通过[!DNL Target]用户界面(UI)创建、编辑和删除自定义标准。 但是，[!DNL Target]还提供一组自定义标准API，以便对自定义标准进行更详细的管理。

>[!IMPORTANT]
>
>对于自定义标准，请遵循以下使用准则：
>
> 使用API为给定自定义标准执行所有操作（创建、编辑、删除），或使用UI执行所有操作（创建、编辑、删除）。 通过UI和API的组合管理自定义标准可能会导致信息冲突或意外结果。 例如，在UI中创建自定义标准，但随后通过API对其进行编辑，将不会反映您在UI中的更新，即使该标准将在后端进行更新（通过API可见）。

## 创建自定义标准

要使用[创建自定义标准API](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)创建自定义标准，语法为：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>如本练习所述，使用创建自定义标准API创建的自定义标准将显示在UI中，并且将保留这些标准。 您将无法从UI中编辑或删除它们。 您可以通过API **编辑或删除它们**，但无论采用哪种方式，它们都将继续显示在[!DNL Target] UI中。 要维护从UI编辑或删除选项，请根据[文档](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en)使用UI创建自定义标准，而不是使用创建自定义标准API。

只有在阅读上述警告并熟练地创建新自定义标准（该标准随后无法从UI中删除）后，才应继续阅读本教程。

1. 验证`TENANT_ID`和`API_KEY`的&#x200B;**创建自定义标准**&#x200B;引用之前建立的Postman环境变量。 使用下图进行比较。

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. 将&#x200B;**Body**&#x200B;添加为&#x200B;**raw** JSON，该JSON定义自定义标准CSV文件的位置。 将[创建自定义标准API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)文档中提供的示例用作模板，根据需要提供`environmentId`和其他值。 在本例中，我们使用LAST_PURCHASED作为键。

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. 发送请求并观察响应，其中包含您刚刚创建的自定义标准的详细信息。

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. 要验证已创建自定义标准，请在Adobe Target中导航到&#x200B;**[!UICONTROL Recommendations] > [!UICONTROL 标准]**&#x200B;并按名称搜索标准，或在下一步中使用&#x200B;**列出自定义标准API**。

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

在这种情况下，我们出错了。 让我们使用&#x200B;**List Custom Criteria API**&#x200B;更仔细地检查自定义标准，以调查该错误。

## 列出自定义标准

要检索所有自定义标准的列表以及每个标准的详细信息，请使用[列表自定义标准API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)。 语法为：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. 按照之前的方式验证`TENANT_ID`和`API_KEY`，并发送请求。 在响应中，请注意自定义标准ID以及有关前面所述错误消息的详细信息。
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

在这种情况下，由于服务器信息不正确而发生错误，这意味着[!DNL Target]无法访问包含自定义标准定义的CSV文件。 让我们编辑自定义标准以更正此问题。

## 编辑自定义标准

要更改自定义标准定义的详细信息，请使用[编辑自定义标准API](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)。 语法为：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 与之前一样，验证`TENANT_ID`和`API_KEY`。
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. 指定要编辑的（单个）自定义标准的标准ID。
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. 在正文中，为更新的JSON提供正确的服务器信息。 （对于此步骤，请指定对可以访问的服务器的FTP访问。）
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. 发送请求并记下响应。
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

让我们使用&#x200B;**获取自定义标准API**&#x200B;来验证更新的自定义标准是否成功。

## 获取自定义标准

要查看特定自定义标准的自定义标准详细信息，请使用[获取自定义标准API](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)。 语法为：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定要获取其详细信息的自定义标准的标准ID。 发送请求，并查看响应。
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. 验证成功。 （在本例中，请确认没有其他FTP错误。）
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. （可选）验证更新是否在UI中正确反映。
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## 删除自定义标准

使用前面提到的标准ID，使用[删除自定义标准API](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)删除自定义标准。 语法为：

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定要删除的（单个）自定义标准的标准ID。 单击&#x200B;**发送**。
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. 验证是否已使用获取自定义标准来删除该标准。
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
在这种情况下，预期的404错误表示找不到已删除的标准。

>[!NOTE]
>提醒一下，即使标准已删除，也不会从[!DNL Target] UI中删除，因为该标准是使用创建自定义标准API创建的。

恭喜！ 现在，您可以使用[!DNL Recommendations] API创建、列出、编辑、删除和获取有关自定义标准的详细信息。 在下一部分中，您将使用[!DNL Target]交付API来检索推荐。

[下一课程“使用服务器端交付API获取Recommendations”>](fetch-recs-server-side-delivery-api.md)
