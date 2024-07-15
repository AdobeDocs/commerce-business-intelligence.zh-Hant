---
title: 預期的Google Analytics倉儲資料
description: 瞭解如何與您的Google Analytics倉儲資料互動。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# 預期[!DNL Google Analytics Warehoused]資料

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

>[!NOTE]
>
>某些資訊已在朋友的許可下使用於[[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics)。

[!DNL Commerce Intelligence]中的[!DNL Google Analytics Warehoused]整合使用[!DNL Google Analytics] [核心報表API](https://developers.google.com/analytics/devguides/reporting/core/v3/)。

>[!NOTE]
>
>若要避免非預期或無意義的結果，請確認您使用的任何維度都與您在`Report Builder`中使用的一或多個量度](https://ga-dev-tools.google/dimensions-metrics-explorer/)相容[。

已在您的Data Warehouse中建立名為`report`的單一資料表。

此資料表的結構描述是由您在設定程式期間選取的量度和Dimension以及兩個其他資料行所組成： `start-date`和`end-date`。

例如，如果您在設定期間選取以下量度和Dimension：

* `Metrics`： `ga:users`
* `Dimensions`： `ga:month`

表格看起來會像下面的範例。

| **資料行名稱** | **描述** |
|-----|-----|
| `\_id` | 此資料行是`primary key`。 |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence]唯一識別碼。 此資料行由[!DNL Commerce Intelligence]建立。 |
| `\_updated\_at` | 此欄包含上次更新資料列的時間。 此資料行由[!DNL Commerce Intelligence]建立。 |
| `start-date` | 資料列適用日期的識別碼。 |
| `end-date` | 資料列適用日期的識別碼。 |
| `month` | 選取的維度：工作階段的月份，介於01到12之間的兩位數整數。 |
| `users` | 選取的量度：請求時段內的使用者總數。 |

{style="table-layout:auto"}

## [!DNL Google Analytics Warehoused]與[!DNL Live Integration]之間有何差異

主要區別在於一個整合已儲存([!DNL Google Analytics Warehoused])，而另一個則未儲存([!DNL Google Analytics Live])。 在[!DNL Google Analytics Warehoused]的情況下，這可讓您操控您的[!DNL Google Analytics]資料，並讓您結合[!DNL Google Analytics]和其他資料來源以建立深入分析的報告。

檢視[!DNL Google Analytics]個廣告行銷活動，以取得從操作觀點可以做些什麼的範例。 假設您在第四季有多個名稱不同的廣告行銷活動。 行銷活動是特定行銷活動的結果。 使用倉儲資料，您可以建立欄，找出有問題的行銷活動名稱，並傳回`Operation Dumbo`的第4季方案名稱。

組合方面可讓[!DNL Google Analytics]資料與其他資料結合，以進行分析。 例如，從[!DNL Google Analytics]取得`Total Time On Site By Ad Campaign`個資料，並與[!DNL Facebook Ads]的`Total Spent Per Campaign`個資料結合，以完整瞭解有多少參與導致您成本。

另一方面，透過[!DNL Google Analytics Live]整合，每個[!DNL Google Analytics]圖表都像是未儲存在您[!DNL Commerce Intelligence]Data Warehouse中的小型定址接收器。

## 相關：

* [正在連線 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
