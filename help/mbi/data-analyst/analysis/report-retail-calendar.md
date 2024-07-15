---
title: 在零售行事曆上建立報表
description: 瞭解如何設定結構，以便在您的 [!DNL Commerce Intelligence] 帳戶中使用4-5-4零售行事曆。
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# 在零售行事曆上建立報表

此主題示範如何設定結構以在您的[!DNL Adobe Commerce Intelligence]帳戶中使用[4-5-4零售行事曆](https://nrf.com/resources/4-5-4-calendar)。 視覺化Report Builder提供極為靈活的時間範圍、間隔和獨立設定。 不過，所有這些設定都可以搭配現有的傳統每月行事曆運作。

由於許多客戶會變更其行事曆以使用零售或會計日期，以下步驟說明如何使用零售日期來使用您的資料並建立報表。 雖然以下指示參考4-5-4零售日曆，但您可以為團隊使用的任何特定日曆更改它們，無論是財務日曆還是自訂時間範圍。

開始之前，您應該檢閱[檔案上傳程式](../../data-analyst/importing-data/connecting-data/using-file-uploader.md)，並確定您已拉長`.csv`檔案。 這可確保日期涵蓋所有歷史資料，並將日期推送至未來。

此分析包含[進階計算資料行](../data-warehouse-mgr/adv-calc-columns.md)。

## 快速入門

您可以[下載](../../assets/454-calendar.csv)2}版本的4-5-4零售日曆，適用於2014至2017年的零售業。 `.csv`您可能需要根據內部零售日曆調整此檔案，並擴大日期範圍以支援您的歷史和目前時間範圍。 下載檔案後，使用檔案上傳程式在[!DNL Commerce Intelligence]Data Warehouse中建立零售業行事曆表格。 如果您使用4-5-4零售行事曆的未變更版本，請確保此表格中欄位的結構和資料型別符合以下內容：

| 欄名稱 | 欄資料型別 | 主索引鍵 |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` （最多255個字元） | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## 要建立的欄

* **sales\_order**&#x200B;資料表
   * `INPUT` `created\_at` (yyyy-mm-dd 00:00:00)
      * [!UICONTROL Column type]： - `Same table > Calculation`
      * [!UICONTROL Inputs]： - `created\_at`
      * [!UICONTROL Datatype]： - `Datetime`
      * [!UICONTROL Calculation]： - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **零售行事曆**&#x200B;檔案上傳表格
   * **目前日期**
      * [!UICONTROL Column type]： `Same table > Calculation`
      * [!UICONTROL Inputs]： `Date Retail`
      * 
        [！UICONTROL資料型別]: `Datetime`
      * [!UICONTROL Calculation]： `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >上述`now()`函式是PostgreSQL專屬的函式。 雖然大部分[!DNL Commerce Intelligence]資料倉儲都在PostgreSQL上代管，但有些可能會在Redshift上代管。 如果上述計算傳回錯誤，您可能需要使用Redshift函式`getdate()`，而非`now()`。

   * **目前的零售年度** （必須由支援分析人員建立）
      * [!UICONTROL Column type]： E`vent Counter`
      * [!UICONTROL Local Key]： `Current date`
      * [!UICONTROL Remote Key]： `Retail calendar.Date Retail`
      * 
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]： `Year Retail`
   * **包含在目前的零售年度中？ （是/否）**
      * [!UICONTROL Column type]： `Same table > Calculation`
      * [!UICONTROL Inputs]：
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [！UICONTROL資料型別]: `String`
      * [!UICONTROL Calculation]： `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **包含在上一個零售年度？ （是/否）**
      * [!UICONTROL Column type]： `Same table > Calculation`
      * [!UICONTROL Inputs]：
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [！UICONTROL資料型別]: String
      * [!UICONTROL Calculation]： `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **sales\_order**&#x200B;資料表
   * **已建立\_at （零售年份）**
      * [!UICONTROL Column type]： `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]： `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]： `Retail Calendar.Date Retail`
      * 選取[!UICONTROL table]： `Retail Calendar`
      * 選取[!UICONTROL column]： `Year Retail`
   * **已建立\_at （零售周）**
      * [!UICONTROL Column type]： `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]： sales\_order。\[INPUT\]已建立\_at (yyyy-mm-dd 00:00:00
         * [!UICONTROL One]： Retail Calendar.Date零售業
      * 選取[!UICONTROL table]： `Retail Calendar`
      * 選取[!UICONTROL column]： `Week Retail`
   * **已建立\_at （零售月份）**
      * [!UICONTROL Column type]： `One to Many > JOINED\_COLUMN`
      * 路徑
         * [!UICONTROL Many]： `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]： `Retail Calendar.Date Retail`
      * 選取[!UICONTROL table]： `Retail Calendar`
      * 選取[!UICONTROL column]： `Month Number Retail`
   * **是否包含在上一個零售年度？ （是/否）**
      * [!UICONTROL Column type]： `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]： `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：零售業`Calendar.Date Retail`
      * 選取[!UICONTROL table]： `Retail Calendar`
      * 選取[!UICONTROL column]： `Include in previous retail year? (Yes/No)`
   * **是否包含於目前的零售年度？ （是/否）**
      * [!UICONTROL Column type]： `One to Many > JOINED\_COLUMN`
      * 路徑 — 
         * [!UICONTROL Many]： `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：零售業`Calendar.Date Retail`
      * 選取[!UICONTROL table]： `Retail Calendar`
      * 選取[!UICONTROL column]： `Include in current retail year? (Yes/No)`

## 量度

注意：此分析不需要新量度。 不過，在繼續處理報表之前，請務必[將您在sales\_order表格中建立的新欄新增為sales\_order表格上所有量度的維度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。

## 報表

* **每週訂單 — 零售行事曆(YoY)**
   * 量度`A`： `2017`
      * [!UICONTROL Metric]：訂單數
      * [!UICONTROL Filter]：
         * 建立時間\_at （零售業年份） = 2017
   * 量度`B`： `2016`
      * [!UICONTROL Metric]：訂單數
      * [!UICONTROL Filter]：
         * 建立時間\_at （零售業年份） = 2016
   * 量度`C`： `2015`
      * [!UICONTROL Metric]： `Number of orders`
      * [!UICONTROL Filter]：
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]： `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
     [!UICONTROL Chart type]: `Line`
      * 關閉`multiple Y-axes`

* **零售行事曆總覽（目前零售年份，依月份）**
   * 量度`A`： `Revenue`
      * 
        [！UICONTROL公制]: `Revenue`
      * [!UICONTROL Filter]：
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * 量度`B`： `Orders`
      * [!UICONTROL Metric]： `Number of orders`
      * [!UICONTROL Filter]：
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * 量度`C`： `Avg order value`
      * [!UICONTROL Metric]： `Avg order value`
      * [!UICONTROL Filter]：
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]： `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

* **零售行事曆總覽（前一個零售年度，依月份）**
   * 量度`A`： `Revenue`
      * 
        [！UICONTROL公制]: `Revenue`
      * [!UICONTROL Filter]：
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * 量度`B`： `Orders`
      * [!UICONTROL Metric]：訂單數
      * [!UICONTROL Filter]：
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * 量度`C`： `Avg order value`
      * [!UICONTROL Metric]： `Avg order value`
      * [!UICONTROL Filter]：
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]： `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

## 後續步驟

上述說明如何設定零售行事曆以與您`sales\_order`資料表上建置的任何量度相容（例如`Revenue`或`Orders`）。 您也可以擴充此功能，以支援任何表格上建立之量度的零售業行事曆。 此表格唯一需要的是一個有效的日期時間欄位，可用來聯結至「零售業行事曆」表格。

例如，若要在4-5-4零售行事曆上檢視客戶層級量度，請在`customer\_entity`表格中建立`Same Table`計算，類似於上述`\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`。 然後，您可以使用此資料行將`customer\_entity`資料表加入`Retail Calendar`資料表，以重新產生`One to Many` JOINED\_COLUMN計算（例如`Created_at (retail year)`）和`Include in previous retail year? (Yes/No)`。

在建立新報表之前，別忘了[將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)的維度。
