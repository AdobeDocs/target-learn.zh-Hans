---
title: 如何使用API管理Recommendations目录
description: 本教程的本部分将指导开发人员完成使用Adobe Target API在Recommendations目录中创建、更新、保存、获取和删除实体所需的步骤。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 8060b69b-e8e5-4fe7-895f-742410d8ed45
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 2%

---

# 管理 [!DNL Recommendations] 使用API的目录

此时，您已学会如何使用JWT身份验证流程生成访问令牌，以将Adobe Target管理员API与Adobe I/O结合使用。

您可以使用 [Recommendations API](https://developers.adobetarget.com/api/recommendations/) 添加、更新或删除推荐目录中的项目。 与Adobe Target的其他管理员API一样， [!DNL Recommendations] API需要身份验证。

>[!TIP]
>
>发送 **[!UICONTROL IMS:JWT通过用户令牌生成+身份验证]** 当您需要刷新访问令牌以进行身份验证时，会请求获取该令牌，因为该令牌在24小时后过期。 请参阅 [配置AdobeAPI身份验证](https://developer.adobe.com/target/before-administer/configure-authentication/){target=&quot;_blank&quot;}以获取相关说明。

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>继续之前，请获取 [RecommendationsPostman收藏集](https://developers.adobetarget.com/api/recommendations/#section/Postman).

## 使用保存实体API创建和更新项目

填充 [!DNL Recommendations] 使用API而不是CSV产品信息源的产品数据库，或 [!DNL Target] 在产品页面上触发的请求，请使用 [保存实体API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities). 此请求可在单个请求中添加或更新项目 [!DNL Target] 环境。 语法为：

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

例如，“保存实体”可用于在满足某些阈值（如库存阈值或价格阈值）时更新项目，以标记这些项目并阻止推荐这些项目。

1. 导航到 **[!DNL Target]> [!UICONTROL 设置] > [!UICONTROL 主机] > [!UICONTROL 环境]** 获取 [!DNL Target] 要在其中添加或更新项目的环境ID。

   ![SaveEntities1](assets/SaveEntities01.png)

2. 验证 `TENANT_ID` 和 `API_KEY` 引用之前已建立的Postman环境变量。 使用下图进行比较。 如有必要，请修改API请求中的标头和路径，以匹配下图中的标头和路径。

   ![SaveEntities3](assets/SaveEntities03.png)

3. 将JSON输入为 **原始** 代码 **正文**. 请不要忘记使用 `environment` 变量。 （在以下示例中，环境ID为6781。）

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   以下是将entity.id kit2001（包含烤面包机烤箱产品的关联实体值）添加到环境6781的示例JSON。

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

4. 单击&#x200B;**发送**。您应会收到以下响应。

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

1. 现在轮到你了！ 使用 **保存实体** 用于将以下项目添加到目录的API。 以上示例JSON作为起点。 （您需要扩展JSON以包含其他实体。）

   ![SaveEntities6.png](assets/SaveEntities06.png)

好象最后两件东西不属于。 让我们使用 **获取实体** API，如有必要，请使用 **删除实体** API。

## 使用获取实体API获取项目详细信息

要检索现有项目的详细信息，请使用 [获取实体API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity). 语法为：

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

一次只能检索单个实体的实体详细信息。 您可以使用获取实体来确认已在目录中按预期进行的更新，或以其他方式审核目录的内容。

1. 在API请求中，使用变量指定实体ID `entityId`. 以下示例将返回entityId=kit2004的实体的详细信息。

   ![GetEntity1](assets/GetEntity1.png)

2. 验证 `TENANT_ID` 和 `API_KEY` 引用之前已建立的Postman环境变量。 使用下图进行比较。 如有必要，请修改API请求中的标头和路径，以匹配下图中的标头和路径。

   ![GetEntity2](assets/GetEntity2.png)

3. 发送请求。

   ![GetEntity3](assets/GetEntity3.png)
如果您收到错误，指出未找到实体（如上面的示例所示），请确认您是否将请求提交到正确的 [!DNL Target] 环境。

   >[!NOTE]
   如果未明确指定任何环境，则获取实体会尝试从 [默认环境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=en) 仅。 如果您希望从默认环境以外的任何环境中提取数据，则必须指定环境ID。

4. 如有必要，请将 `environmentId` 参数，然后重新发送请求。

   ![GetEntity4](assets/GetEntity4.png)

5. 发送另一个 **获取实体** 请求，此时检查entityId=kit2005的实体。

   ![GetEntity5](assets/GetEntity5.png)

假定您决定需要从目录中删除这些实体。 让我们使用 **删除实体** API。

## 使用删除实体API删除项目

要从目录中删除项目，请使用 [删除实体API](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities). 语法为：

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
此API会删除由您指定的ID引用的实体。
如果未提供实体ID，则会删除给定环境中的所有实体。 如果未提供环境ID，则将从所有环境中删除实体。 小心使用！

1. 导航到 **[!DNL Target]> [!UICONTROL 设置] > [!UICONTROL 主机] > [!UICONTROL 环境]** 获取 [!DNL Target] 要从中删除项目的环境ID。

   ![DeleteEntities1](assets/SaveEntities01.png)

2. 在API请求中，使用语法指定要删除的实体的实体ID `&ids=[comma-delimited-entity-ids]` （查询参数）。 删除多个实体时，请使用逗号分隔这些ID。

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. 使用语法指定环境ID `&environment=[environmentId]`，否则，将删除所有环境中的实体。

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. 验证 `TENANT_ID` 和 `API_KEY` 引用之前已建立的Postman环境变量。 使用下图进行比较。 如有必要，请修改API请求中的标头和路径，以匹配下图中的标头和路径。

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. 发送请求。

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. 使用验证结果 **获取实体**，此时应该表示找不到已删除的实体。

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

恭喜！ 您现在可以使用 [!DNL Recommendations] 用于创建、更新、删除和获取有关目录中实体的详细信息的API。 在下一部分中，您将学习如何管理自定义标准。

[下一课程“管理自定义标准”>](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=&quot;_blank&quot;}
