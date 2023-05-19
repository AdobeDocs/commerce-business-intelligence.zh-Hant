---
title: 優惠券代碼分析（基本）
description: 瞭解您的業務的優惠券效能是劃分訂單並更好地瞭解客戶習慣的有趣方法。
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 基本優惠券代碼分析

瞭解您的業務的優惠券表現是劃分訂單和更好地瞭解客戶習慣的有趣方法。

本主題記錄建立此分析所需的步驟，以瞭解購買優惠券的客戶的表現、查看趨勢和跟蹤單個優惠券代碼的使用情況。

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## 入門

首先，要說明如何跟蹤優惠券代碼。 如果客戶將優惠券應用於訂單，則會發生三件事：

* 折扣反映於 `base_grand_total` 金額 `Revenue` 度量)
* 優惠券代碼儲存在 `coupon_code` 的子菜單。 如果此欄位為NULL（空），則訂單沒有與其關聯的優惠券。
* 折現金額儲存於 `base_discount_amount`。 根據您的配置，此值可能顯示為負值或正值。

## 構建度量

第一步是構建新度量，步驟如下：

* 導航到 **[!UICONTROL Manage Data > Metrics > Create New Metric]**。

* 選擇 `sales_order`。
* 此度量執行 **和** 的 **base_discount_amount** 列，排序依據 **建立時間**。
   * [!UICONTROL Filters]:
      * 添加 `Orders we count` （保存的篩選器集）
      * 添加以下內容：
         * `coupon_code`**不**`[NULL]`
      * 為度量指定名稱，如 `Coupon discount amount`。

## 建立儀表板

* 建立度量後：
   * 導航到 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
   * 為儀表板指定名稱，如 `_Coupon Analysis_`。

* 這是您建立和添加所有報告的位置。

## 生成報告

* **新報告：**

>[!NOTE]
>
>的 [!UICONTROL Time Period]**每個報告列為 `All-time`。 您可以隨時更改此項，以滿足分析需要。 Adobe建議此儀表板上的所有報表都涵蓋同一時間段，如 `All time`。 `Year-to-date`或 `Last 365 days`。

* **帶優惠券的訂單**
   * 
      [!UICONTROL度量]: `Orders`
      * 添加篩選器：
         * [`A`] `coupon_code` **不** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **沒有優惠券的訂單**
   * 
      [!UICONTROL度量]: `Orders`
      * 添加篩選器：
         * [`A`] `coupon_code` **是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **帶優惠券的訂單淨收入**
   * 
      [!UICONTROL度量]: `Revenue`
      * 添加篩選器：
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

* **平均生命週期收入：已收購客戶的優惠券**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加篩選器：
         * [`A`] `Customer's first order's coupon_code` **不** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **平均生命週期收入：非優惠券收購客戶**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加篩選器：
         * [A] `Customer's first order's coupon_code` **是**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **優惠券使用詳細資訊（首次訂單）**
   * 度量 `1`: `Orders`
      * 添加篩選器：
         * [`A`] `coupon_code` **不**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`
   * 度量 `2`: `Revenue`
      * 添加篩選器：
         * [`A`] `coupon_code` **不**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`
      * 更名：  `Net revenue`
   * 度量 `3`: `Coupon discount amount`
      * 添加篩選器：
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








* **按一階優惠券列出的平均有效期收入**
   * [!UICONTROL Metric]:**平均生命週期收入**
      * 添加篩選器：
         * [`A`] `coupon_code` **是**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **優惠券使用詳細資訊（首次訂單）**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加篩選器：
         * [`A`] `Customer's first order's coupon_code` **不** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [!UICONTROL圖表類型]: **Column**


* **按優惠券/非優惠券收購劃分的新客戶**
   * 度量 `1`: `New customers`
      * 添加篩選器：
         * [`A`] `Customer's first order's coupon_code` **不** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * 度量 `2`: `New customers`
      * 添加篩選器：
         * [`A`] `coupon_code` **是**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





生成報告後，請參閱本主題頂部的影像，瞭解如何組織儀表板上的報告。
