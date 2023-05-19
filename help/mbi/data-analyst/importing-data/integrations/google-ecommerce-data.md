---
title: 預期[!DNL Google ECommerce]資料
description: 瞭解與Google電子商務共用的資料類型。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 預期[!DNL Google ECommerce] 資料

在 [!DNL Google ECommerce] 帳戶已成功連接到 [!DNL Commerce Intelligence]，系統將開始將資料導入標題為 `ecommerce`。 此表記錄每個事務的資料行。 這包括以下順序級資料列：

| 列名 | 說明 |
|-----|-----|
| `\_id` | 此列是主鍵。 |
| `accountId` | 此列包含與您的 [!DNL Google Analytics] 電子商務帳戶。 |
| `profileName` | 此列包含 [!DNL Google Analytics] 配置檔案名稱。 |
| `profileId` | 此列包含 [!DNL Google Analytics] 配置檔案ID。 |
| `socialNetwork` | 此列包含社交網路的名稱(例如， [!DNL Facebook]或 [!DNL YouTube]) |
| `campaign` | 此列包含市場活動名稱(例如， [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en))。 |
| `medium` | 此列包含媒體名稱(例如， [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | 此列包含源名稱。 (例如， [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | 此列包含關鍵字說明(例如， [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | 此列包含順序ID。 這用於將推薦資料加回您的訂單資料。 |
| `updated\_at` | 此列包含上次更新資料行的時間。 |

{style="table-layout:auto"}
