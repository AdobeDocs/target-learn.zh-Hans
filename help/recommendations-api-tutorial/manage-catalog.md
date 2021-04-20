---
title: 如何使用API管理Recommendations目录
description: 本教程的这一部分将指导开发人员完成使用Adobe Target API在Recommendations目录中创建、更新、保存、获取和删除实体所需的步骤。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---


# 使用API管理[!DNL Recommendations]目录

此时，您已学习了如何使用JWT身份验证流生成访问令牌，以将Adobe Target Admin API与Adobe I/O一起使用。

您可以使用[Recommendations API](https://developers.adobetarget.com/api/recommendations/)添加、更新或删除推荐目录中的项目。 与Adobe Target Admin API的其余部分一样，[!DNL Recommendations] API需要身份验证。

>[!TIP]
>
>发送&#x200B;**[!UICONTROL IMS:JWT在需要刷新访问令牌以进行身份验证时通过用户令牌]**&#x200B;请求生成+身份验证，因为该请求在24小时后过期。 有关说明，请参阅[配置Adobe API身份验证](../apis/configure-io-target-integration.md)。

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>在继续操作之前，获取[Recommendations Postman集合](https://developers.adobetarget.com/api/recommendations/#section/Postman)。

## 使用Save Entities API创建和更新项目

要使用API而不是CSV产品源或在产品页面上触发的[请求填充您的[!DNL Recommendations]产品数据库，请使用[!DNL Target]保存实体API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities)。 此请求在单个[!DNL Target]环境中添加或更新项目。 语法为：

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

例如，“保存实体”可用于在达到某些阈值（如库存阈值或价格阈值）时更新物料，以便标记这些物料并防止建议它们。

1. 导航到&#x200B;**[!DNL Target]> [!UICONTROL Setup] > [!UICONTROL  Hosts] > [!UICONTROL 环境]**，以获取要添加或更新项目的[!DNL Target]环境ID。

   ![SaveEntities1](assets/SaveEntities01.png)

2. 验证`TENANT_ID`和`API_KEY`引用了之前建立的Postman环境变量。 请使用下图进行比较。 如有必要，请修改API请求中的标头和路径，以与下图像中的标头和路径相匹配。

   ![SaveEntities3](assets/SaveEntities03.png)

3. 在&#x200B;**Body**&#x200B;中，将您的JSON输入为&#x200B;**raw**&#x200B;代码。 不要忘记使用`environment`变量指定环境ID。 (在以下示例中，环境ID为6781。)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   以下是向环境 6781中添加具有烤面包机烤箱产品关联实体值的entity.id kit2001的示例JSON。

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

4. 单击&#x200B;**发送**。您应收到以下答复。

   ![SaveEntities6.png](assets/SaveEntities05.png)

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

1. 现在轮到你了！ 使用&#x200B;**保存实体** API将以下项目添加到目录中。 将上面的示例JSON作为起点。 （您需要扩展JSON以包含其他实体。）

   ![SaveEntities6.png](assets/SaveEntities06.png)

哦，看来最后两件东西不属于。 让我们使用&#x200B;**获取实体** API检查它们，如有必要，使用&#x200B;**删除实体** API删除它们。

## 使用Get Entity API获取项目详细信息

要检索现有项的详细信息，请使用[获取实体API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity)。 语法为：

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

一次只能检索单个实体的实体详细信息。 您可以使用“获取实体”确认在目录中按预期进行了更新，或以其他方式审核目录的内容。

1. 在API请求中，使用变量`entityId`指定实体ID。 下面的示例将返回其entityId=kit2004的实体的详细信息。

   ![GetEntity1](assets/GetEntity1.png)

2. 验证`TENANT_ID`和`API_KEY`引用了之前建立的Postman环境变量。 请使用下图进行比较。 如有必要，请修改API请求中的标头和路径，以与下图像中的标头和路径相匹配。

   ![GetEntity2](assets/GetEntity2.png)

3. 发送请求。

   ![GetEntity3如](assets/GetEntity3.png)
上例所示，如果您收到错误，声明未找到实体，请验证您是否将请求提交到正确的 [!DNL Target] 环境。

   >[!NOTE]
   如果未显式指定环境，则“获取实体”将尝试仅从[默认环境](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html#section_4F8539B07C0C45E886E8525C344D5FB0)获取实体。 如果您希望从除默认环境之外的任何环境中提取，则必须指定环境ID。

4. 如有必要，添加`environmentId`参数，然后重新发送请求。

   ![GetEntity4](assets/GetEntity4.png)

5. 发送另一个&#x200B;**获取实体**&#x200B;请求，此时检查其entityId=kit2005的实体。

   ![GetEntity5](assets/GetEntity5.png)

假设您决定需要从您的目录中删除这些实体。 让我们使用&#x200B;**删除实体** API。

## 使用删除实体API删除项目

要从目录中删除项目，请使用[删除实体API](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities)。 语法为：

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
此API将删除由您指定的ID引用的实体。
如果未提供实体ID，则删除给定环境中的所有实体。 如果未提供环境ID，则将从所有环境中删除实体。 小心使用！

1. 导航到&#x200B;**[!DNL Target]> [!UICONTROL Setup] > [!UICONTROL  Hosts] > [!UICONTROL 环境]** ，以获取要从中删除项目的[!DNL Target]环境ID。

   ![DeleteEntities1](assets/SaveEntities01.png)

2. 在API请求中，使用语法`&ids=[comma-delimited-entity-ids]`(查询参数)指定要删除的实体的实体ID。 删除多个实体时，请使用逗号分隔这些ID。

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. 使用语法`&environment=[environmentId]`指定环境ID，否则将删除所有环境中的实体。

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. 验证`TENANT_ID`和`API_KEY`引用了之前建立的Postman环境变量。 请使用下图进行比较。 如有必要，请修改API请求中的标头和路径，以与下图像中的标头和路径相匹配。

   ![删除实体4](assets/DeleteEntities4.png)

5. 发送请求。

   ![删除实体5](assets/DeleteEntities5.png)

6. 使用&#x200B;**获取实体**&#x200B;验证结果，此时应指示找不到已删除的实体。

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

恭喜！ 您现在可以使用[!DNL Recommendations] API创建、更新、删除和获取有关目录中实体的详细信息。 在下一节中，您将学习如何管理自定义标准。

[下一个“管理自定义条件”>](manage-custom-criteria.md)
