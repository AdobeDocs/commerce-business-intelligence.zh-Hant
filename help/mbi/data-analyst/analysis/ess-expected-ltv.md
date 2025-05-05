---
title: 預期期限值(LTV)分析（基本）
description: 瞭解如何建立分析以瞭解目前客戶的期限值，並預測期限值如何隨著更多訂單而增加。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 預期期限值分析

預測客戶下更多訂單時的期限值是任何規模企業最重要的方面之一。

以下是建立分析的步驟，以瞭解目前客戶的期限值，並預測期限值如何隨著更多訂單而增加。

![預期期限值](../../assets/expected_ltv_720.png)

## 建立量度

第一步是透過下列步驟建構新的量度：
* 瀏覽至&#x200B;**[!UICONTROL Manage Data > Metrics]**
   * 檢視現有的&#x200B;**[!UICONTROL Avg lifetime revenue]**。

  >[!NOTE]
  >
  >此量度建構於的資料表（可能是`customer_entity`或`sales_order`，視您的存放區接受訪客結帳的能力而定。）

   * 按一下&#x200B;**[!UICONTROL Create New Metric]**&#x200B;並從上方選取表格。
   * 此量度在`Customer's lifetime revenue`欄上執行&#x200B;**中位數**，排序依據`created_at`。
      * [!UICONTROL Filters]：
         * 新增`Customers we count (Saved Filter Set)` （或`Registered accounts we count`）

   * 為量度命名，例如`Median lifetime revenue`。

## 建立您的控制面板

建立量度後，您可以&#x200B;**建立儀表板**，方法如下：
* 瀏覽至&#x200B;**[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
* 為儀表板命名，例如`Expected LTV`。

* 您可在此建立和新增所有報表。

## 建立報表

>[!NOTE]
>
>在&#x200B;**[!UICONTROL Time Period:]**，每個報表的時段會列為`All-time`。 您可以根據分析需求隨意變更。 Adobe建議此儀表板上的所有報告涵蓋相同時段，例如`All time`、`Year-to-date`或`Last 365 days`。

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]： `Avg lifetime revenue`
   * [!UICONTROL Time period]： `All time`
   * &#x200B;

     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart Type]： `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]： `Avg lifetime revenue`
      * 新增[!UICONTROL filters]：
         * [`A`] `Customer's group code` **不等於** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **大於**`0`

   * [!UICONTROL Time period]： `All time`
   * &#x200B;

     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart Type]： `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * 量度`1`： `Avg lifetime revenue`
   * 量度`2`： `Median lifetime revenue`
   * [!UICONTROL Time period]： `All time`
   * [!UICONTROL Interval]： `By Month`
   * &#x200B;

     [!UICONTROL 圖表型別]: `Line`
   * 取消核取`Multiple Y-Axes`

* **LTV （依存留期訂單數）**
   * 量度`1`： `Avg lifetime revenue`
   * 量度`2`： `New customers`
   * [!UICONTROL Time period]： `All time`
   * &#x200B;

     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Group by]： `Customer's lifetime number of orders`
   * &#x200B;

     [!UICONTROL 圖表型別]: `Line`

  >[!NOTE]
  >
  >不要為`Customer's lifetime number of orders`新增所有值。 反之，看看新客戶數目達到極少數的情況，然後手動將每個客戶的期限訂單值新增到該點。 舉例來說，如果同一訂單有200位客戶、2位75位、3位15位和4位，請新增&#x200B;*1、2和3*。

* 新增現有的[!UICONTROL Avg customer lifetime revenue by cohort]報告。

建立報表後，請參閱本主題頂端的影像，瞭解如何在控制面板上組織報表。
