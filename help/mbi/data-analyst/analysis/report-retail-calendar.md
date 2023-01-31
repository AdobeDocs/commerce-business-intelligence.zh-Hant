---
title: 在零售日曆上製作報表
description: 了解如何設定結構，在您的 [!DNL MBI] 帳戶。
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# 在零售日曆上報告

在本文中，我們演示了如何建立結構以使用 [4-5-4零售日曆](https://nrf.com/resources/4-5-4-calendar) 在 [!DNL MBI] 帳戶。 視覺化報告建立工具提供極富彈性的時間範圍、間隔和獨立設定。 我們的團隊也能協助您變更一週中的開始日，以符合您的業務偏好。 不過，所有這些設定都可搭配傳統的每月日曆使用。

由於我們的許多客戶更改其日曆以使用零售或會計日期，下列步驟將說明如何使用您的資料並使用零售日期建立報表。 雖然下列指示會參考4-5-4零售日曆，但您可以針對您的團隊使用的任何特定日曆加以變更，無論是財務日曆還是自訂日曆。

開始之前，請熟悉 [檔案上傳程式](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 並確保你把 `.csv` 檔案，讓日期可涵蓋所有歷史資料，並將日期推送至未來。

此分析包含 [進階計算欄](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入門

您可以 [下載](../../assets/454-calendar.csv) a `.csv` 零售年度4-5-4零售日曆版本（2014至2017年）。 請注意，您可能需要根據內部零售日曆調整此檔案，並延長日期範圍，以支援您的歷史和目前時間範圍。 下載檔案後，請使用「檔案上傳程式」，在您的 [!DNL MBI] 資料倉庫。 如果您使用的是4-5-4零售日曆的未更改版本，請確保此表中欄位的結構和資料類型與以下內容相符：

| 欄名稱 | 列資料類型 | 主鍵 |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` （最多255個字元） | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style=&quot;table-layout:auto&quot;}

## 要建立的列

* **sales\_order** 表格
   * `INPUT` `created\_at` (yyyy-mm-dd 00:00:00)
      * [!UICONTROL Column type]:- `Same table > Calculation`
      * [!UICONTROL Inputs]:- `created\_at`
      * [!UICONTROL Datatype]:- `Datetime`
      * [!UICONTROL Calculation]:- ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **零售日曆** 檔案上傳表
   * **目前日期**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL資料類型]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >此 `now()` 上述函式是PostgreSQL專用的。 雖然 [!DNL MBI] 資料倉庫由PostgreSQL托管，有些可能由Redshift托管。 如果上述計算返回錯誤，則可能需要使用Redshift函式 `getdate()` 而非 `now()`.
   * **當前零售年** （必須由支援分析人員建立）
      * [!UICONTROL Column type]:E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **是否包含在當前零售年？ （是/否）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL資料類型]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **是否包含在前一零售年？ （是/否）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL資料類型]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** 表格
   * **建立\_at（零售年）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 選取 [!UICONTROL table]: `Retail Calendar`
      * 選取 [!UICONTROL column]: `Year Retail`
   * **建立\_at（零售周）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]:sales\_order。\[INPUT\]已建立\_at(yyyy-mm-dd 00:00:00
         * [!UICONTROL One]：零售日曆。日期重新整理
      * 選取 [!UICONTROL table]: `Retail Calendar`
      * 選取 [!UICONTROL column]: `Week Retail`
   * **建立\_at（零售月）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 選取 [!UICONTROL table]: `Retail Calendar`
      * 選取 [!UICONTROL column]: `Month Number Retail`
   * **包括在前一個零售年？ （是/否）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]:零售 `Calendar.Date Retail`
      * 選取 [!UICONTROL table]: `Retail Calendar`
      * 選取 [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **是否包括在當前零售年？ （是/否）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]:零售 `Calendar.Date Retail`
      * 選取 [!UICONTROL table]: `Retail Calendar`
      * 選取 [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## 量度

注意：此分析不需要新量度。 不過，請務必 [將您在sales\_order表中建立的新列作為維添加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ，以繼續前往報表。

## 報表

* **每週訂單 — 零售日曆(YoY)**
   * 量度 `A`: `2017`
      * [!UICONTROL Metric]:訂單數
      * [!UICONTROL Filter]:
         * 建立\_at（零售年）= 2017
   * 量度 `B`: `2016`
      * [!UICONTROL Metric]:訂單數
      * [!UICONTROL Filter]:
         * 建立\_at（零售年）= 2016
   * 量度 `C`: `2015`
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

* **零售日曆概述（當前按月的零售年份）**
   * 量度 `A`: `Revenue`
      * 
         [!UICONTROL量度]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `C`: `Avg order value`
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

* **零售日曆概觀（前一個零售年份，按月）**
   * 量度 `A`: `Revenue`
      * 
         [!UICONTROL量度]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `B`: `Orders`
      * [!UICONTROL Metric]:訂單數
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `C`: `Avg order value`
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

上述說明如何設定零售日曆，使其與您 `sales\_order` 表格(例如，`Revenue` 和 `Orders`)，但您也可以延伸此功能，以支援任何表格上所建量度的零售日曆。 唯一的要求是此表具有有效的日期時間欄位，可用於連接到零售日曆表。

例如，若要在零售日曆上檢視4-5-4度量，請建立新 `Same Table` 在 `customer\_entity` 表格，類似 `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` 如上所述。 然後，您可以使用此欄來重現 `One to Many` JOINED\_COLUMN計算(如 `Created_at (retail year)` 和 `Include in previous retail year? (Yes/No)` 加入 `customer\_entity` 表格 `Retail Calendar` 表格。

別忘了 [將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。
