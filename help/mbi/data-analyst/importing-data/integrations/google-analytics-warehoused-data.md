---
title: 預期的Google Analytics倉庫資料
description: 了解如何與Google Analytics的儲存資料互動。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 預期 [!DNL Google Analytics] 倉儲資料

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>有些資訊是經我們朋友許可，在 [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] 整合 [!DNL MBI] 利用 [!DNL Google Analytics] [核心報表API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>若要避免非預期或無意義的結果，請確認您使用的任何維度皆為 [與量度相容](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) 在 `Report Builder`.

單一表格 — 稱為 `report`  — 會在您的Data Warehouse中建立。

此表的架構將由您在設定過程中選擇的度量和Dimension以及另外兩列組成： `start-date` 和 `end-date`.

舉例來說，如果您在設定期間選取了下列量度和Dimension:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

表格如下所示。

| **欄名稱** | **說明** |
|-----|-----|
| `\_id` | 此欄是 `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] 唯一識別碼。 此列由建立 [!DNL MBI]. |
| `\_updated\_at` | 此欄包含上次更新資料列的時間。 此列由建立 [!DNL MBI]. |
| `start-date` | 列用於哪一天的標識。 |
| `end-date` | 列用於哪一天的標識。 |
| `month` | 所選維：工作階段月份，一個從01到12的兩位數整數。 |
| `users` | 所選量度：請求時段的用戶總數。 |

{style=&quot;table-layout:auto&quot;}

## 提醒：Google Analytics倉庫與即時整合之間的差異

主要優點在於儲存了一個整合([!DNL Google Analytics Warehoused])，而另一個不是([!DNL Google Analytics Live])。 若 [!DNL Google Analytics Warehoused]，這可讓您 [!DNL Google Analytics] 資料，讓您能夠 [!DNL Google Analytics] 及其他資料來源，以建立有洞察力的報表。

讓我們看看 [!DNL Google Analytics] 廣告促銷活動，以說明從操作觀點可以執行的作業。 假設第4季有多個不同名稱的廣告促銷活動。 行銷活動是特定行銷計畫的結果。 有了倉庫資料，我們可以建立新的欄，找出相關的促銷活動名稱並傳回的第4季計畫名稱 `Operation Dumbo`.

組合方面允許 [!DNL Google Analytics] 要連結到其他資料以進行分析的資料。 例如，取 `Total Time On Site By Ad Campaign` 資料來源 [!DNL Google Analytics] 加入 `Total Spent Per Campaign` 資料來源 [!DNL Facebook Ads] 來全面了解您的投入成本。

使用 [!DNL Google Analytics Live] 另一方面， [!DNL Google Analytics] 圖表就像沒有儲存在您的 [!DNL MBI] 資料倉庫。

## 相關：

* [連接 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
