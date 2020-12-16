---
title: 为Adobe TargetAPI配置身份验证
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target·Recommendations包含一组专用的API，允许您管理推荐产品和／或内容目录；管理推荐算法和活动;并在JSON、HTML或XML对象中提供推荐，以便在Web、移动、电子邮件、物联网和其他渠道中显示。
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 624172d4bc4bc2431ad8af0956c93d3bcc0b9870
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 2%

---


# 为Adobe TargetAPI配置身份验证

Adobe Target管理API（包括[!DNL Recommendations]管理API）通过身份验证进行保护，以确保只有授权用户才能使用它们访问Adobe Target。 使用[Adobe开发者控制台](https://console.adobe.io/)管理所有Adobe Experience Cloud解决方案的此身份验证，包括[!DNL Target]。

本课程将介绍生成与Adobe TargetAPI成功交互所需的身份验证令牌所需的初步步骤。 在接下来的几节中，您将：

1. 在Adobe开发人员控制台中创建项目（以前称为集成）。
2. 将项目详细信息导出到邮递员。
3. 生成承载访问令牌。
4. 测试承载访问令牌。

## 先决条件

| 资源 | 详细信息 |
| --- | --- |
| 邮递员 | 要成功完成这些步骤，请获取操作系统的[邮递员应用程序](https://www.postman.com/downloads/)。 Postman Basic免费创建帐户。 虽然一般来说，使用Adobe TargetAPI并非必需，但邮递员使API工作流更加简单，而Adobe Target公司提供多个邮递员集合来帮助执行其API并了解它们的操作方式。 本教程的其余部分假定是邮递员的工作知识。 要获得帮助，请参考[邮递员文档](https://learning.getpostman.com/)。 |
| 引用 | 在本教程的其余部分中，假定您熟悉以下资源：<UL><li>[Adobe I/O·吉图布](https://github.com/adobeio)</li><li>[目标Adobe I/O文档](https://developers.adobetarget.com/api/#introduction)</li><li>[RecommendationsAPI文档](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## 创建Adobe I/O项目

在此部分，您将访问Adobe开发者控制台并为[!DNL Adobe Target]创建一个项目。 有关详细信息，请参考项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md)的[文档。

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. 在[Adobe Admin Console](https://adminconsole.adobe.com/)中，确保您的Adobe用户帐户已被授予[产品管理员](https://helpx.adobe.com/enterprise/using/admin-roles.html)和[开发人员](https://helpx.adobe.com/enterprise/using/manage-developers.html)级别访问权限。[!DNL Target]

2. 在[Adobe开发者控制台](https://console.adobe.io/)中，选择要为其创建此集成的Experience Cloud组织。 (注意，您可能只能访问单个Experience Cloud组织。)

   ![configure-io-目标-createproject2.png](assets/configure-io-target-createproject2.png)

3. 单击&#x200B;**[!UICONTROL 新建项目]**。

   ![configure-io-目标-createproject3.png](assets/configure-io-target-createproject3.png)

4. 单击&#x200B;**[!UICONTROL 添加API]**&#x200B;向项目添加REST API，以访问Adobe服务和产品。

   ![添加API](assets/configure-io-target-createproject4.png)

5. 选择&#x200B;**[!DNL Adobe Target]**&#x200B;作为要集成的Adobe服务。 单击显示的&#x200B;**[!UICONTROL Next]**&#x200B;按钮。

   ![configure-io-目标-createproject5](assets/configure-io-target-createproject5.png)

6. 选择一个选项，以将公钥和私钥与您为目标创建的服务帐户集成关联。 对于本教程，请选择&#x200B;**[!UICONTROL 选项1:生成密钥对]**&#x200B;并单击“生成密钥对&#x200B;]**”。**[!UICONTROL 
   ![configure-io-目标-createproject6](assets/configure-io-target-createproject6.png)

7. 注意结果！ 按照说明，记下自动下载的配置文件(`config`)，它包含您的私钥。 单击&#x200B;**[!UICONTROL 下一步]**。
   ![configure-io-目标-createproject7](assets/configure-io-target-createproject7.png)
8. 在文件系统中，验证`config`的位置，这是在上一步中创建的压缩配置文件。 同样，此`config`文件包含您以后需要的私钥。 文件系统中的确切位置可能与此处显示的位置不同。
   ![configure-io-目标-createproject8](assets/configure-io-target-createproject8.png)
9. 返回到Adobe开发者控制台，选择与您使用[!DNL Recommendations]的属性对应的[产品用户档案](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html)。 (如果您未使用属性，请选择“默认工作区”(Default Workspace)选项。) 单击&#x200B;**[!UICONTROL 保存配置的API]**。
   ![configure-io-目标-createproject9](assets/configure-io-target-createproject9.png)

10. 单击&#x200B;**[!UICONTROL 创建集成]**。 您应会收到一条临时消息，指明您的API已成功配置。

11. 最后，将项目重命名为比原始`Project 1`更有意义的名称。 为此，请使用如图所示的导航路径导航到项目，单击&#x200B;**[!UICONTROL 编辑项目]**&#x200B;以访问**[!UICONTROL 编辑项目]模式，然后重命名项目。

![configure-io-目标-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>在本教程中，我们将项目命名为“目标集成”。 如果您预计将项目用于的对象不仅仅是Adobe Target，您可能希望相应地命名它。 例如，您可以选择将其命名为“AdobeAPI”或“Experience CloudAPI”，因为它可以与Adobe Experience Cloud的其他解决方案一起使用。

## 导出项目详细信息

现在，您有了可用于访问[!DNL Target]的Adobe项目，您需要确保发送该项目的详细信息以及AdobeAPI请求。 需要这些详细信息才能与多个AdobeAPI交互，包括多个[!DNL Target] API。 例如，集成详细信息包括[!DNL Target]管理员API所需的授权和身份验证信息。 因此，要将API与Postman一起使用，您需要将这些详细信息导入Postman。

在Postman中可以通过多种方式指定项目的详细信息，但在本节中，我们充分利用了一些预建功能和集合。 首先（在本部分），您将将集成的详细信息导出到邮递员环境。 接下来（在下一节中），您将生成一个承载访问令牌，以授予您对必要的Adobe资源的访问权限。

>[!NOTE]
>
>有关适用于任何Experience Cloud解决方案（包括[!DNL Target]）的视频说明，请参阅[将邮递员与Experience PlatformAPI结合使用](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html)。 以下各节与[!DNL Target] API相关：
>
> 1. 将Adobe I/O集成详细信息导出到邮递员
> 2. 使用邮递员生成访问令牌

>
> 
下面还提供了这些步骤。

1. 仍位于[Adobe开发者控制台](https://console.adobe.io/)中，导航到视图新项目的&#x200B;**[!UICONTROL 服务帐户(JWT)]**&#x200B;凭据。 请使用左侧导航或&#x200B;**[!UICONTROL 凭据]**部分，如所示。
   ![JWT1在](assets/configure-io-target-jwt1.png)
凭 **[!UICONTROL 据详细信息]**&#x200B;中，请注意，您可以视图 **您的公钥**、 **客户端ID**，以及与您的服务帐户相关的其他信息。
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. 单击导航到有关&#x200B;**[!UICONTROL Adobe Target]** API的信息。 请使用左侧导航或&#x200B;**[!UICONTROL 已连接的产品和服务]**部分，如所示。
   ![JWT2](assets/configure-io-target-jwt2.png)
3. 单击&#x200B;**[!UICONTROL Download for Postman]** > **[!UICONTROL 服务帐户(JWT)]**以创建JSON文件，捕获Postman环境的身份验证信息。
   ![JWT3](assets/configure-io-target-jwt3.png)
请注意文件系统中的JSON文件。
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. 在Postman中，单击齿轮图标以管理环境，然后单击&#x200B;**导入**以导入JSON文件(环境)。
   ![JWT4](assets/configure-io-target-jwt4.png)
5. 选择文件，然后单击&#x200B;**打开**。
   ![JWT5](assets/configure-io-target-jwt5.png)
6. 在邮递员&#x200B;**管理环境**模式中，单击新导入的环境的名称以检查它。 (您的环境名称可能与此处显示的名称不同。 根据需要编辑名称。 它不一定需要与Adobe项目的名称匹配。)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. 注意`CLIENT_SECRET`和`API_KEY`（连同其他变量）会预先填充其值，这些值取自Adobe开发者控制台中定义的集成。 (Postman `CLIENT_SECRET`变量应与开发人员控制台中显示的`CLIENT SECRET`Adobe凭据匹配，而Postman中的`API_KEY`也应与开发人员控制台中的`CLIENT ID`匹配。) 相反，注`PRIVATE_KEY`、`JWT_TOKEN`和`ACCESS_TOKEN`为空。 让我们通过提供`PRIVATE_KEY`值进行开始。
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**惊喜！**
   >
   >快测验！ 你记得你的私钥在哪吗？
   >没错，它位于之前从Adobe开发者控制台下载的`config`文件中！

8. 从文件系统打开`config`文件，然后打开`private`密钥文件。
   ![JWT8](assets/configure-io-target-jwt8.png)
9. 选择并复制`private`密钥文件的整个内容。
   ![JWT9](assets/configure-io-target-jwt9.png)
10. 在Postman中，将私钥值粘贴到&#x200B;**INITIAL VALUE**&#x200B;和&#x200B;**CURRENT VALUE**字段中。
   ![JWT10](assets/configure-io-target-jwt10.png)
11. 单击&#x200B;**[!UICONTROL 更新]**&#x200B;并关闭环境模式。


## 生成承载访问令牌

在本节中，您将生成您的持牌访问令牌，这是验证您与Adobe TargetAPI的交互所必需的。 要生成载体访问令牌，您需要将集成详细信息（在前几节中建立）发送到[AdobeIdentity Management服务(IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md)。 有几种不同的方法可以实现此目的，但在本教程中，我们将构建一个定制的IMS APIPOST请求。 开玩笑吧。 在本教程中，我们将利用一个包含预建IMS调用的Postman集合，该调用使流程更直接、更简单。 导入集合后，您可以在需要时重用它，为Adobe Target以及其他AdobeAPI生成新令牌。

1. 导航到[AdobeIdentity Management服务API示例调用](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)。
   ![token1](assets/configure-io-target-generatetoken1.png)
2. 单击&#x200B;**Adobe I/O访问令牌生成邮递员集合**。
   ![token2](assets/configure-io-target-generatetoken2.png)
3. 单击&#x200B;**Raw**，然后将生成的JSON复制到剪贴板，以获取此集合的原始JSON。 （您也可以将原始JSON另存为。json文件。）
   ![token3](assets/configure-io-target-generatetoken3.png)
4. 在Postman中，通过粘贴并从剪贴板提交原始JSON来导入集合。 （您也可以上传您保存的。json文件。） 单击&#x200B;**继续**。
   ![token4](assets/configure-io-target-generatetoken4.png)
5. 选择&#x200B;**[!UICONTROL IMS:JWT在Adobe I/O访问令牌生成邮递员集合中通过用户令牌]**&#x200B;生成+身份验证请求，确保您的环境已被选中，然后单击&#x200B;**发送**&#x200B;以生成令牌。

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >此不记名访问令牌的有效期为24小时。 需要生成新令牌时，请再次发送请求。

6. 再次打开“管理环境”模式，然后选择您的环境。
   ![token6](assets/configure-io-target-jwt11.png)
7. 请注意，`ACCESS_TOKEN`和`JWT_TOKEN`值现已填充。
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>问：我是否必须使用Adobe I/O访问令牌生成邮递员集合来生成JSON Web令牌(JWT)和承载访问令牌?
>
>答：不！ Adobe I/O访问令牌世代邮递员集合可方便地在邮递员中生成JWT和无记名访问令牌。 或者，您也可以使用Adobe开发者控制台中的功能手动生成承载访问令牌。

## 测试承载访问令牌

在本练习中，您将通过发送从[!DNL Target]帐户检索列表的API请求来使用新的持有访问令牌。 成功的响应表明您的Adobe项目和身份验证正按预期运行以使用API。

1. 导入[Adobe Target管理API邮递员集合](https://developers.adobetarget.com/api/#admin-postman-collection)。 按照所有提示操作，直到集合导入邮递员。
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. 展开集合，并记下&#x200B;**[!UICONTROL 列表活动]**请求。
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. 请注意，`{{access_token}}`等变量最初未解析。 您可以通过几种不同的方式解决此问题，例如，您可以定义一个名为`{{access_token}}`的新集合变量，但在本教程中，您将更改API请求以利用您之前使用的邮递员环境。 这将使环境能够继续作为单一、一致的整合所有AdobeAPI中通用的变量。
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. 键入以将`{{access_token}}`替换为`{{ACCESS_TOKEN}}`。
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. 键入以将`{{api_key}}`替换为`{{API_KEY}}`。
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. 键入以将`{{tenant}}`替换为`{{TENANT_ID}}`。 注意`{{TENANT_ID}}`尚未被识别。
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. 打开“管理环境”模式，然后选择您的环境。
   ![JWT11](assets/configure-io-target-jwt11.png)
1. 键入以添加新的`{{TENANT_ID}}`环境变量。 将租户ID值复制并粘贴到新`TENANT_ID`环境变量的&#x200B;**初始值**&#x200B;和&#x200B;**当前值**&#x200B;字段中。

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >租户ID与您的[!DNL Target] `clientcode`不同。 登录到[!DNL Target]时，URL中存在租户ID。 要获取您的租户ID，请登录[!DNL Adobe Experience Cloud]，打开[!DNL Target]，然后单击[!DNL Target]卡。 请按照URL子域中的说明使用租户ID值。
   >
   >例如，如果您登录Adobe Target时的URL为
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >您的租户ID为“mycompany”。

1. 在确保选择了正确的环境后，发送您的请求。 您应收到包含列表活动的响应。
   ![testtoken6](assets/configure-io-target-testtoken6.png)

恭喜！ 现在您已验证Adobe身份验证，您可以使用它与Adobe TargetAPI(以及其他AdobeAPI)交互。 例如，您可以[使用RecommendationsAPI](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html)创建或管理推荐。
