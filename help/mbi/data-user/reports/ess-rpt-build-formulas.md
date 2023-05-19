---
title: 公式
description: 瞭解如何使用公式。
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 公式

一個公式將多個度量和數學邏輯組合以回答問題。 例如，在假日季節，每個產品的收入中有多少是由新客戶創造的？

![儀表板中的假日銷售](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 步驟1:建立基本報告

1. 在菜單中，選擇 `Report Builder`。

1. 按一下 **[!UICONTROL Add Metric]** 並為報告選擇第一個度量。

   對於此示例， `Revenue by products ordered` 使用度量。

1. 按一下 **[!UICONTROL Add Metric]** 再次選擇報告的第二個度量。

   對於此示例， `New Customers` 使用度量。

1. 在提要欄中，按一下 **[!UICONTROL Details]** 顯示有關每個度量的資訊。

   ![按訂購產品列出的收入](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. 在提要欄中，按一下每個度量的名稱以在新瀏覽器頁籤中開啟設定頁。 向下滾動以查看度量的每個元件，包括度量查詢、篩選器和維。

   ![度量設定](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. 要返回報表，請按一下上一個瀏覽器頁籤。

1. 在圖表中，將滑鼠懸停在每行上的幾個資料點上，查看與每個度量關聯的金額。

## 步驟2:添加公式

1. 在提要欄頂部，按一下 **[!UICONTROL Add Formula]**。

   公式框將度量顯示為可用輸入 `A` 和 `B`，並包括一個輸入框，您可以在其中輸入公式。

   執行以下操作：

   * 在 `Enter your Formula` 輸入框，輸入 `A/B`。

      這將收入除以按新客戶數量訂購的產品。

   * 設定 `Select format` 至 `123Number`。

   * 在提要欄中，替換 `Untitled` 的名稱。

   ![公式設定](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 完成後，按一下 **[!UICONTROL Apply]**。

   報告現在有新的公式行， `New Customer Revenue`，邊欄顯示新客戶產生的收入總額。

   ![具有公式的報表](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 第3步：添加日期範圍

1. 按一下 **[!UICONTROL Date Range]** 在右上角。

1. 在 `Fixed Date Range` 頁籤中，執行以下操作：

   * 在日曆上，選擇日期範圍。

      對於此示例，假日季節是 `November 1` 通 `December 31`。

   * 下 `Select Time Interval`選項 `Day`。

      ![固定日期範圍](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 完成後，按一下 **[!UICONTROL Apply]**。

   現在，報告僅限於假日季節，每天都有資料點。

   ![固定日期範圍](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 第4步：保存報告

在此步驟中，您將報表另存為圖表和表。

1. 按一下 `Untitled Report` 在頁面頂部輸入描述性標題。 對於此示例，報表標題為 `2017 Holiday Sales`。

   然後，執行以下操作：

   * 在右上角，按一下 **[!UICONTROL Save]**。

   * 對於 `Type`，接受預設值 `Chart` 的子菜單。

   * 選擇 `Dashboard` 報告將在何處提供。

   * 按一下 **[!UICONTROL Save to Dashboard]**。

1. 按一下報告標題並更改名稱。 對於此示例，報告標題將更改為 `2017 Holiday Sales Data`。

   然後，執行以下操作：

   * 在右上角，按一下 **[!UICONTROL Save a Copy]**。

   * 設定 `Type` 至 `Table`。

   * 選擇 `Dashboard` 報告將在何處提供。

   * 按一下 **[!UICONTROL Save a Copy to Dashboard]**。

1. 要在儀表板中查看報表，請執行以下操作之一：

   * 按一下 **[!UICONTROL Go to Dashboard]** 的子菜單。

   * 在菜單中，選擇 **[!UICONTROL Dashboards]**。 按一下當前儀表板的名稱以顯示清單。 然後，按一下保存報告的儀表板的名稱。
