---
title: 公式
description: 瞭解如何使用公式。
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 公式

公式結合多個量度和數學邏輯來回答問題。 例如，新客戶在假日季節每件產品會產生多少收入？

![儀表板中的假日銷售](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 步驟1：建立基本報表

1. 在功能表中，選擇`Report Builder`。

1. 按一下「**[!UICONTROL Add Metric]**」並選擇報表的第一個量度。

   此範例使用`Revenue by products ordered`量度。

1. 再按一下「**[!UICONTROL Add Metric]**」，然後選擇報表的第二個量度。

   此範例使用`New Customers`量度。

1. 在側邊欄中，按一下&#x200B;**[!UICONTROL Details]**&#x200B;以顯示每個量度的相關資訊。

   ![依訂購產品區分的收入](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. 在側邊欄中，按一下每個量度的名稱，以在新的瀏覽器分頁中開啟設定頁面。 向下捲動以檢視量度的每個元件，包括量度查詢、篩選器和維度。

   ![量度設定](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. 若要返回您的報表，請按一下前一個瀏覽器索引標籤。

1. 在圖表中，將滑鼠游標停留在每條線上的幾個資料點上，即可檢視與每個量度關聯的金額。

## 步驟2：新增公式

1. 在側邊欄的頂端，按一下&#x200B;**[!UICONTROL Add Formula]**。

   公式方塊會將量度顯示為可用的輸入`A`和`B`，並包含一個輸入方塊，您可以在其中輸入公式。

   執行下列動作：

   * 在`Enter your Formula`輸入方塊中，輸入`A/B`。

     這會將收入除以新客戶數量訂購的產品。

   * 將`Select format`設為`123Number`。

   * 在側邊欄中，將`Untitled`取代為公式的名稱。

   ![公式設定](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 完成時，按一下&#x200B;**[!UICONTROL Apply]**。

   報表現在有公式的新行`New Customer Revenue`，而側邊欄會顯示新客戶產生的收入總額。

   ![含公式的報告](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 步驟3：新增日期範圍

1. 按一下右上角的&#x200B;**[!UICONTROL Date Range]**。

1. 在`Fixed Date Range`標籤上，執行下列動作：

   * 在行事曆上，選擇日期範圍。

     在此範例中，假日季節是從`November 1`到`December 31`。

   * 在`Select Time Interval`底下，選擇`Day`。

     ![固定日期範圍](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 完成時，按一下&#x200B;**[!UICONTROL Apply]**。

   報表現在僅限於假日季節，每天會有資料點。

   ![固定日期範圍](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 步驟4：儲存報表

在此步驟中，您可將報表另存為圖表和表格。

1. 按一下頁面頂端的`Untitled Report`並輸入描述性標題。 在此範例中，報告標題為`2017 Holiday Sales`。

   接著，執行下列動作：

   * 按一下右上角的&#x200B;**[!UICONTROL Save]**。

   * 對於`Type`，接受預設的`Chart`設定。

   * 選擇要提供報表的`Dashboard`。

   * 按一下&#x200B;**[!UICONTROL Save to Dashboard]**。

1. 按一下報告標題並變更名稱。 在此範例中，報告標題已變更為`2017 Holiday Sales Data`。

   接著，執行下列動作：

   * 按一下右上角的&#x200B;**[!UICONTROL Save a Copy]**。

   * 將`Type`設為`Table`。

   * 選擇要提供報表的`Dashboard`。

   * 按一下&#x200B;**[!UICONTROL Save a Copy to Dashboard]**。

1. 若要在控制面板中檢視報表，請執行下列任一項作業：

   * 按一下頁面頂端訊息中的&#x200B;**[!UICONTROL Go to Dashboard]**。

   * 在功能表中，選擇&#x200B;**[!UICONTROL Dashboards]**。 按一下目前圖示板的名稱以顯示清單。 然後，按一下儲存報表之控制面板的名稱。
