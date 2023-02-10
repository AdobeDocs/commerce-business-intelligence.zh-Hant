---
title: 預期的Salesforce資料
description: 了解Salesforce資料中支援和不支援的物件。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 預期 [!DNL Salesforce] 資料

[在 [!DNL Salesforce] 安裝完成](../integrations/salesforce.md)，每個查詢的表 [物件](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm)  — 已命名 `sf_/\{sobject-name}`  — 會在您的資料倉庫中建立。

>[!NOTE]
>
>每個表的結構（列）取決於對象中包含的欄位。

若要取得組織可用的物件清單，請參閱 [!DNL Salesforce] [獲取對象清單文檔](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). 擁有對象清單後，請檢出 [實體關係圖(ERD)部分](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) of [!DNL Salesforce] 說明檔案，以了解實體彼此的關聯性。

## 不支援的對象

目前， [!DNL Salesforce] 目前未在其API中公開下列物件：

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [什麼是外部物件？](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## 相關：

* [連接 [!DNL Salesforce]](../integrations/salesforce.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
