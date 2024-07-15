---
title: 預期[!DNL Google ECommerce]資料
description: 瞭解哪些型別的資料與Google E-commerce共用。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '158'
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
