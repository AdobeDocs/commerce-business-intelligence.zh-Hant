---
title: 預期[!DNL Google ECommerce]資料
description: 瞭解哪些型別的資料與Google E-commerce共用。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 158
ht-degree: 0%

---

# 必須有[!DNL Google ECommerce]個資料

在您的[!DNL Google ECommerce]帳戶成功連線到[!DNL Commerce Intelligence]之後，系統就會開始將資料匯入標題為`ecommerce`的資料表。 此表格記錄每個交易的資料列。 這包括下列順序層級資料欄：

| 欄名稱 | 說明 |
|-----|-----|
| `\_id` | 此欄是主索引鍵。 |
| `accountId` | 此欄包含與您的[!DNL Google Analytics]電子商務帳戶相關聯的帳戶識別碼。 |
| `profileName` | 此欄包含您的[!DNL Google Analytics]設定檔名稱。 |
| `profileId` | 此欄包含您的[!DNL Google Analytics]設定檔識別碼。 |
| `socialNetwork` | 此欄包含社交網路的名稱（例如，[!DNL Facebook]或[!DNL YouTube]） |
| `campaign` | 此欄包含行銷活動名稱（例如，[`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)）。 |
| `medium` | 此資料行包含媒體名稱（例如，[`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `source` | 此欄包含來源名稱。 （例如，[`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `keyword` | 此欄包含關鍵字描述（例如，[`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `transactionId` | 此欄包含訂單ID。 這可用來將轉介資料聯結回您的訂單資料。 |
| `updated\_at` | 此欄包含上次更新資料列的時間。 |

{style="table-layout:auto"}
