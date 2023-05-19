---
title: 建立和使用Data Warehouse視圖
description: 瞭解通過修改現有表建立新倉庫表的方法，或通過使用SQL將多個表連接或合併在一起。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 9%

---

# 使用Data Warehouse視圖

本文檔概述了 `Data Warehouse Views` 導航至 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**。 下面是它所執行的操作和如何建立視圖的說明，以及如何使用的示例 `Data Warehouse Views` 合併 [!DNL Facebook] 和 [!DNL AdWords] 花費資料。

## 通用

的 `Data Warehouse Views` 特徵是一種通過修改現有表建立新的倉庫表的方法，或者通過使用SQL將多個表連接或合併在一起。 一次 `Data Warehouse View` 已由更新週期建立和處理，它將作為新表在Data Warehouse中填充 `Data Warehouse Views` 下拉清單，如下所示：

![](../../assets/Data_Warehouse.png)

從這裡，新視圖可以像其他任何表一樣運行，從而讓您能夠建立新的計算列或在其上構建度量和報告。

`Data Warehouse Views` 主要用於將多個相似但不同的表合併在一起，這樣所有報告都可以構建在單個新表上。 幾個常見的示例包括：將表從舊資料庫和活動資料庫合併，以組合歷史資料和當前資料，或將多個廣告源(如Facebook和AdWords)合併為單個廣告源 `Consolidated ad spend` 的子菜單。

如果您熟悉SQL ，則這兩個合併示例都使用 `UNION` 函式，但是在生成新視圖時，可以使用任何PostgreSQL語法和函式。

## 建立和管理Data Warehouse視圖

新建 `Data Warehouse Views` 可以建立現有視圖，並可通過導航刪除 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**，如下所示：

![](../../assets/Data_Warehouse_Views.png)

在此處，您可以按照以下示例說明建立視圖：

1. 如果觀察現有視圖，請按一下 **[!UICONTROL New Data Warehouse View]** 的子菜單。 如果已開啟空查詢窗口，請繼續執行下一步。
1. 通過在 `View Name` 的子菜單。 此處提供的名稱決定了Data Warehouse中視圖的顯示名稱。 `View names` 限於小寫字母、數字和下划線(_)。 所有其他字元都被禁止。
1. 在標題為「Oracle Unter(O)」的窗口中輸入查詢 `Select Query`，使用標準PostgreSQL語法。

   >[!NOTE]
   >
   >查詢必須引用特定的列名。 使用 `*`不允許使用選擇所有列的字元。

1. 完成後，按一下 **[!UICONTROL Save]** 的子菜單。 您的視圖暫時具有 `Pending` 狀態，直到下一個完整更新週期處理它，此時狀態將更改為 `Active`。 在由更新處理後，您的視圖已準備好在報告中使用。

必須指出，保存後，用於生成 `Data Warehouse View` 無法編輯。 如果需要調整 `Data Warehouse View`，必須建立視圖，並手動將任何計算列、度量或報表從原始視圖遷移到新視圖。 遷移完成後，可以安全地刪除原始視圖。 因為 `Data Warehouse Views` 不可編輯，Adobe建議您使用 `SQL Report Builder` 將查詢另存為Data Warehouse視圖。

## 示例： [!DNL Facebook] 和 [!DNL Google AdWords] 資料

更仔細地看一下本文前面提到的一個例子：合併 [!DNL Facebook] 和 [!DNL AdWords] 將資料用於新的整合廣告表。 最常見的是，這包括合併兩個表，下面是示例資料集：

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | e | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | gggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | a | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | e | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | ff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | a | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | a | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | a | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | c | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

建立包含兩者的單個廣告支出表 [!DNL Facebook] 和 [!DNL Google AdWords] 市場活動，您必須編寫SQL查詢並使用 `UNION ALL` 的子菜單。 A `UNION ALL` 語句通常用於組合多個不同的SQL查詢，同時將每個查詢的結果附加到單個輸出。

有幾個要求 `UNION` 值得一提的語句，如PostgreSQL中所述 [文檔](https://www.postgresql.org/docs/8.3/queries-union.html):

* 所有查詢必須返回相同數目的列
* 相應列必須具有相同的資料類型

執行 `UNION` 或 `UNION ALL` 語句，最終輸出中列的名稱反映第一個查詢中列的命名。

通常，整合您的 [!DNL Facebook] 和 [!DNL Google AdWords] 將資料 `Data Warehouse View` 要求建立包含七列的表，其查詢與以下內容類似：

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

關於上面的幾個重要點：

* 為了清晰起見，所有列都在上方別名，以便所有查詢的名稱都匹配。 但這並不是要求。 在SELECT查詢中調用列的順序指示列的排列方式。
* 名為 `ad_source` 是為了便於篩選 [!DNL AdWords] 或 [!DNL Facebook] 資料。 請記住，此查詢合併了兩個表中的所有資料。 如果不建立類似 `ad_source`)，從特定來源識別支出並非易事。

將上述查詢另存為 `Data Warehouse View` 建立同時具有兩者的表 [!DNL Facebook] 和 [!DNL AdWords] 支出，與以下內容類似：

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | a | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | e | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | gggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | a | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | a | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | a | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | e | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | c | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | ff | 28.5 | 10200 | 280 |

您不能為每個廣告源建立一組單獨的營銷指標，而只能使用上表建立一組指標，以捕獲您的所有廣告。

**尋求其他幫助？**

寫入SQL並建立 `Data Warehouse Views` 不包括在技術支援中。 然而， [服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 確實有助於建立觀點。 從使用新資料庫遷移舊式資料庫到建立單個Data Warehouse視圖以用於特定分析，支援團隊可以提供幫助。

通常，建立 `Data Warehouse View` 為了整合2-3個類似結構的表，需要5個小時的服務時間，也就是大約1 250美元的工作時間。 然而，以下是可增加預期所需投資的幾個共同因素：

* 將三個以上的表合併到單個視圖中
* 建立多個Data Warehouse視圖
* 複合連接邏輯或過濾條件
* 具有不同資料結構的兩個或多個表的合併
