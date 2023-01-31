---
title: 預期[!DNL Google ECommerce]資料
description: 了解與Google電子商務共用的資料類型。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 預期[!DNL Google ECommerce] 資料

在 [!DNL Google ECommerce] 帳戶已成功連接到 [!DNL MBI]，系統會開始將資料匯入名為的表格中 `ecommerce`. 此表將記錄每個事務的資料行。 這包括下列順序層級資料欄：

| 欄名稱 | 說明 |
|-----|-----|
| `\_id` | 此欄是主要索引鍵。 |
| `accountId` | 此欄包含與您的 [!DNL Google Analytics] 電子商務帳戶。 |
| `profileName` | 此欄包含您的 [!DNL Google Analytics] 設定檔名稱。 |
| `profileId` | 此欄包含您的 [!DNL Google Analytics] 設定檔ID。 |
| `socialNetwork` | 此欄包含社交網路的名稱(例如 [!DNL Facebook]，或 [!DNL YouTube]) |
| `campaign` | 此欄包含促銷活動名稱(例如 [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en))。 |
| `medium` | 此欄包含媒體名稱(例如 [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | 此列包含源名稱。 (例如， [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | 此欄包含關鍵字說明(例如 [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | 此欄包含訂單ID。 這將用於將反向連結資料加入您的訂單資料。 |
| `updated\_at` | 此欄包含上次更新資料列的時間。 |

{style=&quot;table-layout:auto&quot;}
