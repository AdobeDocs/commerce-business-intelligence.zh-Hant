---
title: 建立和使用Data Warehouse檢視
description: 了解如何通過修改現有表來建立新倉庫儲存的表，或通過使用SQL將多個表連接或合併在一起。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# 使用Data Warehouse檢視

本檔案概述 `Data Warehouse Views` 瀏覽至 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. 以下說明其作用以及如何建立新檢視，以及如何使用範例 `Data Warehouse Views` 整合 [!DNL Facebook] 和 [!DNL AdWords] 花費資料。

## 一般用途

此 `Data Warehouse Views` 特徵是一種通過修改現有表來建立新倉庫儲存表的方法，或通過使用SQL將多個表連接或合併在一起。 一次a `Data Warehouse View` 已由更新週期建立和處理，則會在您的Data Warehouse中填入為 `Data Warehouse Views` 下拉式清單，如下所示：

![](../../assets/Data_Warehouse.png)

從這裡，您的新檢視的運作方式與任何其他表格相同，讓您能夠建立新的計算欄，或在其上方建立量度和報表。

`Data Warehouse Views` 主要用於將多個相似但不同的表合併在一起，以便所有報告都可以建立在單個新表上。 一些常見範例包括整合來自舊版資料庫和即時資料庫的表格，以結合歷史和目前資料，或將多個廣告來源(例如Facebook和AdWords)合併為單數 `Consolidated ad spend` 表格。

如果您熟悉SQL，這兩個整合示例都利用 `UNION` 函式，但在建立新視圖時，可以使用任何PostgreSQL語法和函式。

## 建立和管理Data Warehouse檢視

新增 `Data Warehouse Views` 可以建立，而且可以借由導覽至 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**，如下所示：

![](../../assets/Data_Warehouse_Views.png)

您可以在此處依照下列範例指示建立新檢視：

1. 如果觀察現有視圖，請按一下 **[!UICONTROL New Data Warehouse View]** 開啟空白查詢窗口。 如果已開啟空白查詢窗口，請繼續執行下一步。
1. 在 `View Name` 欄位。 此處提供的名稱將決定Data Warehouse中檢視的顯示名稱。 `View names` 限於小寫字母、數字和底線(_)。 其他字元都禁止使用。
1. 在標題為的窗口中輸入查詢 `Select Query`，使用標準PostgreSQL語法。
   >[!NOTE]
   >
   >您的查詢必須引用特定列名。 使用 `*`不允許使用字元來選擇所有列。

1. 完成後，按一下 **[!UICONTROL Save]** 來儲存檢視。 請注意，您的檢視會暫時 `Pending` 狀態，直到下一個完整更新週期處理完畢，此時狀態將變更為 `Active`. 由更新處理之後，您的檢視就可供報表使用。

請務必提及，儲存後，用來產生 `Data Warehouse View` 無法編輯。 如果由於某些原因，您需要調整 `Data Warehouse View`，您將需要建立新檢視，並手動將任何計算欄、量度或報表從原始檢視移轉到新檢視。 完成移轉後，您就可以安全地刪除原始檢視。 因為 `Data Warehouse Views` 不可編輯，強烈建議您使用 `SQL Report Builder` 將查詢儲存為「Data Warehouse檢視」之前。

## 範例： [!DNL Facebook] 和 [!DNL Google AdWords] 資料

讓我們更仔細地看一下本文前面提到的一個例子：合併 [!DNL Facebook] 和 [!DNL AdWords] 將資料花費到新的匯總廣告表格中。 最常見的情況是需要合併兩個表，示例資料集如下：

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | ee | 60 | 2017-05-05 00:00:00 | 2000年 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | ee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | ff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | dd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aa | 40 | 2017-05-22 00:00:00 | 2000年 | 7 |
| 4 | aa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | cc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

若要建立包含兩者的單一廣告支出表格 [!DNL Facebook] 和 [!DNL AdWords] 促銷活動，我們需要編寫SQL查詢並使用 `UNION ALL` 函式。 A `UNION ALL` 語句通常用於組合多個不同的SQL查詢，同時將每個查詢的結果附加到單個輸出。

以下是 `UNION` 值得一提的語句，如PostgreSQL中所述 [檔案](https://www.postgresql.org/docs/8.3/queries-union.html):

* 所有查詢都必須返回相同數目的列
* 對應的列必須具有相同的資料類型

執行 `UNION` 或 `UNION ALL` 語句，則最終輸出中的列名將反映第一個查詢中的列的命名。

在大多數情況下，整合 [!DNL Facebook] 和 [!DNL Google AdWords] 將資料花費到 `Data Warehouse View` 將需要建立一個包含7列的表，其查詢如下所示：

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

以上幾項要點：

* 為了清楚起見，所有欄會設為上方的別名，以便所有查詢的名稱相符。 然而，這並非必要條件。 在SELECT查詢中調用列的順序指定它們的排列方式。
* 名為的新列 `ad_source` 是為了更輕鬆篩選 [!DNL AdWords] 或 [!DNL Facebook] 資料。 請記住，此查詢會結合兩個表中的所有資料。 如果您不建立 `ad_source`)，從特定來源識別支出並不容易。

將上述查詢儲存為 `Data Warehouse View` 將建立包含兩者的新表 [!DNL Facebook] 和 [!DNL AdWords] 支出，如下所示：

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | ee | 10.2 | 2000年 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | dd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aa | 7 | 2000年 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | ee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | cc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | ff | 28.5 | 10200 | 280 |

您現在可以使用上表來建立單一量度集，以擷取所有廣告，而不必為每個廣告來源建立個別的行銷量度集。

**想要其他幫助嗎？**

寫入SQL並建立 `Data Warehouse Views` 技術支援中未包含。  但是，服務團隊在建立意見方面提供協助。 從使用新資料庫遷移和整合舊資料庫到建立單個Data Warehouse視圖以用於特定分析的所有方面，他們都擅長針對您的所有資料結構難題組織基於SQL的解決方案。

在大多數情況下，建立 `Data Warehouse View` 為了整合2-3個類似結構的表，需要5小時的服務時間，這相當於1250美元的工作。 但以下是一些可能增加預期所需投資的共同因素：

* 將3個以上的表合併到單個視圖中
* 建立多個資料倉庫視圖
* 複雜的連接邏輯或過濾條件
* 將2個或多個表與不同的資料結構合併
