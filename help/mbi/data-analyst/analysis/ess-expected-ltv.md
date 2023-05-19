---
title: 預期生存期值(LTV)分析（基本）
description: 瞭解如何建立分析以瞭解當前客戶的生命週期價值，並預測生命週期價值隨更多訂單的增加而如何增加。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 預期壽命值分析

預測客戶在下更多訂單時的生命週期價值是任何規模業務中最重要的方面之一。

下面是建立分析以瞭解當前客戶的生命週期價值並預測生命週期價值如何隨著訂單增加而增加的步驟。

![預期生存期](../../assets/expected_ltv_720.png)

## 構建度量

第一步是構建新度量，步驟如下：
* 導航到 **[!UICONTROL Manage Data > Metrics]**
   * 查看現有 **[!UICONTROL Avg lifetime revenue]**。

   >[!NOTE]
   >
   >此度量構建於(可能 `customer_entity` 或 `sales_order` 取決於您的商店接受來賓結帳的能力。)

   * 按一下 **[!UICONTROL Create New Metric]** 並從上面選擇表。
   * 此度量執行 **中值** 的 `Customer's lifetime revenue` 列，排序依據 `created_at`。
      * [!UICONTROL Filters]:
         * 添加 `Customers we count (Saved Filter Set)` 或 `Registered accounts we count`)
   * 為度量指定名稱，如 `Median lifetime revenue`。



## 建立儀表板

建立度量後，您可以 **建立儀表板** 通過執行以下操作：
* 導航到 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
* 為儀表板指定名稱，如 `Expected LTV`。

* 這是您建立和添加所有報告的位置。

## 生成報告

>[!NOTE]
>
>開 **[!UICONTROL Time Period:]**，每個報告的時段列為 `All-time`。 您可以隨時更改此項，以滿足分析需要。 Adobe建議此儀表板上的所有報表都涵蓋同一時間段，如 `All time`。 `Year-to-date`或 `Last 365 days`。

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加 [!UICONTROL filters]:
         * [`A`] `Customer's group code` **不等於** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **大於**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * 度量 `1`: `Avg lifetime revenue`
   * 度量 `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL圖表類型]: `Line`
   * 取消選中 `Multiple Y-Axes`

* **按訂單生存期數的LTV**
   * 度量 `1`: `Avg lifetime revenue`
   * 度量 `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL間隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL圖表類型]: `Line`
   >[!NOTE]
   >
   >不要為 `Customer's lifetime number of orders`。 相反，查看新客戶數量達到一個小數目的點，然後手動將每個客戶的生命週期訂單數量值添加到該點。 例如，如果一個訂單有200個客戶，則添加75個客戶(2),15個客戶(3)和3個客戶(4) *1、2和3*。

* 添加現有 [!UICONTROL Avg customer lifetime revenue by cohort] 報告。

生成報告後，請參閱本主題頂部的影像，瞭解如何組織儀表板上的報告。
