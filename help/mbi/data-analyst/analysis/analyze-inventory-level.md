---
title: 分析庫存水準
description: 瞭解如何分析庫存水準。
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 分析庫存水準

本主題演示如何設定儀表板，該儀表板可提供對當前清單的洞察，並包含有關舊體系結構或新體系結構上客戶端的說明。 如果您沒有 **[!UICONTROL Data Warehouse Views]** 選項 **[!UICONTROL Manage Data]** 的子菜單。 如果您在舊體系結構上，請提交 [新支援請求](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 和主題 **[!UICONTROL INVENTORY ANALYSIS]** 一旦您到達 _計算列_ 下面的說明。

## 要跟蹤的列：

### 跟蹤說明的列

* **[!UICONTROL cataloginventory_stock_item]** 表：
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** 表：
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## 計算列：

+++ 新體系結構

* **[!UICONTROL catalog_product_entity]** 表：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * 選擇 [!UICONTROL DATETIME column]: `Product's most recent order date`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 輸入：
         * 答： `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * 如果A為空或B為空，則為空，則為null則為round(A::decimal/(extract(epocom from(current_timestamp - B))::decimal/604800.0),2)end





* **[!UICONTROL cataloginventory_stock_item]** 表：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 輸入：
         * 答： `qty`
         * B: `Avg products sold per week (all time)`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * 如果A為空或B為空或B = 0.0則為空，則為空，則為捨入(A::decimal/B,2)結束





+++
+++ 舊體系結構

* **[!UICONTROL catalog_product_entity]** 表：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * 選擇DATETIME列： **`Product's most recent order date`**
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * 選擇 [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * 在提交檔案時由分析師建立 **[庫存分析]** 支援請求





* **[!UICONTROL cataloginventory_stock_item]** 表：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選擇 [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * 在提交檔案時由分析師建立 **[!UICONTROL INVENTORY ANALYSIS]** 支援請求





+++

## 度量

### 度量說明

* **[!UICONTROL cataloginventory_stock_item]** 表：
   * **`Inventory on hand`**:此度量執行
      * **和** 的
      * **`qty`** 按排序的列
      * [無] 列

## 報告

### 報告說明

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * 時間間隔： `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 

      [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`
   * [!UICONTROL Time period]: `All time`
   * 時間間隔： `None`
   * 
      [!UICONTROL組依據]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`
   * [!UICONTROL Time period]: `All time`
   * 時間間隔： `None`
   * 
      [!UICONTROL組依據]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


如果您在構建此分析時遇到任何問題，或者只想與專業服務團隊接洽， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
