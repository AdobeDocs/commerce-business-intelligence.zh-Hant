---
title: 預期期限值(LTV)分析（基本）
description: 瞭解如何建立分析以瞭解目前客戶的期限值，並預測期限值如何隨著更多訂單而增加。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 預期期限值分析

預測客戶下更多訂單時的期限值是任何規模企業最重要的方面之一。

以下是建立分析的步驟，以瞭解目前客戶的期限值，並預測期限值如何隨著更多訂單而增加。

![預期期限值](../../assets/expected_ltv_720.png)

## 建立量度

第一步是透過下列步驟建構新的量度：
* 瀏覽至 **[!UICONTROL Manage Data > Metrics]**
   * 檢視現有的 **[!UICONTROL Avg lifetime revenue]**.

  >[!NOTE]
  >
  >建構此量度的表格(可能 `customer_entity` 或 `sales_order` 視您的商店是否接受訪客結帳而定。)

   * 按一下 **[!UICONTROL Create New Metric]** 並從上方選取表格。
   * 此量度會執行 **中間值** 於 `Customer's lifetime revenue` 欄，排序依據： `created_at`.
      * [!UICONTROL Filters]:
         * 新增 `Customers we count (Saved Filter Set)` (或 `Registered accounts we count`)

   * 為量度命名，例如 `Median lifetime revenue`.

## 建立您的控制面板

建立量度後，您可以 **建立儀表板** 藉由執行下列動作：
* 瀏覽至 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* 為控制面板命名，例如 `Expected LTV`.

* 您可在此建立和新增所有報表。

## 建立報表

>[!NOTE]
>
>開啟 **[!UICONTROL Time Period:]**，則每個報表的時段會列為 `All-time`. 您可以根據分析需求隨意變更。 Adobe建議此儀表板上的所有報告涵蓋相同時段，例如 `All time`， `Year-to-date`，或 `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增 [!UICONTROL filters]：
         * [`A`] `Customer's group code` **不等於** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **大於**`0`

   * [!UICONTROL Time period]: `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * 量度 `1`： `Avg lifetime revenue`
   * 量度 `2`： `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
     [！UICONTROL圖表型別]: `Line`
   * 取消核取 `Multiple Y-Axes`

* **LTV （依期限訂單數）**
   * 量度 `1`： `Avg lifetime revenue`
   * 量度 `2`： `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
     [！UICONTROL間隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 
     [！UICONTROL圖表型別]: `Line`

  >[!NOTE]
  >
  >不要新增以下專案的所有值： `Customer's lifetime number of orders`. 反之，看看新客戶數目達到極少數的情況，然後手動將每個客戶的期限訂單值新增到該點。 舉例來說，如果同一訂單有200位客戶、兩訂單有75位、三訂單有15位、四訂單有3位，則新增 *1、2和3*.

* 新增現有 [!UICONTROL Avg customer lifetime revenue by cohort] 報告。

建立報表後，請參閱本主題頂端的影像，瞭解如何在控制面板上組織報表。
