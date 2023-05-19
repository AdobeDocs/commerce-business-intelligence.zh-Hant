---
title: 預期Google Analytics倉庫資料
description: 學習與Google Analytics倉庫資料交互。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 預期 [!DNL Google Analytics Warehoused] 資料

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

>[!NOTE]
>
>某些資訊是在您朋友的許可下使用的 [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics)。

[!DNL Google Analytics Warehoused] 整合 [!DNL Commerce Intelligence] 使用 [!DNL Google Analytics] [核心報告API](https://developers.google.com/analytics/devguides/reporting/core/v3/)。

>[!NOTE]
>
>要避免意外或無意義結果，請確認您使用的任何維 [與一個或多個度量相容](https://ga-dev-tools.google/dimensions-metrics-explorer/) 在 `Report Builder`。

單個表 — 稱為 `report`  — 在Data Warehouse中建立。

此表的架構由您在設定過程中選擇的度量和Dimension以及兩列組成： `start-date` 和 `end-date`。

例如，在設定期間，您選擇了以下度量和Dimension:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

該表看起來與下面的示例類似。

| **列名** | **說明** |
|-----|-----|
| `\_id` | 此列是 `primary key`。 |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] 唯一標識符。 此列由 [!DNL Commerce Intelligence]。 |
| `\_updated\_at` | 此列包含上次更新資料行的時間。 此列由 [!DNL Commerce Intelligence]。 |
| `start-date` | 行的日期標識。 |
| `end-date` | 行的日期標識。 |
| `month` | 所選維：會話的月份，一個01到12的兩位整數。 |
| `users` | 所選度量：請求的時間段的用戶總數。 |

{style="table-layout:auto"}

## 有什麼區別 [!DNL Google Analytics Warehoused] 和 [!DNL Live Integration]

主要區別在於儲存了一個整合([!DNL Google Analytics Warehoused])，另一個不是([!DNL Google Analytics Live])。 在 [!DNL Google Analytics Warehoused]，這允許操縱 [!DNL Google Analytics] 資料，讓你能夠 [!DNL Google Analytics] 以及其他資料來源，以建立有洞察力的報告。

看 [!DNL Google Analytics] 以操縱為例，說明可以做什麼。 假設您有多個不同名稱的第4季度廣告活動。 這些活動是特定營銷計畫的結果。 使用倉庫資料，您可以建立一個列，該列查找有關的市場活動名稱並返回第4季度的方案名稱 `Operation Dumbo`。

組合方面允許 [!DNL Google Analytics] 要與其他資料聯接以便進行分析的資料。 例如， `Total Time On Site By Ad Campaign` 資料 [!DNL Google Analytics] 加入它 `Total Spent Per Campaign` 資料 [!DNL Facebook Ads] 全面瞭解你投入的成本。

使用 [!DNL Google Analytics Live] 另一方面， [!DNL Google Analytics] 圖表就像一個小思洛儲存器，它不儲存在 [!DNL Commerce Intelligence] Data Warehouse。

## 相關：

* [連接 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
