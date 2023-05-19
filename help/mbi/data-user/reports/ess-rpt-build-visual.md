---
title: 視覺Report Builder
description: 瞭解如何使用視覺Report Builder。
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# [!DNL Visual Report Builder]

[!DNL Visual Report Builder] 使基於預定義度量建立快速報告變得容易。 每個度量都包括定義報表資料集的查詢。

以下示例說明如何建立簡單報表、按附加維對資料進行分組、設定日期和時間間隔、更改圖表類型以及將報表保存到儀表板。

## 要建立簡單報表：

1. 在 [!DNL Commerce Intelligence] 菜單，按一下 **[!UICONTROL Report Builder]**。

1. 下 [!UICONTROL Visual Report Builder]按一下 **[!UICONTROL Create Report]** 並執行以下操作：

   * 按一下 **[!UICONTROL Add Metric]**。

      可用度量可以按字母順序或按表列出。

      ![視覺Report Builder](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * 選擇 [度量](../../data-user/reports/ess-manage-data-metrics.md) 描述要用於報表的資料集。

      的 `New Customers` 此示例中使用的度量計算所有客戶，並按客戶註冊帳戶的日期對清單進行排序。 初始報告包括簡單的線形圖，後面是資料表。

      左側的摘要顯示當前度量的名稱，後面是在度量中指定的列資料的任何計算結果。 在此實例中，匯總顯示客戶總數。

      ![視覺Report Builder](../../assets/magento-bi-report-builder-untitled.png)

1. 在圖表中，將滑鼠懸停線上上的每個資料點上。 每個資料點顯示當月註冊的新客戶總數。

1. 按照以下說明對資料進行分組、更改日期範圍和圖表類型。

   **`Group By`**

   的 `Group By` 控制項允許您按組或段添加多個維。 Dimension是表中可用於對資料進行分組的列。

   * 從清單中選擇一個可用維 `Group By` 頁籤

      在此示例中，系統找到了客戶在下訂單時使用的五個優惠券代碼。

      ![分組依據](../../assets/magento-bi-report-builder-group-by-dimensions.png)

      的 `Group By` 詳細資訊列出客戶使用的每個優惠券。 用於放置初始訂單的優惠券用複選框標籤。 此圖表現在具有多條彩色線，這些線代表用於第一訂單的每個優惠券。 圖例是彩色編碼的，對應於每一行資料。

   * 按一下 **[!UICONTROL Apply]** 以關閉Group By詳細資訊。

      ![多個Dimension](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * 將滑鼠指針懸停在每行上的幾個資料點上，查看當月在訂購第一張優惠券時使用該優惠券的客戶數。

   * 資料表現在具有附加維度，每個月都有一列，每個優惠券代碼都有一行。

      ![按表資料分組](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * 按一下轉置(![](../../assets/magento-bi-btn-transpose.png))控制項以更改資料的方向。

      資料的軸被翻轉，表現在為每個優惠券代碼都有一列，每個月都有一行。 您可能會發現此方向更易於閱讀。

      ![轉換資料](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)
   **`Date Range`**

   的 `Date Range` 控制項顯示當前日期範圍和時間間隔設定，位於圖表右上方。

   * 按一下 `Date Range` 控制項，在本例中，它設定為 `All-Time by Month`。

      ![日期範圍](../../assets/magento-bi-report-builder-date-range.png)

   * 進行以下更改：

      * 要放大更近的視圖，請將日期範圍更改為 `Last Full Quarter`。
      * 下 `Select Time Interval`選項 `Week`。
      * 完成後，按一下 **[!UICONTROL Save]**。

      報告現在僅包括上一季度的資料，按星期分列。

      ![按周列出的上一季度報告](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)
   **圖表類型**

   * 按一下右上角的控制項以查找資料的最佳圖表。

      某些圖表類型與多維資料不相容。

      |  |  |
      |-----|-----|
      | ![](../../assets/magento-bi-btn-chart-line.png) | 線圖 |
      | ![](../../assets/magento-bi-btn-chart-horz-bar.png) | 水準條 |
      | ![](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | 水準堆積條 |
      | ![](../../assets/magento-bi-btn-chart-vert-bar.png) | 竪線 |
      | ![](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | 垂直堆積條 |
      | ![](../../assets/magento-bi-btn-chart-pie.png) | 餅 |
      | ![](../../assets/magento-bi-btn-chart-area.png) | 區域 |
      | ![](../../assets/magento-bi-btn-chart-funnel.png) | 漏斗 |

      {style="table-layout:auto"}




1. 給報告一個 `title`，替換 `Untitled Report` 頁面頂部的文本，帶有描述性標題。

1. 在右上角，按一下 **[!UICONTROL Save]** 並執行以下操作：

   * 對於 `Type`，接受預設設定， `Chart`。

   * 選擇 `Dashboard` 報告將在何處提供。

   * 按一下 **[!UICONTROL Save to Dashboard]**。

      ![保存到儀表板](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. 要在儀表板中查看圖表，請執行以下操作之一：

   * 按一下 **[!UICONTROL Go to Dashboard]** 的子菜單。

   * 在菜單中，選擇 `Dashboards` 並按一下當前操控板的名稱以顯示清單。 然後，按一下保存報告的儀表板的名稱。

      ![儀表板中的報告](../../assets/magento-bi-report-builder-my-dashboard.png)
