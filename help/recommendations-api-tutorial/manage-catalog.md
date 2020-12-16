---
title: 使用API管理您的Recommendations目录
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
source-wordcount: '931'
ht-degree: 1%

---


# 使用API管理[!DNL Recommendations]目录

此时，您已学习如何使用JWT身份验证流生成访问令牌，以将Adobe Target管理API与Adobe I/O结合使用。

您可以使用[RecommendationsAPI](https://developers.adobetarget.com/api/recommendations/)添加、更新或删除推荐目录中的项目。 与其他Adobe Target管理API一样，[!DNL Recommendations] API需要身份验证。

>[!TIP]
>
>发送&#x200B;**[!UICONTROL IMS:JWT当您需要刷新访问令牌以进行身份验证时，通过用户令牌生成+身份验证]**&#x200B;请求，因为该请求在24小时后过期。 有关说明，请参阅[配置AdobeAPI身份验证](../apis/configure-io-target-integration.md)。

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>在继续操作之前，获取[Recommendations邮递员集合](https://developers.adobetarget.com/api/recommendations/#section/Postman)。

## 使用Save Entities API创建和更新项目

要使用API而不是CSV产品源或在产品页面上触发[!DNL Target]请求来填充[!DNL Recommendations]产品数据库，请使用[保存实体API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities)。 此请求在单个[!DNL Target]环境中添加或更新项目。 语法为：

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

例如，“保存实体”可用于在达到某些阈值时更新项目（如库存或价格的阈值），以标记这些项目并防止建议它们。

1. 导航到&#x200B;**[!DNL Target]> [!UICONTROL 设置] > [!UICONTROL 主机] > [!UICONTROL 环境]**，以获取要添加或更新项目的[!DNL Target]环境ID。

   ![保存实体1](assets/SaveEntities01.png)

2. 验证`TENANT_ID`和`API_KEY`引用之前建立的邮递员环境变量。 请使用下图进行比较。 如有必要，请修改API请求中的标题和路径，使其与下图中的标题和路径相匹配。

   ![SaveEntities3](assets/SaveEntities03.png)

3. 在&#x200B;**Body**&#x200B;中，将JSON输入为&#x200B;**raw**&#x200B;代码。 不要忘记使用`environment`变量指定环境ID。 (在以下示例中，环境ID为6781。)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   以下是将具有烤面包机烤箱产品相关实体值的entity.id kit2001添加到环境6781的示例JSON。

   ```
      {
      "entities": [{
              "name": "Toaster Oven",
              "id": "kit2001",
              "environment": 6781,
              "categories": [
                  "housewares:appliances"
              ],
              "attributes": {
                  "inventory": 77,
                  "margin": 23,
                  "message": "crashing helicopter",
                  "pageUrl": "www.foobar.foo.com/helicopter.html",
                  "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
              }
          }]
      }
   ```

4. 单击&#x200B;**发送**。您应收到以下响应。

   ![SaveEntities5.png](assets/SaveEntities05.png)

可以缩放JSON对象以发送多个产品。 例如，此JSON指定两个实体。

```
    {
        "entities": [{
                "name": "Toaster Oven",
                "id": "kit2001",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 89,
                    "margin": 11,
                    "message": "Toaster Oven",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 102.5
                }
            },
            {
                "name": "Blender",
                "id": "kit2002",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 36,
                    "margin": 5,
                    "message": "Blender",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 54.5
                }
            }
        ]
    }
```

1. 现在轮到你了！ 使用&#x200B;**保存实体** API将以下项目添加到您的目录。 将上面的示例JSON作为起点。 （您需要扩展JSON以包含其他实体。）

   ![SaveEntities6.png](assets/SaveEntities06.png)

哎哟，看来最后两件东西不属于。 让我们使用&#x200B;**获取实体** API检查它们，如有必要，使用&#x200B;**删除实体** API删除它们。

## 使用Get Entity API获取项目详细信息

要检索现有项的详细信息，请使用[获取实体API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity)。 语法为：

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

一次只能检索单个实体的实体详细信息。 您可以使用“获取实体”来确认在目录中按预期进行了更新，或者以其他方式审核目录的内容。

1. 在API请求中，使用变量`entityId`指定实体ID。 以下示例将返回其entityId=kit2004的实体的详细信息。

   ![GetEntity1](assets/GetEntity1.png)

2. 验证`TENANT_ID`和`API_KEY`引用之前建立的邮递员环境变量。 请使用下图进行比较。 如有必要，请修改API请求中的标题和路径，使其与下图中的标题和路径相匹配。

   ![GetEntity2](assets/GetEntity2.png)

3. 发送请求。

   ![GetEntity3如](assets/GetEntity3.png)
上例所示，如果您收到错误，声明未找到实体，请验证您是否将请求提交到正确的 [!DNL Target] 环境。

   >[!NOTE]
   如果未明确指定环境，则“获取实体”将尝试仅从[默认环境](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html#section_4F8539B07C0C45E886E8525C344D5FB0)获取实体。 如果要从除默认环境之外的任何环境中提取，则必须指定环境ID。

4. 如有必要，请添加`environmentId`参数，然后重新发送请求。

   ![GetEntity4](assets/GetEntity4.png)

5. 发送另一个&#x200B;**获取实体**&#x200B;请求，此时检查其entityId=kit2005的实体。

   ![GetEntity5](assets/GetEntity5.png)

假定您决定需要从您的目录中删除这些实体。 我们使用&#x200B;**删除实体** API。

## 使用删除实体API删除项目

要从目录中删除项目，请使用[删除实体API](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities)。 语法为：

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
此API删除由您指定的ID引用的实体。
如果未提供实体ID，则删除给定环境中的所有实体。 如果未提供环境ID，则将从所有环境中删除实体。 小心使用！

1. 导航到&#x200B;**[!DNL Target]> [!UICONTROL 设置] > [!UICONTROL 主机] > [!UICONTROL 环境]**，以获取要从中删除项的[!DNL Target]环境ID。

   ![删除实体1](assets/SaveEntities01.png)

2. 在API请求中，使用语法`&ids=[comma-delimited-entity-ids]`(查询参数)指定要删除的实体的实体ID。 删除多个实体时，请使用逗号分隔这些ID。

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. 使用语法`&environment=[environmentId]`指定环境ID，否则将删除所有环境中的实体。

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. 验证`TENANT_ID`和`API_KEY`引用之前建立的邮递员环境变量。 请使用下图进行比较。 如有必要，请修改API请求中的标题和路径，使其与下图中的标题和路径相匹配。

   ![删除实体4](assets/DeleteEntities4.png)

5. 发送请求。

   ![删除实体5](assets/DeleteEntities5.png)

6. 使用&#x200B;**获取实体**&#x200B;验证结果，此时应指示找不到已删除的实体。

   ![删除实体6](assets/DeleteEntities6.png)

   ![删除实体6](assets/DeleteEntities7.png)

恭喜！ 您现在可以使用[!DNL Recommendations] API创建、更新、删除和获取有关目录中实体的详细信息。 在下一节中，您将学习如何管理自定义条件。

[下一个“管理自定义条件”>](manage-custom-criteria.md)
