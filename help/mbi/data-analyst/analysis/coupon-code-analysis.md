---
title: 抵用券效益
description: 了解如何分析您的抵用券績效。
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# 進階抵用券代碼分析

了解企業的抵用券績效是劃分訂單的有趣方式，也能更清楚了解客戶。 本文會逐步引導您進行建立分析的步驟，以了解您透過使用抵用券取得哪些客戶、其執行方式，以及追蹤一般抵用券使用情況。

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

此分析包含 [進階計算欄](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入門

第一步，您必須確保將下列欄同步至您的Data Warehouse。 如果沒有，請導覽至「管理資料」>「Data Warehouse」，並同步下列項目，繼續進行追蹤：

* **sales\_flat\_order** 表格
* **抵用券\_代碼**
* **base\_discount\_amount**

## 計算欄

要建立的列，而不考慮來賓訂單策略：

* `sales\_flat\_order` 表格
* **訂購是否已套用抵用券？**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]::案例 `A` 則為null `No coupon` else `Coupon` 結束


* **\[INPUT\] customer\_id — 抵用券代碼**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype]::字串
   * [!UICONTROL Calculation]:: `concat(A,' - ',B)`


* **具有此抵用券的訂單數**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * 事件所有者：`INPUT customer_id - coupon code`
   * 事件排名： `created\_at`
   * [!UICONTROL Filters]: `Orders we count` 篩選集

如果不支援來賓訂單，則要建立的附加列：

* `customer\_entity` 表格
   * **客戶的首筆訂單是否包含抵用券？ （抵用券/無抵用券）**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * 選取 [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **客戶的首次訂購抵用券**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 選取 [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **使用的客戶期限抵用券數量**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **抵用券贏取客戶或非抵用券贏取客戶**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]:: **當A=「抵用券」然後「抵用券贏取客戶」其他「非抵用券贏取客戶」結束時的案例**
   * **具有抵用券的客戶訂單百分比**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * [!UICONTROL Datatype]:: `Decimal`
      * [!UICONTROL Calculation]:: **當A為Null或B為Null或B=0然後為Null時，其他A/B結尾為A/B**
   * **客戶的抵用券使用量**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]:: **當A=0，當A&lt;0.5，當A=0.5，當A=0.5，當A=1，當A=1，當A=0.5，當A=0.5，當A=0.5，當Martily coupain&#39;結尾時，當A=0.5，當A=1，當A=1，當A=0.5，當Marty coupin&#39;，則為Undefined」**









* `sales\_flat\_order` 表格
   * **客戶的首筆訂單是否包括抵用券？ （抵用券/無抵用券）**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 選取 [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **客戶的首次訂購抵用券**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 選取 [!UICONTROL column]: `Customer's first order coupon?`


如果不支援來賓訂單，則要建立的附加列：

* `sales\_flat\_order` 表格
   * **客戶的首筆訂單是否包含抵用券？ （抵用券/無抵用券）** **-** 由分析師建立，作為您\[抵用券分析\]票證的一部分
   * **客戶的首次訂購抵用券**{::}**-** 由分析師建立，作為您\[抵用券分析\]票證的一部分

* **使用的客戶期限抵用券數量**{::}**-** 由分析師建立，作為您\[抵用券分析\]票證的一部分
* **抵用券贏取客戶或非抵用券贏取客戶**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]:: **當A=「抵用券」然後「抵用券贏取客戶」其他「非抵用券贏取客戶」結束時的案例**


* **具有抵用券的客戶訂單百分比**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * [!UICONTROL Datatype]:: `Decimal`
   * [!UICONTROL Calculation]:: **當A為Null或B為Null或B=0然後為Null時，其他A/B結尾為A/B**


* **客戶的抵用券使用量**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]:: **當A=0，當A&lt;0.5，當A=0.5，當A=0.5，當A=1，當A=1，當A=0.5，當A=0.5，當A=0.5，當Martily coupain&#39;結尾時，當A=0.5，當A=1，當A=1，當A=0.5，當Marty coupin&#39;，則為Undefined」**


## 量度

* **抵用券折扣金額**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 在 `sales\_flat\_order` 表格
* 此量度會執行 **總和**
* 在 `discount\_amount` 欄
* 由 `created\_at` timestamp
* [!UICONTROL Filter]:

* **使用的抵用券數量**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 在 `sales\_flat\_order` 表格
* 此量度會執行 **計數**
* 在 `entity\_id` 欄
* 由 `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>一定要 [將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 報表

* **購入的抵用券和非抵用券的客戶百分比**
   * [!UICONTROL Metric]: `New customers`

* 量度 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 或 `Non coupon acquisition customer`
* 

   [!UICONTROL圖表類型]: `Pie`

* **獲得優惠券和非獲得優惠券的客戶數**
   * [!UICONTROL Metric]: `New customers`

* 量度A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 或 `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **平均期限收入：抵用券Acq。 （90天以上）**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * 客戶的首筆訂單包含抵用券（抵用券/無抵用券）=抵用券

* 量度 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **平均期限收入：非抵用券Acq。 （90天以上）**
   * [!UICONTROL Metric]:平均期限收入
   * [!UICONTROL Filter]:
      * 客戶的首筆訂單包含抵用券（抵用券/無抵用券）=無抵用券

* 量度 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **依首次訂購抵用券的平均期限收入**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 量度 `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL圖表類型]: `Column`

>[!NOTE]
>
>如果您有大量抵用券代碼，像我們的許多客戶一樣，您會想要套用「排名最前/最下」（例如依「平均期限」收入排序的「排名最前10」）

* **重複訂單可能性：優惠券贏取**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶的首筆訂單包含抵用券（抵用券/無抵用券）=抵用券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶的首筆訂單包含抵用券（抵用券/無抵用券）=抵用券
      * 客戶的最後訂單？ =否
   * 
      [!UICONTROL公式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 從中選擇統計顯著數 `Customer's by lifetime orders` 圖表。 查看圖表時，我們通常會尋找貯體中有30位或更多客戶的訂單編號。 視您的資料集而定，這可能是很大的數字，因此您可以自由加入1-10。


* 量度 `A`: `Number of orders`
* 量度 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **重複順序機率：非優惠券收購**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶的首筆訂單包含抵用券（抵用券/無抵用券）=無抵用券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶的首筆訂單包含抵用券（抵用券/無抵用券）=無抵用券
      * 客戶的最後訂單？ =否
   * 
      [!UICONTROL公式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 從中選擇統計顯著數 `Customer's by lifetime orders` 圖表或1-5。



* 量度 `A`: `Number of orders`
* 量度 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **獲得優惠券的客戶優惠券使用率（重複訂購）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 抵用券贏取客戶或非抵用券贏取客戶=抵用券贏取
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號> 1
      * 客戶的首筆訂單是否包含抵用券？ （抵用券/無抵用券）=抵用券
   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號> 1
      * 客戶的首筆訂單是否包含抵用券？ （抵用券/無抵用券）=抵用券
      * 訂購是否已套用抵用券？ （抵用券/無抵用券）=抵用券
   * 
      [!UICONTROL公式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 量度 `A`: `Coupon-acquired customers`
* 量度 `B`: `Number of repeat orders`
* 量度 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Table` (可以轉換此表格，以提供更理想的視覺效果)

* **非抵用券購買客戶的抵用券使用率（重複訂購）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 抵用券贏取客戶或非抵用券贏取客戶=非抵用券贏取
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號> 1
      * 客戶的首筆訂單是否包含抵用券？ （抵用券/無抵用券）=無抵用券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號> 1
      * 客戶的首筆訂單是否包含抵用券？ （抵用券/無抵用券）=無抵用券
      * 訂購是否已套用抵用券？ （抵用券/無抵用券）=抵用券
   * 
      [!UICONTROL公式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 量度 `A`: `Non-coupon-acquired customers`
* 量度 `B`: `Number of repeat orders`
* 量度 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Table` (可以轉換此表格，以提供更理想的視覺效果)

* **抵用券使用量詳細資料（首次訂購）**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客戶訂單編號= 1
      * 具有此抵用券的訂單數> 10
   * 
      [!UICONTROL量度]: `Revenue`
   * [!UICONTROL Filter]:
      * 客戶訂單編號= 1
      * 具有此抵用券的訂單數> 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 客戶訂單編號= 1
      * 具有此抵用券的訂單數> 10
   * [!UICONTROL Formula]: `B-C` （C為負數）;B+C（如果C為正）
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 客戶訂單編號= 1
      * 具有此抵用券的訂單數> 10




* 量度 `A`: `First time orders (FTO)`
* 量度 `B`: `Revenue from FTO`
* 量度 `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* 量度 `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL圖表類型]: `Table`
>[!NOTE]
>
>「具有此抵用券的訂單數」為10的數量是任意的。 請隨時使用此篩選器的最適當數量。

* **具有抵用券的訂單數（所有時間）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 量度 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **來自具有抵用券的訂單的淨收入（所有時間）**
   * 
      [!UICONTROL量度]: `Revenue`
   * [!UICONTROL Filter]:
      * 訂購是否已套用抵用券？ （抵用券/無抵用券）=抵用券

* 量度 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **優惠券折扣（所有時間）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 量度 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **具有和沒有抵用券的訂單數**
   * [!UICONTROL Metric]: `Number of orders`

* 量度 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **重複使用者的抵用券使用量**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 客戶的期限訂購數> 1

* 量度 `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL圖表類型]: `Pie`

* **抵用券使用量詳細資料**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * 具有此抵用券的訂單數> 10
   * 
      [!UICONTROL量度]: `Revenue`
   * [!UICONTROL Filter]:
      * 具有此抵用券的訂單數> 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 具有此抵用券的訂單數> 10
   * [!UICONTROL Formula]: `B-C` (如果 `C` 為負); `B+C` (如果 `C` 為正)
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (如果 `C` 為負); `C/(B+C)` (如果 `C` 為正)
   * 

      [!UICONTROL格式]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 具有此抵用券的訂單數> 10
   * 
      [!UICONTROL公式]: `C/A`
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * 具有此抵用券的訂單數> 10





* 量度 `A`: `Number of orders`
* 量度 `B`: `Net revenue from orders`
* 量度 `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* 量度 `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* 量度 `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL圖表類型]: `Table`

>[!NOTE]
>
>「具有此抵用券的訂單數」為10的數量是任意的。 請隨時使用此篩選器的最適當數量。

編譯所有報表後，您可以視需要在控制面板上組織報表。 結束結果可能看起來像頁面頂端的影像。

如果您在建立此分析時遇到任何問題，或只是想與我們的專業服務團隊接洽， [聯絡支援](../../guide-overview.md).
