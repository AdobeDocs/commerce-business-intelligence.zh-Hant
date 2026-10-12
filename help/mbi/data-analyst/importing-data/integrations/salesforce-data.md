---
title: 預期Salesforce資料
description: 瞭解Salesforce資料中支援和不支援的物件。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/eBX3Y0luu60A8PSAF43H6O3fsYjJnSWzyIybSOcSELE'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%
---
# 必須有[!DNL Salesforce]個資料

在[[!DNL Salesforce] 設定](../integrations/salesforce.md)完成之後，會在Data Warehouse中為每個可查詢的[物件](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) （名為`sf_/\{sobject-name}`）建立資料表。

>[!NOTE]
>
>每個表格的結構（欄）取決於物件中包含的欄位。

若要取得貴組織可用的物件清單，請參閱[!DNL Salesforce] [取得物件清單檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm)。 取得物件清單之後，請檢視[!DNL Salesforce]檔案的[實體關聯圖(ERD)區段](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm)，瞭解實體如何相互關聯。

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
* [重新驗證整合](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations)
