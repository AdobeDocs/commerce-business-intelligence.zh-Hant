---
title: 報告零售日曆
description: 瞭解如何設定結構以在您的 [!DNL Commerce Intelligence] 帳戶。
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# 報告零售日曆

本主題演示如何設定結構以使用 [4-5-4零售日曆](https://nrf.com/resources/4-5-4-calendar) 在 [!DNL Adobe Commerce Intelligence] 帳戶。 可視報表生成器提供了極其靈活的時間範圍、間隔和獨立設定。 但是，所有這些設定都與傳統的月曆配合使用。

由於許多客戶更改其日曆以使用零售日期或會計日期，因此以下步驟說明了如何使用資料並使用零售日期建立報表。 儘管下面的說明引用了4-5-4零售日曆，但您可以根據您的團隊使用的任何特定日曆對其進行修改，無論是財務日曆還是僅是自定義時間框架。

在開始之前，您應查看 [檔案上載程式](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 並確保你把 `.csv` 的子菜單。 這可確保日期涵蓋您的所有歷史資料，並將日期推向未來。

此分析包含 [高級計算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 入門

你可以 [下載](../../assets/454-calendar.csv) a `.csv` 零售年度4-5-4零售日曆版本，由2014年至2017年。 您可能需要根據內部零售日曆調整此檔案並擴展日期範圍以支援您的歷史和當前時間範圍。 下載檔案後，使用「檔案上載程式」在中建立「零售日曆」表 [!DNL Commerce Intelligence] Data Warehouse。 如果您使用的是4-5-4零售日曆的未更改版本，請確保此表中欄位的結構和資料類型與以下內容相匹配：

| 列名 | 列資料類型 | 主鍵 |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` （最多255個字元） | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## 要建立的列

* **銷售\_訂單** 表
   * `INPUT` `created\_at` (yyyy-mm-dd 00):00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **零售日曆** 檔案上載表
   * **當前日期**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL資料類型]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >的 `now()` 以上函式是特定於PostgreSQL的。 儘管 [!DNL Commerce Intelligence] 資料倉庫在PostgreSQL上托管，有些可能在Redshift上托管。 如果上述計算返回錯誤，則可能需要使用Redshift函式 `getdate()` 而不是 `now()`。
   * **當前零售年** （必須由支援分析員建立）
      * [!UICONTROL Column type]:E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **是否包括在當前零售年度？ （是/否）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL資料類型]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **是否包括在上個零售年度？ （是/否）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL資料類型]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **銷售\_訂單** 表
   * **建立\_at（零售年）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 選擇 [!UICONTROL table]: `Retail Calendar`
      * 選擇 [!UICONTROL column]: `Year Retail`
   * **建立時間\_at（零售周）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]:銷售\_訂單。\[INPUT\]已建立\_at(yyyy-mm-dd 00):00:00
         * [!UICONTROL One]:零售日曆。日期零售
      * 選擇 [!UICONTROL table]: `Retail Calendar`
      * 選擇 [!UICONTROL column]: `Week Retail`
   * **建立\_at（零售月）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 選擇 [!UICONTROL table]: `Retail Calendar`
      * 選擇 [!UICONTROL column]: `Month Number Retail`
   * **是否包括在上一零售年度？ （是/否）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]:零售 `Calendar.Date Retail`
      * 選擇 [!UICONTROL table]: `Retail Calendar`
      * 選擇 [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **是否包括在當前零售年度？ （是/否）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]:零售 `Calendar.Date Retail`
      * 選擇 [!UICONTROL table]: `Retail Calendar`
      * 選擇 [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## 度量

注：此分析不需要新的度量。 但是，請確保 [將sales\_order表中生成的新列添加為維](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 在繼續報告之前，獲取sales\_order表上的所有度量。

## 報告

* **每週訂單 — 零售日曆(YoY)**
   * 度量 `A`: `2017`
      * [!UICONTROL Metric]:訂單數
      * [!UICONTROL Filter]:
         * 建立\_at（零售年）= 2017
   * 度量 `B`: `2016`
      * [!UICONTROL Metric]:訂單數
      * [!UICONTROL Filter]:
         * 建立\_at（零售年）= 2016
   * 度量 `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
      [!UICONTROL Chart type]: `Line`
      * 關閉 `multiple Y-axes`

* **零售日曆概覽（當前按月的零售年）**
   * 度量 `A`: `Revenue`
      * 
         [!UICONTROL度量]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 度量 `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 度量 `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

* **零售日曆概覽（上個零售年按月）**
   * 度量 `A`: `Revenue`
      * 
         [!UICONTROL度量]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 度量 `B`: `Orders`
      * [!UICONTROL Metric]:訂單數
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 度量 `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

## 後續步驟

上面介紹如何將零售日曆配置為與基於您的 `sales\_order` 表(例如 `Revenue` 或 `Orders`)。 您還可以擴展此功能，以支援任何表上構建的度量的零售日曆。 唯一的要求是此表具有可用於加入Retail Calendar表的有效日期時間欄位。

例如，要查看4-5-4零售日曆上的客戶級別度量，請建立 `Same Table` 計算 `customer\_entity` 表，類似於 `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` 如上所述。 然後，可以使用此列重現 `One to Many` JOINED\_COLUMN計算(如 `Created_at (retail year)`) `Include in previous retail year? (Yes/No)` 加入 `customer\_entity` 的 `Retail Calendar` 的子菜單。

別忘了 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。
