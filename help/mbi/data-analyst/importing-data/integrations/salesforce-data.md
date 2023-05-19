---
title: 預期的Salesforce資料
description: 瞭解Salesforce資料中支援的和不受支援的對象。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 預期 [!DNL Salesforce] 資料

在 [[!DNL Salesforce] 設定](../integrations/salesforce.md) 是完整的，每個可查詢的表 [對象](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm)  — 命名 `sf_/\{sobject-name}`  — 在Data Warehouse中建立。

>[!NOTE]
>
>每個表的結構（列）取決於對象中包含的欄位。

要獲取組織可用對象清單，請參閱 [!DNL Salesforce] [獲取對象清單文檔](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm)。 擁有對象清單後，請簽出 [實體關係圖(ERD)部分](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) 共 [!DNL Salesforce] 查看實體之間的關係。

## 不支援的對象

目前， [!DNL Salesforce] 當前不在其API中公開以下對象：

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [什麼是外部對象？](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
