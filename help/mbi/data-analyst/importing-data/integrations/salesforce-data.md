---
title: 預期Salesforce資料
description: 瞭解Salesforce資料中支援和不支援的物件。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 必須有[!DNL Salesforce]個資料

在[[!DNL Salesforce] 設定](../integrations/salesforce.md)完成之後，會在Data Warehouse中為每個可查詢的[物件](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) （名為`sf_/\{sobject-name}`）建立資料表。

>[!NOTE]
>
>每個表格的結構（欄）取決於物件中包含的欄位。

若要取得貴組織可用的物件清單，請參閱[!DNL Salesforce] [取得物件清單檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm)。 取得物件清單之後，請檢視[檔案的](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm)實體關聯圖(ERD)區段[!DNL Salesforce]，瞭解實體如何相互關聯。

## 不支援的物件

目前，[!DNL Salesforce]尚未在其API中公開下列物件：

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [什麼是外部物件？](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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

* [正在連線 [!DNL Salesforce]](../integrations/salesforce.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
