---
title: 抵用券代碼分析（基本）
description: 瞭解企業的優惠券成效，是細分訂單，以及更清楚瞭解客戶習慣的有趣方式。
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# 基本抵用券程式碼分析

瞭解企業的優惠券成效是細分訂單和更好地瞭解客戶習慣的有趣方式。

本主題記錄建立此分析所需的步驟，以瞭解取得優惠券的客戶如何執行、檢視趨勢以及追蹤個別優惠券程式碼的使用情況。

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## 快速入門

首先，附註說明如何追蹤優惠券代碼。 如果客戶將抵用券套用至訂單，則會發生下列三件事：

* 折扣會反映在 `base_grand_total` 金額(您的 `Revenue` Commerce Intelligence中的量度)
* 優惠券代碼會儲存在 `coupon_code` 欄位。 如果此欄位為NULL （空白），則訂單沒有相關聯的抵用券。
* 折扣金額儲存在 `base_discount_amount`. 根據您的設定，此值可能顯示為負數或正數。

自Commerce 2.4.7起，客戶可將多個抵用券代碼套用至訂單。 在此案例中：

* 所有套用的優惠券代碼都會儲存在 `coupon_code` 欄位 `sales_order_coupons`. 套用的第一個抵用券代碼也會儲存在 `coupon_code` 欄位 `sales_order`. 如果此欄位為NULL （空白），則訂單沒有相關聯的抵用券。

## 建立量度

第一步是透過下列步驟建構新的量度：

* 瀏覽至 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* 選取 `sales_order`.
* 此量度會執行 **Sum** 於 **base_discount_amount** 欄，排序依據： **created_at**.
   * [!UICONTROL Filters]：
      * 新增 `Orders we count` （儲存的篩選器集）
      * 新增下列專案：
         * `coupon_code`**不是**`[NULL]`
      * 為量度命名，例如 `Coupon discount amount`.

## 建立您的控制面板

* 建立量度後：
   * 瀏覽至 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
   * 為控制面板命名，例如 `_Coupon Analysis_`.

* 您可在此建立和新增所有報表。

## 建立報表

* **新報告：**

>[!NOTE]
>
>此 [!UICONTROL Time Period]每個報表的**列為 `All-time`. 您可以根據分析需求隨意變更。 Adobe建議此儀表板上的所有報告涵蓋相同時段，例如 `All time`， `Year-to-date`，或 `Last 365 days`.

* **含優惠券的訂單**
   * 
     [！UICONTROL公制]: `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是** `[NULL]`

   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]：`Number (scalar)`

* **沒有優惠券的訂單**
   * 
     [！UICONTROL公制]: `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **是** `[NULL]`

   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]：`Number (scalar)`

* **含抵用券的訂單淨收入**
   * 
     [！UICONTROL公制]: `Revenue`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是** `[NULL]`

   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]： `Number (scalar)`

* **優惠券折扣**
   * [!UICONTROL Metric]： `Coupon discount amount`
   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]： `Number (scalar)`

* **平均期限收入：獲得優惠券的客戶**
   * [!UICONTROL Metric]： `Avg lifetime revenue`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`

   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]： `Number (scalar)`

* **平均期限收入：非優惠券取得的客戶**
   * [!UICONTROL Metric]： `Avg lifetime revenue`
      * 新增篩選器：
         * [A] `Customer's first order's coupon_code` **是**`[NULL]`

   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]： `Number (scalar)`

* **抵用券使用量詳細資料（首次訂單）**
   * 量度 `1`： `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`

   * 量度 `2`： `Revenue`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`

      * 重新命名：  `Net revenue`

   * 量度 `3`： `Coupon discount amount`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`

   * 建立公式： `Gross revenue`
      * [!UICONTROL Formula]： `(B – C)`
      * 
        [!UICONTROL Format]: `Currency`

   * 建立公式：**%折扣**
      * 公式： `(C / (B - C))`
      * 
        [!UICONTROL Format]: `Percentage`

   * 建立公式： `Average order discount`
      * [!UICONTROL Formula]： `(C / A)`
      * 
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * 
     [！UICONTROL圖表型別]: `Table`

* **依第一筆抵用券區分的平均期限收入**
   * [!UICONTROL Metric]：**平均期限收入**
      * 新增篩選器：
         * [`A`] `coupon_code` **是**`[NULL]`

   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]： `Number (scalar)`

* **抵用券使用量詳細資料（首次訂單）**
   * [!UICONTROL Metric]： `Avg lifetime revenue`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`

   * [!UICONTROL Time period]： `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Group by]： `Customer's first order's coupon_code`
   * 
     [！UICONTROL圖表型別]: **Column**

* **依優惠券/無優惠券贏取的新客戶**
   * 量度 `1`： `New customers`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`

      * [!UICONTROL Rename]： `Coupon acquisition customer`

   * 量度 `2`： `New customers`
      * 新增篩選器：
         * [`A`] `coupon_code` **是**`[NULL]`

      * [!UICONTROL Rename]： `Non-coupon acquisition customer`

   * [!UICONTROL Time period]： `All time`
   * [!UICONTROL Interval]： `By Month`
   * [!UICONTROL Chart type]： `Stacked Column`

建立報表後，請參閱本主題頂端的影像，瞭解如何在控制面板上組織報表。

>[!NOTE]
>
>截至Adobe Commerce 2.4.7，客戶可使用 **quote_coupons** 和 **sales_order_coupons** 取得客戶如何使用多張抵用券的深入分析表格。

![](../../assets/multicoupon_relationship_tables.png)
