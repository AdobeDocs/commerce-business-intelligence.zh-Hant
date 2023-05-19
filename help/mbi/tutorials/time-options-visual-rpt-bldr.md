---
title: 在可視Report Builder中使用時間選項
description: 學習分析報告中特定時段的資料。
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# 使用 [!DNL Time] 中的選項 [!DNL Visual Report Builder]

的一個特徵 [!DNL Visual Report Builder] 是全球 `Time Range` 和 `Interval` 的子菜單。 這些設定允許您分析報告中特定時間段的資料。

但是，對於某些分析，可能需要考慮同一報告中的不同時間範圍或時間間隔。 那就是 `Time` 選擇就來了。 讓你更清楚地知道如何使用 `Time` 本教程將介紹以下使用案例：

* [分析沒有時間戳的度量](#notimestamp)
* [給一個度量一個獨立的時間間隔](#independenttimeinterval)
* [比較不同時間範圍內的相同度量](#difftimerange)

如果要跟隨本主題中討論的某些示例報告，請開啟 [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) 再繼續。

## 分析沒有時間戳的度量 {#notimestamp}

某些度量根本無法隨時間變化而變化，因為未收集或儲存資料時沒有關聯的時間戳。 例如，清單表通常只包含一行，每個SKU都包含一行。 那樣的話，你應該 [建立度量](../data-user/reports/ess-manage-data-metrics.md) 不指定時間戳。

在報告中使用此度量時，您會注意到，將此度量添加到報告中會自動設定獨立 `Time Interval` 共 `None` 和 `Time Range` 共 `Global`:

![](../assets/Metrics_without_timestamps.gif)

## 給一個度量一個獨立的時間間隔 {#independenttimeinterval}

`Time` 選項允許您建立基於時間的100%圖表，以確定在特定時間範圍內哪天、周、月或年貢獻的值最多。 在此部分，您將建立一個圖表，顯示每年每個日曆月中生成的收入百分比。

如果要比較年內生成的收入，此類型的報表將非常有用。 例如，你有一張2015年的圖表顯示，1月份貢獻了該年收入的18%，而2016年的圖表只貢獻了8%。 你可以開始研究可能發生的事。

1. 添加 `Revenue` 度量。
1. 按一下 **[!UICONTROL Duplicate]** 來複製度量。
1. 按一下全局 **[!UICONTROL Time Range]** 選項 **[!UICONTROL Moving Time Range]**。 將此設定為 `Last Year`。
1. 按一下全局 **[!UICONTROL Time Interval]** 選項，並將其設定為 `Monthly`。
1. Report Builder自動為第二度量添加第二Y軸。 取消選擇 `Multiple Y-Axes` 框。
1. 接下來，你申請一個 `Time Interval` 到第一個指標。 按一下 **[!UICONTROL Time Options]** （時鐘錶徵圖） `first Revenue metric`。
1. 按一下 **[!UICONTROL Time Options]** 的子菜單。
1. 在下拉清單中，設定以下內容：

   * `Time Interval`:將其設定為 `None`。

   * `Time Range`:將其設定為 `Last Year` 按 **[!UICONTROL Custom]**，則 **[!UICONTROL Moving Range]**，最後選擇 `Last Year` 的雙曲餘切值。

   * 按一下 **[!UICONTROL Apply]** 的子菜單。 這將建立一個計算上一年總收入的度量。 接下來，您將此度量用作公式中的分母。

   * 要查看每月收入百分比，您必須向報表添加公式。 按一下 **[!UICONTROL Add Formula]**。

   * 輸入 `B/A` 在「公式」欄位中，然後選擇 `% Percent` 的子菜單。 此公式將去年某個特定月份的收入金額除以去年的總收入金額。

   * 按一下 **[!UICONTROL Apply Changes]**。

   * 隱藏兩個輸入度量並更名公式。

現在，你可以看到，去年每個月的影響有多大：

![](../assets/Independent_Time_Int.png)

## 比較不同時間範圍內的相同度量 {#difftimerange}

此示例使用名為 `Day number of the month`。 如果要建立此報表，並且Data Warehouse中尚未包含此維， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 尋求幫助。

此類別中最常見的兩個示例是：(1)比較增長指標（年比收入或月比）和(2)更好地瞭解最近的庫存或物料銷售趨勢。

要演示此使用情形，請查看上個月與上年同月相比的每日收入。 如果您想查看2016年1月的每天收入，然後將其與2015年1月、2014年1月等等進行比較，則此報告將向我們展示這一點。

1. 添加 `Revenue` 度量。
1. 按一下 **[!UICONTROL Duplicate]** 來複製度量。
1. 將第一個度量更名為 `Items sold last 7 days` 第二個指標 `Items sold last 28 days`。
1. 按一下 **[!UICONTROL Time Range]**，則 **[!UICONTROL Moving Time Range]**。 將此設定為 `Last Month`。
1. 按一下 **[!UICONTROL Time Interval]** 並將其設定為 `None`。
1. 按一下 **[!UICONTROL Time Options]** （時鐘錶徵圖） `Revenue` 度量。
1. 按一下 **[!UICONTROL Time Options]** 的子菜單。
1. 在下拉清單中，設定以下內容：

   * `Time Interval`:將其設定為 `None`。

   * `Time Range`:將其設定為 `From 14 Months Ago To 13 Months Ago` 按 **[!UICONTROL Custom]** 然後 **[!UICONTROL Moving Range]**。 使用菜單頂部的欄位和下拉清單設定範圍。 此設定允許我們查看上個月（但是上一年）的收入。
   不要擔心度量是否從報告中消失 — 設定獨立時間選項會自動將度量從報告中隱藏。 要重新顯示它，請按一下 **[!UICONTROL Show]** 指標旁邊。

   ![](../assets/Different_Time_Ranges.gif)

   * 按一下 **[!UICONTROL Apply]** 的子菜單。

   * 接下來，添加自定義 `Day number of the month` 按一下 **[!UICONTROL Group By]** 和選取尺寸。 這將返回訂單月份的日號 — 例如，在3月2日下達的訂單將返回 `2`。

   * 在 `Group By` 下拉清單，選擇 `Show All` 按一下 **[!UICONTROL Apply]**。 這將建立報表的X軸值：

   ![](../assets/TO4.png)

   * 更名度量。 在示例中，第一個度量是 `Revenue - 2015` 第二個是 `Revenue - 2014`。



自定義的另一種常用用途 `Time Options` 就是確定供應周數。 特別是在假日季或特殊促銷期間，您可能要考慮在上週、月和上一促銷期間銷售的物料，以便做出明智的採購決策。

切記將時間範圍設定為您自己構建此報告時需要的時間範圍。

1. 添加 `Items Sold` 度量。
1. 按一下 **[!UICONTROL Duplicate]** 來複製度量。
1. 更名度量。 可以使用相同的名稱或使用相似的內容：
   1. 將第一個度量更名為 `Items sold last 7 days`。
   1. 將第二個度量更名為 `Items sold last 28 days`。
1. 在 `Items sold last 7 days` 度量，按一下全局 **[!UICONTROL Time Range]** 選項 **[!UICONTROL Moving Time Range]**。 對於此示例，將其設定為 `Last 7 Days`。
1. 按一下 **[!UICONTROL Time Interval]** 並將其設定為 `None`。
1. 接下來，定義 `Time Options` 為 `Items sold last 28 days` 度量。 按一下 **[!UICONTROL Time Options]** （時鐘錶徵圖） `second Items sold` 度量。
1. 按一下 **[!UICONTROL Time Options]** 的子菜單。
1. 在下拉清單中，設定以下內容：

   * `Time Interval`:將其設定為 `None`。
   * `Time Range`:將其設定為 `From 29 days to 1 day ago` 按 **[!UICONTROL Custom]**，則 **[!UICONTROL Moving Range]**。 使用菜單頂部的欄位和下拉清單設定範圍。
   * 按一下 **[!UICONTROL Apply]** 的子菜單。
   * 複製 `Items sold last 28 days` 並開啟新度量 `Time Options`。 將選項設定為：

      * `Time Interval`:留下 `None`。
      * `Time Range`:通過按一下 **[!UICONTROL Specific Date Range]** 然後輸入相應的日期。
      * 更名度量 `Items sold during last promotion` 或者類似的。
      * 添加 `Units on hand` 度量。
      * 接下來，您必須添加計算，以顯示該時段的現有周數（考慮銷售趨勢）(`last 7 days`。 `last 28 days`, `last promo` 包括在報表中。 您必須對每個時間段執行一次此操作。

要建立公式，請按一下 **[!UICONTROL Add Formula]**。 輸入下面的公式，然後按一下 **[!UICONTROL Apply Changes]** 的子菜單。 對以下三個時段中的每個時段重複此步驟：

* 對於 `last 7 days time period`輸入 `D / A` 的 `Formula` 的子菜單。
* 對於 `last 28 days time period`輸入 `D / (B/4)` 的 `Formula` 的子菜單。

   >[!NOTE]
   >
   >在此處將所選時間範圍規範化非常重要。 在本例中，將28天分為4週。 您可能需要對公式應用不同的邏輯。

* 對於 `last promo period`輸入 `D / C` 的 `Formula` 的子菜單。

   ![](../assets/Different_Time_Ranges_2.png)

* 最後，通過隱藏度量並添加 `SKU` 或與報表類似的維 `Group By`。

此示例說明，當前庫存水準非常適合於整個產品範圍的14天銷售。 但是，增加一個可比的促銷期意味著公司需要做出一些改變 — 要麼訂購更多庫存，要麼只推廣庫存足夠的物品。

因為客戶的行為隨著時間的推移而有所不同，因此在執行分析時，您會看到資料的差異。 設定自定義時間選項使您能夠快速建立複雜的分析，從而實現資料驅動的決策，該決策將歷史趨勢考慮在內。

