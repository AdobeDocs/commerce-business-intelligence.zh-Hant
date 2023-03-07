---
title: 抵用券代碼分析（基本）
description: 了解企業的抵用券表現，是劃分訂單和深入了解客戶習慣的有趣方式。
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 基本抵用券代碼分析

了解企業的抵用券表現，是劃分訂單和深入了解客戶習慣的有趣方式。

本文記錄建立此分析所需的步驟，以了解購買抵用券的客戶如何執行、查看趨勢，以及追蹤個別抵用券代碼的使用情形。

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## 快速入門

首先，提供如何追蹤抵用券代碼的附註。 如果客戶將抵用券套用至訂單，會發生三件事：

* 折扣反映於 `base_grand_total` amount( `Revenue` 度量(MBI)
* 抵用券代碼儲存在 `coupon_code` 欄位。 如果此欄位為NULL（空），則訂單沒有與其關聯的抵用券。
* 貼現金額儲存在 `base_discount_amount`. 視您的設定而定，此值可能會顯示為負值或正值。

## 建立量度

第一步是透過下列步驟來建構新量度：

* 導覽至 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* 選取 `sales_order`.
* 此量度會執行 **總和** 在 **base_discount_amount** 列，按順序排列 **created_at**.
   * [!UICONTROL Filters]:
      * 新增 `Orders we count` （儲存的篩選集）
      * 新增下列項目：
         * `coupon_code`**不**`[NULL]`
      * 為量度命名，例如 `Coupon discount amount`.

## 建立控制面板

* 建立量度後：
   * 導覽至 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
   * 為控制面板命名，例如 `_Coupon Analysis_`.

* 這是您建立和新增所有報表的位置。

## 建立報表

* **新報表：**

>[!NOTE]
>
>此 [!UICONTROL Time Period]**對於每個報告，列為 `All-time`. 您可以隨意修改，以符合您的分析需求。 Adobe建議此控制面板上的所有報表涵蓋相同時段，例如 `All time`, `Year-to-date`，或 `Last 365 days`.

* **具有優惠券的訂單**
   * 
      [!UICONTROL量度]: `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **不** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **沒有優惠券的訂單**
   * 
      [!UICONTROL量度]: `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **IS** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **具有抵用券之訂單的淨收入**
   * 
      [!UICONTROL量度]: `Revenue`
      * 新增篩選器：
         * [`A`] `coupon_code` **不** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **優惠券折扣**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **平均期限收入：獲得優惠券的客戶**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **平均期限收入：非抵用券購買客戶**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增篩選器：
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **抵用券使用量詳細資料（首次訂購）**
   * 量度 `1`: `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **不**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`
   * 量度 `2`: `Revenue`
      * 新增篩選器：
         * [`A`] `coupon_code` **不**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`
      * 重新命名：  `Net revenue`
   * 量度 `3`: `Coupon discount amount`
      * 新增篩選器：
         * [`A`] `coupon_code` **不**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`
   * 建立公式： `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * 建立公式：**%折扣**
      * 公式： `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * 建立公式： `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * 

      [!UICONTROL圖表類型]: `Table`








* **依首次訂購抵用券的平均期限收入**
   * [!UICONTROL Metric]:**平均期限收入**
      * 新增篩選器：
         * [`A`] `coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **抵用券使用量詳細資料（首次訂購）**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [!UICONTROL圖表類型]: **Column**


* **按抵用券/非抵用券贏取列出的新客戶**
   * 量度 `1`: `New customers`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * 量度 `2`: `New customers`
      * 新增篩選器：
         * [`A`] `coupon_code` **IS**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





建立報表後，請參閱本主題頂端的影像，了解如何組織控制面板上的報表。
