---
title: 在視覺Report Builder中使用時間選項
description: 瞭解如何分析特定時段內的報表資料。
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# 在[!DNL Time]中使用[!DNL Visual Report Builder]選項

[!DNL Visual Report Builder]的功能之一是全域`Time Range`和`Interval`設定。 這些設定可讓您分析特定時段內的報表資料。

但是，對於某些分析，您可能需要在同一報告中考慮不同的時間範圍或時間間隔。 這是`Time`選項的功能。 為了讓您更瞭解如何在報表中使用`Time`選項，本教學課程涵蓋下列使用案例：

* [分析沒有時間戳記的量度](#notimestamp)
* [指定一個量度獨立的時間間隔](#independenttimeinterval)
* [比較不同時間範圍內的相同量度](#difftimerange)

如果您想要跟隨此主題中討論的一些範例報告，請先開啟[[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md)再繼續。

## 分析沒有時間戳記的量度 {#notimestamp}

有些量度無法隨著時間推移而改變，因為資料並未收集或與相關聯的時間戳記一起儲存。 例如，詳細目錄表格通常每個SKU只包含一列。 在這種情況下，您應該在不指定時間戳記的情況下[建立量度](../data-user/reports/ess-manage-data-metrics.md)。

當您在報表中使用這類量度時，您會注意到，將此量度新增至報表，會自動設定獨立的`Time Interval` （共`None`個）和`Time Range` （共`Global`個）：

![](../assets/Metrics_without_timestamps.gif)

## 指定一個量度獨立的時間間隔 {#independenttimeinterval}

`Time`選項可讓您建立以時間為基礎的100%圖表，以識別在特定時間範圍內哪一天、周、月或年貢獻了最大的值。 在此區段中，您會建立圖表以顯示一年中每個日曆月所產生的收入百分比。

如果您想要比較逐年產生的收入，這類報表相當實用。 舉例來說，您有一張2015年圖表顯示，1月貢獻該年18%的收入，而另一張圖表顯示2016年只有8%。 您可以開始研究可能已發生的情況。

1. 將您的`Revenue`量度新增至報表。
1. 按一下&#x200B;**[!UICONTROL Duplicate]**&#x200B;以製作量度副本。
1. 按一下全域&#x200B;**[!UICONTROL Time Range]**&#x200B;選項，然後按&#x200B;**[!UICONTROL Moving Time Range]**。 將此專案設定為`Last Year`。
1. 按一下全域&#x200B;**[!UICONTROL Time Interval]**&#x200B;選項，並將其設定為`Monthly`。
1. Report Builder會自動為第二個量度新增第二個Y軸。 取消選取`Multiple Y-Axes`方塊。
1. 接下來，您將獨立的`Time Interval`套用至第一個量度。 按一下&#x200B;**[!UICONTROL Time Options]**&#x200B;右側的`first Revenue metric` （時鐘圖示）。
1. 在報表上方顯示的展開視窗中，按一下&#x200B;**[!UICONTROL Time Options]**。
1. 在下拉式清單中，設定下列專案：

   * `Time Interval`：將此專案設為`None`。

   * `Time Range`：先按一下`Last Year`，再按一下&#x200B;**[!UICONTROL Custom]**，最後選取&#x200B;**[!UICONTROL Moving Range]**&#x200B;選項，將此專案設定為`Last Year`。

   * 按一下&#x200B;**[!UICONTROL Apply]**&#x200B;以儲存間隔和範圍設定。 這會建立一個量度，用於計算上一年度的總收入。 接下來，您將此量度當做公式中的分母。

   * 若要檢視每個月的收入百分比，您必須將公式新增至報表。 按一下&#x200B;**[!UICONTROL Add Formula]**。

   * 在公式欄位中輸入`B/A`，並從文字欄位旁的下拉式清單中選取`% Percent`。 此公式將去年特定月份的收入金額除以去年的收入總額。

   * 按一下&#x200B;**[!UICONTROL Apply Changes]**。

   * 隱藏您的兩個輸入量度並重新命名公式。

現在您可以瞭解去年每個月的影響力有多大：

![](../assets/Independent_Time_Int.png)

## 比較不同時間範圍內的相同量度 {#difftimerange}

此範例使用名為`Day number of the month`的自訂維度。 如果您想要建立此報表，但您的Data Warehouse中尚未有此維度，請[聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)以尋求協助。

此類別中最常見的兩個範例是(1)比較成長量度（逐年收入或逐月收入），以及(2)更瞭解最近的存貨或專案銷售趨勢。

若要示範此使用案例，請檢視上個月的每日收入與去年同期比較。 假設您想檢視2016年1月的每日收入，然後與2015年1月、2014年1月等比較，此報表會顯示該情形。

1. 將您的`Revenue`量度新增至報表。
1. 按一下&#x200B;**[!UICONTROL Duplicate]**&#x200B;以製作量度副本。
1. 將第一個量度重新命名為`Items sold last 7 days`，將第二個量度重新命名為`Items sold last 28 days`。
1. 按一下&#x200B;**[!UICONTROL Time Range]**，然後按&#x200B;**[!UICONTROL Moving Time Range]**。 將此專案設定為`Last Month`。
1. 按一下&#x200B;**[!UICONTROL Time Interval]**&#x200B;並將其設定為`None`。
1. 按一下第二個&#x200B;**[!UICONTROL Time Options]**&#x200B;量度旁的`Revenue` （時鐘圖示）。
1. 在報表上方顯示的展開視窗中，按一下&#x200B;**[!UICONTROL Time Options]**。
1. 在下拉式清單中，設定下列專案：

   * `Time Interval`：將此專案設為`None`。

   * `Time Range`：先按一下`From 14 Months Ago To 13 Months Ago`，再按一下&#x200B;**[!UICONTROL Custom]**，將此專案設定為&#x200B;**[!UICONTROL Moving Range]**。 使用功能表頂端的欄位和下拉式清單來設定範圍。 此設定可讓我們檢視上個月的收入，但同時也是上年的收入。

   如果量度從報表中消失，不必擔心，設定獨立時間選項會自動隱藏報表中的量度。 若要重新顯示，請按一下量度旁的&#x200B;**[!UICONTROL Show]**。

   ![](../assets/Different_Time_Ranges.gif)

   * 按一下&#x200B;**[!UICONTROL Apply]**&#x200B;以儲存間隔和範圍設定。

   * 接著，按一下`Day number of the month`並選取維度，以新增自訂&#x200B;**[!UICONTROL Group By]**&#x200B;維度。 這會傳回訂單當月的天數，例如，在3月2日下單的訂單會傳回`2`。

   * 在`Group By`下拉式清單中，選取`Show All`並按一下&#x200B;**[!UICONTROL Apply]**。 這會建立報表的X軸值：

   ![](../assets/TO4.png)

   * 重新命名量度。 在此範例中，第一個量度是`Revenue - 2015`，第二個是`Revenue - 2014`。

自訂`Time Options`的另一個常見用途是決定供給的周數。 特別是在節日季節或特殊促銷期間，您可能想要考量過去一週、一個月及上一個促銷期間所出售的料號，以做出明智的購買決定。

請記得在自行建立此報表時，將時間範圍設定為您所需的設定。

1. 將您的`Items Sold`量度新增至報表。
1. 按一下&#x200B;**[!UICONTROL Duplicate]**&#x200B;以製作量度副本。
1. 重新命名量度。 您可以使用相同的名稱或類似名稱：
   1. 將第一個量度重新命名為`Items sold last 7 days`。
   1. 將第二個量度重新命名為`Items sold last 28 days`。
1. 在`Items sold last 7 days`量度上，按一下全域&#x200B;**[!UICONTROL Time Range]**&#x200B;選項，然後按&#x200B;**[!UICONTROL Moving Time Range]**。 在此範例中，您將其設為`Last 7 Days`。
1. 按一下&#x200B;**[!UICONTROL Time Interval]**&#x200B;並將其設定為`None`。
1. 接下來，您定義`Time Options`量度的`Items sold last 28 days`。 按一下&#x200B;**[!UICONTROL Time Options]**&#x200B;量度右邊的`second Items sold` （時鐘圖示）。
1. 在報表上方顯示的展開視窗中，按一下&#x200B;**[!UICONTROL Time Options]**。
1. 在下拉式清單中，設定下列專案：

   * `Time Interval`：將此專案設為`None`。
   * `Time Range`：先按一下`From 29 days to 1 day ago`，再按一下&#x200B;**[!UICONTROL Custom]**，將此專案設定為&#x200B;**[!UICONTROL Moving Range]**。 使用功能表頂端的欄位和下拉式清單來設定範圍。
   * 按一下&#x200B;**[!UICONTROL Apply]**&#x200B;以儲存間隔和範圍設定。
   * 複製`Items sold last 28 days`量度並開啟新量度的`Time Options`。 設定下列選項：

      * `Time Interval`：請將此專案保留為`None`。
      * `Time Range`：按一下&#x200B;**[!UICONTROL Specific Date Range]**，然後輸入適當的日期，將此變更為符合您感興趣之促銷活動的日期範圍。
      * 重新命名量度`Items sold during last promotion`或類似專案。
      * 新增您的`Units on hand`量度。
      * 接下來，您必須針對您要納入報表中的時段（`last 7 days`、`last 28 days`及`last promo`時段），新增顯示庫存周數的計算，並考量銷售趨勢。 您必須針對每個時段執行此動作一次。

若要建立公式，請按一下&#x200B;**[!UICONTROL Add Formula]**。 在下面輸入公式，完成後，按一下&#x200B;**[!UICONTROL Apply Changes]**。 對三個時段中的每一個重複此步驟：

* 針對`last 7 days time period`，在`D / A`欄位中輸入`Formula`。
* 針對`last 28 days time period`，在`D / (B/4)`欄位中輸入`Formula`。

  >[!NOTE]
  >
  >請務必在此標準化您選取的時間範圍。 在此範例中，將28天分成四周。 您可能需要將不同的邏輯套用至公式。

* 針對`last promo period`，在`D / C`欄位中輸入`Formula`。

  ![](../assets/Different_Time_Ranges_2.png)

* 最後，隱藏量度並將`SKU`或類似的維度以`Group By`形式新增至報表，以自訂報表。

此範例說明目前的存貨層次適合全產品14天銷售。 不過，新增可供比較的促銷期間時，表示公司需要進行一些變更，或是訂購更多存貨，或是隻促銷庫存量足夠的料號。

由於您的客戶隨著時間的推移而表現出不同的行為，您可能會在執行分析時看到資料中的差異。 設定自訂時間選項可讓您快速建立複雜的分析，啟用資料導向式決策，將歷史趨勢納入考量。

