---
title: 分析存貨層次
description: 瞭解如何分析存貨層次。
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 分析存貨層次

此主題示範如何設定儀表板，其中提供您目前詳細目錄的分析，並包含舊版架構或新架構的客戶說明。 如果您在&#x200B;**[!UICONTROL Data Warehouse Views]**&#x200B;功能表下沒有&#x200B;**[!UICONTROL Manage Data]**&#x200B;選項，表示您使用的是舊版架構。 如果您使用舊版架構，請在到達以下[計算欄](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)指示中的指定區段後，提交主旨為&#x200B;**[!UICONTROL INVENTORY ANALYSIS]**&#x200B;的&#x200B;_新支援要求_。

## 要追蹤的欄：

### 要追蹤指示的欄

* **[!UICONTROL cataloginventory_stock_item]**&#x200B;資料表：
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]**&#x200B;資料表：
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## 計算的欄：

+++ 新架構

* **[!UICONTROL catalog_product_entity]**&#x200B;資料表：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]： `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]： `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]： `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * 選取[!UICONTROL DATETIME column]： `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]： `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `qty_ordered`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]： `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column]個輸入：
         * A： `Product's lifetime number of items sold`
         * B： `Product's first order date`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * 當A為null或B為null時則為空值，否則四捨五入(A：：decimal/(extract(epoch from (current_timestamp - B))：：decimal/604800.0)，2)結束

* **[!UICONTROL cataloginventory_stock_item]**&#x200B;資料表：
   * **`Sku`**
      * [!UICONTROL Column type]： `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]： `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]： `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]： `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]： `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column]個輸入：
         * A： `qty`
         * B： `Avg products sold per week (all time)`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * 當A為null或B為null或B = 0.0則為null，否則四捨五入(A：：decimal/B，2)結束

+++
+++ 舊版架構

* **[!UICONTROL catalog_product_entity]**&#x200B;資料表：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]： `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]： `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]： `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * 選取DATETIME資料行： **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]： `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]： **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * 選取[!UICONTROL column]： **`qty_ordered`**
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * 由分析人員建立，當您提交您的&#x200B;**[詳細目錄分析]**&#x200B;支援要求時

* **[!UICONTROL cataloginventory_stock_item]**&#x200B;資料表：
   * **`Sku`**
      * [!UICONTROL Column type]： `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]： `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]： `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]： `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取[!UICONTROL column]： `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * 由分析人員建立，當您提交您的&#x200B;**[!UICONTROL INVENTORY ANALYSIS]**&#x200B;支援要求時

+++

## 量度

### 量度指示

* **[!UICONTROL cataloginventory_stock_item]**&#x200B;資料表：
   * **`Inventory on hand`**：此量度執行
      * **總和**&#x200B;於
      * **`qty`**&#x200B;欄由
      * [無]欄

## 報表

### 報表指示

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]： `Inventory on hand`
   * [!UICONTROL Time period]： `All time`
   * 時間間隔： `None`
   * [!UICONTROL Group by]：
      * `Sku`
      * `Weeks on hand`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]： `Inventory on hand`
      * [!UICONTROL Filters]：
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]： `All time`
   * 時間間隔： `None`
   * &#x200B;
     [!UICONTROL 群組依據]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]： `Inventory on hand`
      * [!UICONTROL Filters]：
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]： `All time`
   * 時間間隔： `None`
   * &#x200B;
     [!UICONTROL 群組依據]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

如果您在建立此分析時遇到任何問題，或只是想與專業服務團隊互動，請[聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)。
