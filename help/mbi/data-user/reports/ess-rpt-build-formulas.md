---
title: 公式
description: 了解如何使用公式。
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# 公式

公式結合多個量度和數學邏輯以回答問題。 例如，假日期間每個產品的收入有多少是由新客戶產生？

![儀表板中的節假日銷售](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 步驟1:建立基本報表

1. 在功能表中，選擇 `Report Builder`.

1. 按一下 **[!UICONTROL Add Metric]** 並選擇報表的第一個量度。

   在此範例中， `Revenue by products ordered` 度量已使用。

1. 按一下 **[!UICONTROL Add Metric]** 再次，為報表選擇第二個量度。

   在此範例中， `New Customers` 度量已使用。

1. 在側欄中，按一下 **[!UICONTROL Details]** 以顯示每個量度的相關資訊。

   ![按訂購產品列出的收入](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. 在側欄中，按一下每個量度的名稱，在新瀏覽器分頁中開啟設定頁面。 向下捲動以查看量度的每個元件，包括量度查詢、篩選和維度。

   ![量度設定](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. 若要返回報表，請按一下上一個瀏覽器標籤。

1. 在圖表中，將滑鼠指標暫留在每行的數個資料點上，查看與每個量度相關聯的金額。

## 步驟2:新增公式

1. 在側欄頂端，按一下 **[!UICONTROL Add Formula]**.

   公式方塊會將量度顯示為可用輸入 `A` 和 `B`，並包含輸入方塊，您可在此輸入公式。

   執行下列動作：

   * 在 `Enter your Formul` 輸入框，輸入 `A/B`.

      這會將收入除以訂購的產品數量。

   * 設定 `Select format` to `123Number`.

   * 在側欄中，取代 `Untitled` 的名稱。

   ![公式設定](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 完成後，按一下 **[!UICONTROL Apply]**.

   報表現在有新的公式行， `New Customer Revenue`，側邊欄則顯示新客戶產生的收入總額。

   ![含公式的報表](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 步驟3:新增日期範圍

1. 按一下 **[!UICONTROL Date Range]** 在右上角。

1. 在 `Fixed Date Range` 頁簽，執行下列操作：

   * 在日曆上，選擇日期範圍。

      在此範例中，節日季節是從11月1日到12月31日。

   * 在 `Select Time Interval`，選擇 `Day`.

      ![固定日期範圍](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 完成後，按一下 **[!UICONTROL Apply]**.

   報表現在僅限於節日季，且每天都有資料點。

   ![固定日期範圍](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 步驟4:儲存報表

在此步驟中，您會將報表儲存為圖表和表格。

1. 按一下 `Untitled Report` 並輸入描述性標題。 在此範例中，報表標題為 `2017 Holiday Sales`.

   然後，執行下列動作：

   * 在右上角，按一下 **[!UICONTROL Save]**.

   * 針對 `Type`，接受預設值 `Chart` 設定。

   * 選擇 `Dashboard` 報表可供使用的位置。

   * 按一下 **[!UICONTROL Save to Dashboard]**.

1. 按一下報表標題並變更名稱。 在此範例中，報表標題已變更為 `2017 Holiday Sales Data`.

   然後，執行下列動作：

   * 在右上角，按一下 **[!UICONTROL Save a Copy]**.

   * 設定 `Type` to `Table`.

   * 選擇 `Dashboard` 報表可供使用的位置。

   * 按一下 **[!UICONTROL Save a Copy to Dashboard]**.

1. 若要在控制面板中查看報表，請執行下列其中一項操作：

   * 按一下 **[!UICONTROL Go to Dashboard]** 在頁面頂端的訊息中。

   * 在功能表中，選擇 **[!UICONTROL Dashboards]**. 按一下目前控制面板的名稱以顯示清單。 然後，按一下儲存報表的控制面板名稱。
