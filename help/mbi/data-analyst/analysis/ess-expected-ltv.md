---
title: 預期期限值(LTV)分析（基本）
description: 了解如何建立分析以了解您目前客戶的期限值，並預測期限值會隨著更多訂單而增加的情形。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 預期期限值分析

在客戶下更多訂單時預測其期限值，是任何規模業務中最重要的環節之一。

以下是建立分析以了解目前客戶期限值的步驟，以及預測期限值將如何隨著更多訂單而增加的步驟：

![預期期限值](../../assets/expected_ltv_720.png)

## 建立量度

第一步將是透過下列步驟建立新量度：
* 導覽至 **[!UICONTROL Manage Data > Metrics]**
   * 檢視現有 **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >此量度所建構的表格(可能 `customer_entity` 或 `sales_order` 取決於您商店接受訪客結帳的能力。)

   * 按一下 **[!UICONTROL Create New Metric]** 並從上方選取表格。
   * 此量度會執行 **中位數** 在 `Customer's lifetime revenue` 列，按順序排列 `created_at`.
      * [!UICONTROL Filters]:
         * 新增 `Customers we count (Saved Filter Set)` (或 `Registered accounts we count`)
   * 為量度命名，例如 `Median lifetime revenue`.



## 建立控制面板

建立量度後，您可以 **建立控制面板** 通過執行以下操作：
* 導覽至 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* 為控制面板命名，例如 `Expected LTV`.

* 我們將在此建立和新增所有報表。

## 建立報表

* 如果尚未，請簽出 [此影片](https://fast.wistia.net/embed/iframe/24zz7wmjrt) 關於使用**[!UICONTROL Visual Report Builder] 建立圖表、表和標量值。

>[!NOTE]
>
>開啟 **[!UICONTROL Time Period:]**，則每個報表的時段會列為 `All-time`. 您可以隨意修改，以符合您的分析需求。 我們建議此控制面板上的所有報表涵蓋相同時段，例如 `All time`, `Year-to-date`，或 `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增 [!UICONTROL filters]:
         * [`A`] `Customer's group code` **不等於** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **大於**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * 量度 `1`: `Avg lifetime revenue`
   * 量度 `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL圖表類型]: `Line`
   * 取消選中 `Multiple Y-Axes`

* **按期限訂購數的LTV**
   * 量度 `1`: `Avg lifetime revenue`
   * 量度 `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL圖表類型]: `Line`
   >[!NOTE]
   >
   >請勿為 `Customer's lifetime number of orders`，而是查看新客戶數量達到少數的點，然後手動將每個客戶的期限訂單數量值新增至該點。 例如，如果一次訂購有200位客戶，第2次75位，第3次15位，第4次3位，新增 *1、2和3*.

* 新增現有 [!UICONTROL Avg customer lifetime revenue by cohort] 報表。

建立報表後，請參閱本主題頂端的影像，了解如何組織控制面板上的報表。
