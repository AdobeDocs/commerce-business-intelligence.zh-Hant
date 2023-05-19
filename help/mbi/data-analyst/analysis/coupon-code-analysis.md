---
title: 優惠券效能
description: 瞭解分析優惠券效能。
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# 高級優惠券代碼分析

瞭解您的業務的優惠券表現是您細分訂單並更好地瞭解客戶的有趣方法。 本主題將引導您完成建立分析的步驟，以瞭解您使用優惠券獲得的客戶、他們如何執行和跟蹤一般優惠券使用情況。

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

此分析包含 [高級計算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 入門

作為第一步，您需要確保以下列已同步到您的Data Warehouse。 如果它們不是，請通過導航到 `Manage Data` > `Data Warehouse`，並同步以下內容：

* **銷售\_flat\訂單** 表
* **優惠券\_代碼**
* **基\_折扣\金額**

## 計算列

要建立的列，而不考慮來賓訂單策略：

* `sales\_flat\_order` 表
* **是否已應用優惠券？**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * 
      [!UICONTROL資料類型]: `String`
   * [!UICONTROL Calculation]:情況 `A` 然後為null `No coupon` 其他 `Coupon` 端


* **\[INPUT\]客戶\_id — 優惠券代碼**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype] 字串
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`


* **具有此優惠券的訂單數**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * 事件所有者：`INPUT customer_id - coupon code`
   * 事件級別： `created\_at`
   * [!UICONTROL Filters]: `Orders we count` 過濾器集

如果不支援來賓訂單，則要建立的附加列：

* `customer\_entity` 表
   * **客戶的第一訂單包括優惠券？ （贈券/無贈券）**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * 選擇 [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **客戶的第一訂單優惠券**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 選擇 [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **客戶使用的優惠券的使用期數**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **優惠券收購客戶或非優惠券收購客戶**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * 
         [!UICONTROL資料類型]: `String`
      * [!UICONTROL Calculation]: **當A=&#39;Coupon&#39;然後是&#39;Coupon購買客戶&#39;esle &#39;非Coupon購買客戶&#39;結束時的情況**
   * **具有優惠券的客戶訂單百分比**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * 
         [!UICONTROL資料類型]: `Decimal`
      * [!UICONTROL Calculation]: **如果A為空或B為空或B=0則為空，則A/B結束**
   * **客戶的優惠券使用情況**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * 
         [!UICONTROL資料類型]: `String`
      * [!UICONTROL Calculation]: **當A=0時A為空，當A&lt;0.5時，當A=0.5時，當A=1時，當A=1時，當A=0.5時，當A=0.5時，當A>0.5時，當A>0.5時，當Martily counipe&quot;ele&quot; else &quot; Undendendeded&quot;**









* `sales\_flat\_order` 表
   * **客戶的第一訂單包括優惠券？ （贈券/無贈券）**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 選擇 [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **客戶的第一訂單優惠券**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 選擇 [!UICONTROL column]: `Customer's first order coupon?`


如果不支援來賓訂單，則要建立的附加列：

* `sales\_flat\_order` 表
   * **客戶的第一訂單包括優惠券？ （贈券/無贈券）** **-** 由分析師建立，作為\[GOUPON ANALYSIS\]票證的一部分
   * **客戶的第一訂單優惠券**{:}**-** 由分析師建立，作為\[GOUPON ANALYSIS\]票證的一部分

* **客戶使用的優惠券的使用期數**{:}**-** 由分析師建立，作為\[GOUPON ANALYSIS\]票證的一部分
* **優惠券收購客戶或非優惠券收購客戶**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * 
      [!UICONTROL資料類型]: `String`
   * [!UICONTROL Calculation]: **當A=&#39;Coupon&#39;然後是&#39;Coupon購買客戶&#39;esle &#39;非Coupon購買客戶&#39;結束時的情況**


* **具有優惠券的客戶訂單百分比**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * 
      [!UICONTROL資料類型]: `Decimal`
   * [!UICONTROL Calculation]: **如果A為空或B為空或B=0則為空，則A/B結束**


* **客戶的優惠券使用情況**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * 
      [!UICONTROL資料類型]: `String`
   * [!UICONTROL Calculation]: **當A=0時A為空，當A&lt;0.5時，當A=0.5時，當A=1時，當A=1時，當A=0.5時，當A=0.5時，當A>0.5時，當A>0.5時，當Martily counipe&quot;ele&quot; else &quot; Undendendeded&quot;**


## 度量

* **優惠券折扣金額**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 在 `sales\_flat\_order` 表
* 此度量執行 **和**
* 在 `discount\_amount` 列
* 按 `created\_at` 時間戳
* [!UICONTROL Filter]:

* **使用的優惠券數**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 在 `sales\_flat\_order` 表
* 此度量執行 **計數**
* 在 `entity\_id` 列
* 按 `created\_at` 時間戳
* [!UICONTROL Filter]:

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 報告

* **購入優惠券及非購入優惠券之客戶百分比**
   * [!UICONTROL Metric]: `New customers`

* 度量 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 或 `Non coupon acquisition customer`
* 

   [!UICONTROL圖表類型]: `Pie`

* **購入優惠券和非購入優惠券的客戶數**
   * [!UICONTROL Metric]: `New customers`

* 指標A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 或 `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **平均生命週期收入：優惠券Acq。 （90天以上）**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * 客戶的第一訂單包括優惠券（優惠券/無優惠券）=優惠券

* 度量 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **平均生命週期收入：非優惠券Acq。 （90天以上）**
   * [!UICONTROL Metric]:平均生命週期收入
   * [!UICONTROL Filter]:
      * 客戶的第一訂單包括優惠券（優惠券/無優惠券）=無優惠券

* 度量 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **按一階優惠券列出的平均有效期收入**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 度量 `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL圖表類型]: `Column`

>[!NOTE]
>
>如果您有許多優惠券代碼，您希望應用「頂部/底部」，如按平均生存期收入排序的「前10個」

* **重複訂單概率：優惠券收購**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶的第一訂單包括優惠券（優惠券/無優惠券）=優惠券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶的第一訂單包括優惠券（優惠券/無優惠券）=優惠券
      * 客戶的最後一份訂單嗎？ =否
   * 
      [!UICONTROL公式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 從中選擇統計有效數 `Customer's by lifetime orders` 圖表。 在查看圖表時，一個好的規則是查找在桶中包含30個或更多客戶的訂單號。 根據您的資料集，這可能是一個很大的數字，因此您可以隨意添加1-10。


* 度量 `A`: `Number of orders`
* 度量 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **重複順序概率：非優惠券收購**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶的第一訂單包括優惠券（優惠券/無優惠券）=無優惠券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶的第一訂單包括優惠券（優惠券/無優惠券）=無優惠券
      * 客戶的最後一份訂單嗎？ =否
   * 
      [!UICONTROL公式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 從中選擇統計有效數 `Customer's by lifetime orders` 圖表或1-5。



* 度量 `A`: `Number of orders`
* 度量 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **購入優惠券的客戶優惠券使用率（重複訂單）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 贈券購買客戶或非贈券購買客戶=贈券購買
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號> 1
      * 客戶的第一訂單包括優惠券？ （贈券/無贈券）=贈券
   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號> 1
      * 客戶的第一訂單包括優惠券？ （贈券/無贈券）=贈券
      * 是否已應用優惠券？ （贈券/無贈券）=贈券
   * 
      [!UICONTROL公式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 度量 `A`: `Coupon-acquired customers`
* 度量 `B`: `Number of repeat orders`
* 度量 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Table` (可以轉換此表格，以便更好地進行可視化)

* **非優惠券收購客戶的優惠券使用率（重複訂單）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 贈券收購客戶或非贈券收購客戶=非贈券收購
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號> 1
      * 客戶的第一訂單包括優惠券？ （贈券/無贈券）=無贈券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號> 1
      * 客戶的第一訂單包括優惠券？ （贈券/無贈券）=無贈券
      * 是否已應用優惠券？ （贈券/無贈券）=贈券
   * 
      [!UICONTROL公式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 度量 `A`: `Non-coupon-acquired customers`
* 度量 `B`: `Number of repeat orders`
* 度量 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Table` (可以轉換此表格，以便更好地進行可視化)

* **優惠券使用詳細資訊（首次訂單）**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號= 1
      * 此優惠券的訂單數> 10
   * 
      [!UICONTROL度量]: `Revenue`
   * [!UICONTROL Filter]:
      * 客戶訂單編號= 1
      * 此優惠券的訂單數> 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 客戶訂單編號= 1
      * 此優惠券的訂單數> 10
   * [!UICONTROL Formula]: `B-C` （C為負數）;B+C（如果C為正）
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 客戶訂單編號= 1
      * 此優惠券的訂單數> 10




* 度量 `A`: `First time orders (FTO)`
* 度量 `B`: `Revenue from FTO`
* 度量 `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* 度量 `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL圖表類型]: `Table`
>[!NOTE]
>
>「具有此優惠券的訂單數」的10數量是任意的。 您可以隨意使用此篩選器的最合適數量。

* **具有贈券的訂單數（全時）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 度量 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **帶優惠券的訂單淨收入（始終）**
   * 
      [!UICONTROL度量]: `Revenue`
   * [!UICONTROL Filter]:
      * 是否已應用優惠券？ （贈券/無贈券）=贈券

* 度量 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **優惠券折扣（始終）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 度量 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **有票證和沒有票證的訂單數**
   * [!UICONTROL Metric]: `Number of orders`

* 度量 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **重複用戶之間的優惠券使用**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 客戶的生存期訂單數> 1

* 度量 `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL圖表類型]: `Pie`

* **優惠券使用詳細資訊**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * 此優惠券的訂單數> 10
   * 
      [!UICONTROL度量]: `Revenue`
   * [!UICONTROL Filter]:
      * 此優惠券的訂單數> 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 此優惠券的訂單數> 10
   * [!UICONTROL Formula]: `B-C` （如果） `C` 為負); `B+C` （如果） `C` 為正)
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` （如果） `C` 為負); `C/(B+C)` （如果） `C` 為正)
   * 

      [!UICONTROL格式]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 此優惠券的訂單數> 10
   * 
      [!UICONTROL公式]: `C/A`
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * 此優惠券的訂單數> 10





* 度量 `A`: `Number of orders`
* 度量 `B`: `Net revenue from orders`
* 度量 `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* 度量 `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* 度量 `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL圖表類型]: `Table`

>[!NOTE]
>
>「具有此優惠券的訂單數」的10數量是任意的。 您可以隨意使用此篩選器的最合適數量。

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與頁面頂部的影像相似。

如果您在構建此分析時遇到任何問題，或者只想與專業服務團隊接洽， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
