---
title: 預期的Google Analytics倉儲資料
description: 瞭解如何與您的Google Analytics倉儲資料互動。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 預期 [!DNL Google Analytics Warehoused] 資料

>[!NOTE]
>
>需要 [管理員許可權](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>某些資訊是在您的朋友允許下使用於 [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] 整合 [!DNL Commerce Intelligence] 使用 [!DNL Google Analytics] [核心報表API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>若要避免非預期或無意義的結果，請確認您使用的任何維度皆為 [與一或多個量度相容](https://ga-dev-tools.google/dimensions-metrics-explorer/) 您會使用 `Report Builder`.

單一表格 — 稱為 `report`  — 在您的Data Warehouse中建立。

此資料表的綱要是由您在設定過程中選取的「測量結果和Dimension」以及另外兩個資料欄所組成： `start-date` 和 `end-date`.

例如，如果您在設定期間選取以下量度和Dimension：

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

表格看起來會像下面的範例。

| **欄名稱** | **說明** |
|-----|-----|
| `\_id` | 此欄是 `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] 唯一識別碼。 此欄的建立者： [!DNL Commerce Intelligence]. |
| `\_updated\_at` | 此欄包含上次更新資料列的時間。 此欄的建立者： [!DNL Commerce Intelligence]. |
| `start-date` | 資料列適用日期的識別碼。 |
| `end-date` | 資料列適用日期的識別碼。 |
| `month` | 選取的維度：工作階段的月份，介於01到12之間的兩位數整數。 |
| `users` | 選取的量度：請求時段內的使用者總數。 |

{style="table-layout:auto"}

## 兩者之間有何差異？ [!DNL Google Analytics Warehoused] 和 [!DNL Live Integration]

主要區別在於儲存了一項整合([!DNL Google Analytics Warehoused])而其他不是([!DNL Google Analytics Live])。 在下列情況下 [!DNL Google Analytics Warehoused]，這允許操控您的 [!DNL Google Analytics] 資料並提供您合併 [!DNL Google Analytics] 和其他資料來源，以建立具洞察力的報表。

檢視 [!DNL Google Analytics] 廣告行銷活動是從操作角度可以做些什麼的範例。 假設您在第四季有多個名稱不同的廣告行銷活動。 行銷活動是特定行銷活動的結果。 使用倉儲資料，您可以建立欄，找出有問題的行銷活動名稱，並傳回的第4季方案名稱 `Operation Dumbo`.

組合外觀允許 [!DNL Google Analytics] 要與其他資料結合以進行分析的資料。 例如， take `Total Time On Site By Ad Campaign` 資料來源 [!DNL Google Analytics] 並加入對抗的行列 `Total Spent Per Campaign` 資料來源 [!DNL Facebook Ads] 以全面瞭解參與成本是多少。

使用 [!DNL Google Analytics Live] 另一方面，整合會 [!DNL Google Analytics] 圖表就像是未儲存在中的小型筒倉 [!DNL Commerce Intelligence] Data Warehouse。

## 相關：

* [正在連線 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
