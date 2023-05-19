---
title: 瞭解並構建基本分析
description: 瞭解如何瞭解和構建基礎分析。
exl-id: 23cea7b3-2e66-40c3-b4bd-d197237782e3
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '3113'
ht-degree: 0%

---

# 基本分析

一旦你熟悉了 [!DNL Adobe Commerce Intelligence] 平台，並且對工具有基本的瞭解，您將要開始生成報告。 你最常問的一個問題是&quot;我該看什麼？&quot;

以下資訊概括了您可能認為有價值的一些常用度量和報告。 有些報告存在於您的帳戶中，因此請確保您查看了帳戶中存在的度量和報告以避免建立重複項。

## 要瞭解的表和列

在構建度量時，您需要瞭解四條資訊：

1. 資料所在的表格，
1. 要執行的特定操作，
1. 要對和執行該操作的列
1. 要用於跟蹤該資料的時間戳。

最有可能的是，這些示例中使用的表的名稱與資料庫中的列和表名稱稍有不同，因為每個資料庫都是唯一的。 如果需要幫助來識別資料庫中的相應表或列，請參考以下定義。

## 客戶表

此表包含有關每個客戶的關鍵資訊，如唯一的客戶ID、電子郵件地址等。 以下示例使用 **[!UICONTROL customer_entity]** 示例customer表的名稱。

如果資料庫中當前不存在這些計算中的某些計算，則帳戶中的任何管理員用戶都可以生成這些計算。 此外，您還要確保這些維可對所有適用度量進行分組。

**Dimension**

* **[!UICONTROL Entity_id]**:每個客戶的唯一標識符。 這也可能是唯一的客戶編號或客戶電子郵件地址，它應作為訂單表的參考密鑰。
* **[!UICONTROL Created_at]**:建立客戶帳戶並將其添加到資料庫的日期。
* **[!UICONTROL Customer's lifetime revenue]**:客戶生成的總生命週期收入。
* **[!UICONTROL Customer's first 30-day revenue]**:客戶在其頭30天中產生的收入總額。
* **[!UICONTROL Customer's lifetime number of orders]**:客戶在其生命週期內下達的訂單數。
* **[!UICONTROL Customer's lifetime number of coupons]**:客戶在其一生中使用的優惠券總數。
* **[!UICONTROL Customer's first order date]**:客戶第一次訂單的日期。 如果客戶在建立時未下訂單，則此日期可能與createdat日期不同。

**你接受客人的命令嗎？**

*如果是，則此表可能不包含您的所有客戶。 聯繫 [支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 確保客戶分析包括所有客戶。*

*不確定你是否接受客人訂單？ 請參閱 [此主題](../data-warehouse-mgr/guest-orders.md) 來瞭解更多資訊。*

## 訂單表

在此表中，每行代表一個順序。 此表中的列包含有關每個訂單的基本資訊，如訂單的ID、建立日期、狀態、下達訂單的客戶的ID等。 以下示例使用 **[!UICONTROL sales_flat_order]** 命令。

**Dimension**

* **[!UICONTROL Customer_id]**:下達訂單的客戶的唯一標識符。 這通常用於在客戶表和訂單表之間移動資訊。 在這些示例中，您期望在 **[!UICONTROL sales_flat_order]** 與對齊的表 **[!UICONTROL entitiy_id]** 的 **[!UICONTROL customer_entity]** 的子菜單。
* **[!UICONTROL Created_at]**:建立或下達訂單的日期。
* **[!UICONTROL Customer_email]**:下訂單的客戶的電子郵件地址。 這也可能是客戶的唯一標識符。
* **[!UICONTROL Customer's lifetime number of orders]**:在上具有相同名稱的列的副本 `Customers` 的子菜單。
* **[!UICONTROL Customer's order number]**:與訂單關聯的客戶順序訂單編號。 例如，如果您正在查看的行是客戶的第一訂單，則此列為「1」；但是，如果這是客戶的第15個訂單，則此列顯示此訂單的「15」。 如果您的 `Customers` 表格 [支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 來幫你建造它。
* **[!UICONTROL Customer's order number (previous-current)]**:中兩個值的串聯 **[!UICONTROL Customer's order number]** 的雙曲餘切值。 在下面的示例報告中使用它來顯示任意兩個訂單之間的已用時間。 例如，客戶的第一訂單日期與其第二訂單日期之間的時間表示為「1-2」，並使用此計算。
* **[!UICONTROL Coupon_code]**:顯示每個訂單上使用的優惠券。
* **[!UICONTROL Seconds since previous order]**:客戶訂單之間的時間（秒）。

## 訂單項表

在此表中，每行都表示已銷售的一個物料。 此表包含有關每個訂單中銷售的物料的資訊，如訂單參考編號、產品編號、數量等。 以下示例使用 `sales_flat_order_item` 示例訂單項表的名稱。

**Dimension**

* **[!UICONTROL Item_id]**:表中每行的唯一標識符。
* **[!UICONTROL Order_id]**:您的引用鍵 `Orders` 表，它告訴您按相同順序購買了哪些物料。 如果訂單包含多個項，則重複此值。
* **[!UICONTROL Product_id]**:如果您想要有關所購買的特定產品的資訊（如顏色、大小等），則可以使用此列從產品表中提取此資訊。
* **[!UICONTROL Order's created_at]**:下單的時間戳，通常複製到 `order line items` 表格 `Orders` 的子菜單。
* **[!UICONTROL Order's coupon_code]**:與 `Order's created_at` 維，此列從您的訂單表中複製。

## 預訂表

此表用於管理您的訂閱資訊，如訂閱ID、訂閱者的電子郵件地址、訂閱開始日期等。

**Dimension**

* **[!UICONTROL Customer_id]**:下達訂單的客戶的唯一標識符。 這是在Customers表和Orders表之間構建路徑的常用方法。 在這些示例中，您期望在 **sales_flat_order** 與對齊的表 `entitiy_id` 的 `customer_entity` 的子菜單。
* **[!UICONTROL Start date]**:客戶訂閱的開始日期。

## 市場營銷支出表

在分析您的營銷支出時，您可以包括 [!DNL Facebook]。 [!DNL Google AdWords]或分析中的其他源。 如果您有多個市場營銷支出來源，請與 [Managed Services隊](https://business.adobe.com/products/magento/fully-managed-service.html) 幫助您設定市場營銷活動的合併表。

**Dimension**

* **[!UICONTROL Spend]**:廣告總支出。 在 [!DNL Facebook]，這是 `facebook_ads_insights_####` 的子菜單。 對於 [!DNL Google AdWords]這是 `adCost` 列 `campaigns####` 的子菜單。
* 的 `####` 附加到這些表中的每個表的帳戶ID [!DNL Facebook] 或 [!DNL Google AdWords] 帳戶。
* **[!UICONTROL Clicks]**:點擊總數。 在 [!DNL Facebook]，這是 `facebook_ads_insights_####` 的子菜單。 在 [!DNL Google AdWords]，這是 `campaigns####` 的子菜單。
* **[!UICONTROL Impressions]**:印象總數。 在 [!DNL Facebook]，這是在 `facebook_ads_insights_####` 的子菜單。 在 [!DNL Google AdWords]這樣就會是 `campaigns####` 的子菜單。
* **[!UICONTROL Campaign]**:點擊總數。 在 [!DNL Facebook]，這將是 `facebook_ads_insights_####` 的子菜單。 在 [!DNL Google AdWords]，這將是 `campaigns####` 的子菜單。
* **[!UICONTROL Date]**:特定市場活動的活動（支出、點擊或印象）發生的時間和日期。 在 [!DNL Facebook]這是 `date_start` 列 `facebook_ads_insights_####` 的子菜單。 在 [!DNL Google AdWords]，這將是 `campaigns####` 的子菜單。
* **[!UICONTROL Customer's first order's source]**:訂單的來源來自客戶的第一訂單。 首先，檢查您是否有一列 `customer's first order's source` 你的賬戶。 如果未看到此列，則可以使用這些說明建立所需的列。
* **[!UICONTROL Customer's first order's medium]**:客戶第一訂單中訂單的介質。 首先，檢查您是否有一列 `customer's first order's source` 你的賬戶。 如果未看到此列，則可以使用這些說明建立所需的列。
* **[!UICONTROL Customer's first order's campaign]**:客戶第一訂單的訂單促銷活動。 首先，檢查您是否有一列 `customer's first order's source` 你的賬戶。 如果未看到此列，則可以使用這些說明建立所需的列。

## 常見報告和度量

以下是一些報告和度量的常見示例，您可能會發現這些示例非常有用：

* [客戶分析](#customeranalytics)
* [訂單分析](#orderanalytics)
* [營銷支出分析](#mktgspendanalytics)

## 客戶分析 {#customeranalytics}

### 新用戶

* **說明**:指定期間內新獲取用戶總數的計數。 `New Users` 不同於 `Unique Customers`，因為 `New Users` 具有使用您的服務建立帳戶的時間戳（這並不表示他們必須下訂單） `Unique Customers` 已經下了至少一個訂單。
* **度量定義**:此度量執行 **計數** 共 `entity_id` 從 `customer_entity` 表排序 `created_at`。
* **報表示例**:上個月建立的新用戶數
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Time Range]**: `Last Month`
   * **[!UICONTROL Time Interval]**: `By Day`

![新用戶](../../assets/New_Users_Last_Month.png)<!--{: width="929"}-->

### 獨特的客戶

* **說明**:指定期間內不同客戶總數的計數。 這與 `New Users`，因為它只跟蹤至少下了一個訂單的客戶。 不同客戶的報告在給定時間間隔內只跟蹤一次客戶。 如果將時間間隔設定為 `By Day` 當天客戶進行一次以上的購買，客戶只被計數一次。 如果要查看總採購數，請查看 `Number of Orders`。
* **度量定義**:此度量執行 **非重複計數** 共 `customer_id` 從 `sales_flat_order` 表排序 `created_at`。
* **報表示例**:過去90天中按周分列的不同客戶
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving range > Last 90 Days`
   * **[!UICONTROL Time Interval]**: `By Day`

![獨特的客戶。](../../assets/Unique_customers_last_7_days.png)<!--{: width="929"}-->

### 新訂戶

* **說明**:在指定期間內新購用戶總數的計數。
* **度量定義**:此度量執行 **非重複計數** 共 `customer_id` 從 `subscriptions` 表排序 `start_date`。
* **報表示例**:今年按月新增訂戶
   * **[!UICONTROL Metric]**: `New Subscribers`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 0 Days Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

![訂閱者](../../assets/New_Subscribers_This_Year_by_Month.png)<!--{: width="929"}-->

### 重複客戶

* **說明**:在一個期間內下了多個訂單的客戶總數。 在重複客戶報表中，您可以 `Distinct Customers` 度量和 `Customer's Order Number` 維 `orders` 的子菜單。
* **使用的度量**: `Distinct Customers`
* **報表示例**:去年第2次和第3次採購的數量
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving Range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's Order Number`，然後選擇 `2` 和 `3`

   ![](../../assets/2nd_and_3rd_purchases_last_year.png)

* **報告示例2**:去年的重複客戶數
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Filters]**: `Customer's Order Number Greater Than 1`
   * **[!UICONTROL Time Range]**: `Moving range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`

   ![去年重複客戶](../../assets/Repeat_customers_last_year.png)<!--{: width="929"}-->

### 按訂單生存期數列出的頂級客戶

* **說明**:根據訂單總數列出的頂級客戶清單。 這將直接列出您最頻繁的購物者。
* **使用的度量**: `Orders`
* **報表示例**:按訂單生存期數列出的25大客戶
   * **[!UICONTROL Metric]**: `Orders`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top/Bottom]**:按訂單排序的前25位

   ![按訂單列出的25大客戶](../../assets/Top_25_customers_by_lifetime_orders.png)<!--{: width="929"}-->

### 按終身收入劃分的頂級客戶

* **說明**:基於終身收入的頂級客戶清單。
* **使用的度量**: `Average Lifetime Revenue`
* **報表示例**:按終身收入劃分的25大客戶
   * **[!UICONTROL Metric]**: `Average Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top Bottom]**:前25位按Lifetime收入排序

   ![按收入劃分的25大客戶](../../assets/top_25_customers_by_lifetime_revneue.png)<!--{: width="929"}-->

### 按群組劃分的平均終身收入

* **說明**:跟蹤 [不同群體的平均壽命收入](../dev-reports/lifetime-rev-cohort-analysis.md) 確定效能最高的組。 按公用日期（如第一訂單日期或建立日期）分組。
* **使用的度量**: `Revenue`
* **報表示例**:按隊列列出的平均客戶壽命收入
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Cohort Date]**: `Customer's first order date`
   * **[!UICONTROL Time Interval]**: `Month`
   * **[!UICONTROL Time Period]**:最近8個組的移動組，至少包含4個月的資料
   * **[!UICONTROL Duration]**: `12 Month(s)`
   * **[!UICONTROL Table]**: `Customer_entity`
   * **[!UICONTROL Perspective]**:每個隊列成員的累計平均值

   ![按隊列列出的客戶生命週期收入](../../assets/Avg_customer_lifetime_revenue_by_cohort.png)<!--{: width="929"}-->

### 按優惠券使用情況劃分的客戶

* **說明**:已使用優惠券/折扣代碼的已購買客戶數目的計數。 這可以幫助你清楚地瞭解你的折扣購買者和全價購買者。
* **使用的度量**: `New Users`
* **報表示例**:按月分類的優惠券和非優惠券客戶
   * **[!UICONTROL Metric A]**: `Non coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**:超過0的客戶的有效期訂單數和等於0的客戶有效期優惠券數
   * **[!UICONTROL Metric B]**: `Coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**:客戶生存期訂單數大於0，客戶生存期優惠券數大於0
   * **[!UICONTROL Time range]**: `All Time`
   * **[!UICONTROL Time interval]**: `By Month`

   ![按優惠券使用率列出的客戶](../../assets/Customers_by_coupon_usage.png)<!--{: width="929"}-->

* **報告示例2**:按月的優惠券和非優惠券客戶百分比
   * **[!UICONTROL Metric A]**: `Non coupon customers` （隱藏度量）
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customer's Lifetime Number of Orders Greater Than 0` 和 `Customer's Lifetime Number of Coupons Equal to 0`
   * **[!UICONTROL Metric B]**: `Coupon customers`
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customers Lifetime Number of Orders Greater Than 0` 和 `Customer's Lifetime Number of Coupons Greater Than 0`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Formula]**: `B/(A+B)`

>[!NOTE]
>
> **隱藏所有度量**

![優惠券使用](../../assets/Customers_by_coupon_usage_formula.png)<!--{: width="929"}-->

### 前30天平均收入

* **說明**:客戶作為客戶於其首30日內產生之平均收入金額。
* **度量說明**:此度量執行 **平均** 共 `Customer's First 30 Day Revenue` 從 `customer_entity` 表排序 `created_at`。
* **報表說明**:客戶首個30天收入的全時平均值
* **[!UICONTROL Metric]**: `Average First 30 Day Revenue`
* **[!UICONTROL Time Range]**: `All Time`
* **[!UICONTROL Time Interval]**: `None`

![前30天平均收入](../../assets/Avg_first_30_day_revenue.png)<!--{: width="929"}-->

### 平均客戶生命週期收入

* **說明**:客戶在其有生之年中產生的平均收入金額。
* **度量說明**:此度量執行 **平均** 的 `Customer's Lifetime Revenue` 列 `customer_entity` 基於 `created_at`。
* **報表說明**:客戶終身收入的全時平均值
   * **[!UICONTROL Metric]**: `Average Customer Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`

![客戶生存期收入](../../assets/Avd_customer_lifetime_revenue_.png)<!--{: width="929"}-->

## 訂單分析 {#orderanalytics}

### 收入

* **說明**:收入度量顯示選定時間期內的總收入。
* 此度量執行 **總和** 共 `grand_total` 從 `sales_flat_order` 表排序 `created_at`。
* **報表示例**:按月收入，YTD
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **時間間隔**: `By Month`

>[!TIP]
>
>確保收入指標的計算與內部討論的定義一致。 例如，您可能需要計算已發運訂單的收入、折換不同區域的幣種或排除稅。 另外，您可以 [篩選器集](../../data-user/reports/ess-manage-data-filters.md) 確保在同一表上構建的所有度量的一致性。

![收入](../../assets/revenue.png)<!--{: width="929"}-->

### 訂單

* **說明**:指定期間內訂單總數的計數。 訂單報表跟蹤由新產品產品、促銷或任何可能增加（或減少）交易量的其他因素引起的訂單量變化。 您可能經常希望通過一些變數來劃分此度量以回答您的問題。
* **度量定義**:此度量執行 **計數** 共 `entity_id` 從 `sales_flat_order` 表排序 `created_at`。
* **報表示例**:按月訂單，YTD
   * **[!UICONTROL Metric]**: `number of orders`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

>[!TIP]
>
>和收入指標一樣，你應該 [篩選器集](../../data-user/reports/ess-manage-data-filters.md) 排除未完成、test或退貨訂單。

![訂單](../../assets/orders_pic.png)<!--{: width="929"}-->

### 訂購的產品

* **說明**:訂購的產品度量告訴您在特定時間段內銷售的物料數量。
* **度量定義**:此度量執行 **總和** 共 `qty_ordered` 從 `sales_flat_order_item` 表排序 `created_at`。
* **報表示例**:按月銷售的物料，YTD
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

   ![訂購的產品](../../assets/products_ordered_pic1.png)<!--{: width="929"}-->

* 將此度量與訂單數度量結合，以計算每個訂單的物料數。 接下來，將優惠券代碼添加到報表中，以確定促銷如何影響購物車大小，或按新訂單與重複訂單細分，以更好地瞭解客戶行為。
* **報表示例**:每訂單產品：第一訂單與重複訂單
   * **[!UICONTROL Metric A]**:訂購的產品：先
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric B]**:訂單：先
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric C]**:訂購的產品：重複訂單
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Metric D]**:訂單：重複訂單
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Week`
   * **[!UICONTROL Formula 1]**: `A/B`
   * **[!UICONTROL Formula 2]**: `C/D`

>[!NOTE]
>
>取消選中 `Multiple Y-Axes box` 和 `Hide` 所有度量

![訂購的產品2](../../assets/products_ordered_pic2.png)<!--{: width="929"}-->

### 平均訂單值

* **說明**:跟蹤在某個期間內下達的訂單的平均值。 使用此指標可快速確定平均訂單值(AOV)因您的營銷工作、產品提供和/或業務中的其他更改而波動的情況。
* **度量定義**:此度量執行 **平均** 共 `grand_total` 從 `sales_flat_order` 表排序 `created_at`。
* **報表示例**:AOV與上一年(YTD)
   * **[!UICONTROL Metric]**: `Average order value`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Perspective]**: `Amount Change vs Previous Year`

   ![AOV](../../assets/aov_pic.png)<!--{: width="929"}-->

### 最多使用優惠券購買的產品

* **說明**:此報表可讓您深入瞭解在您提供促銷或優惠券時銷售哪些產品。
* **使用的度量**:訂購的產品
* **報表示例**:最多使用優惠券購買的產品
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Filter]**: `Order's coupon_code Is Not \[NULL\]`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By**]: `name` 或 `SKU`，或任何其他產品標識符)
   * **[!UICONTROL Show top/bottom]**:按訂購產品排序的前25位

   ![帶優惠券的產品](../../assets/prod_coupons_pic.png)<!--{: width="929"}-->

### 訂單間的時間

* **說明**:Test您對客戶購買週期的假設和期望， **訂單間時間** 平均值（或中值！）的分析 兩次採購之間的時間。 在下圖中，您可以看到您的最佳客戶 — 那些下訂單超過三個的客戶 — 在不到6個月的時間內進行了第二次購買。 未下第四份訂單的客戶等待14個月後再進行第二次購買。
* **度量定義**:此度量執行 **平均** 共 `Time since previous order` 從 `sales_flat_order` 排序 `created_at`。
* **報表示例**:
   * **度量1**:≤ 3訂單
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders ≤ 3`
   * **度量2**:> 3個訂單
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders > 3`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**:` Customer's order number (previous-current)`

>[!NOTE]
>
>取消選中 `Multiple Y-Axes` 框。

![訂單間時間](../../assets/time_bw_orders_pic.png)<!--{: width="929"}-->

## 營銷支出分析 {#mktgspendanalytics}

### 廣告支出

* **說明**:您可以按市場活動或廣告集或其它細分來分析不同時段和間隔的市場營銷支出。
* **度量定義**:此度量對中的支出列執行總和 `Marketing Spend` 按順序排列的表 `date` 的雙曲餘切值。
* **報表示例**:按市場活動列出的廣告支出
   * **[!UICONTROL Metric]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `campaign`

![廣告支出](../../assets/ad_spend.png)<!--{: width="929"}-->

### 廣告印象和廣告點擊

* **說明**:除了分析廣告支出外，您還可以分析廣告印象和廣告點擊量。
* **度量定義**:此度量對中的印數（或按一下）列執行總和 `Marketing Spend` 按日期列排序的表。
* **報表示例**:按天添加印象和廣告點擊量
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 3 Months Ago`
   * **[!UICONTROL Time Interval]**: `By Day`

   ![廣告印象](../../assets/ad_impressions.png)<!--{: width="929"}-->

### 點擊率(CTR)

* **說明**:使用上面建立的廣告印象和廣告點擊量度，您可以根據不同的市場活動隨時間而分析點擊率。
* **報表示例**:按市場活動分列的CTR
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**:`All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * 選擇 `%` 的雙曲餘切值。
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>你可以 **標題** 公式為 `CTR`, **隱藏** 所有指標。

![CTR](../../assets/CTR.png)<!--{: width="929"}-->

### 每按一下成本(CPC)

* **說明**:使用上面建立的廣告支出和廣告按一下量度，您可以根據不同的市場活動隨時間而分析每次按一下的成本。
* **報表示例**:各戰役中國共產黨
   * **[!UICONTROL Metric A]**: `Ad spend`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `A/B`
   * 選擇 `currency` 選項
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>你可以 **標題** 公式為 `CPC`, **隱藏** 所有指標。

![中共](../../assets/CPC.png)<!--{: width="929"}-->

### 按採購來源劃分的客戶

* **說明**:如果您使用 [!DNL Google eCommerce]，您可以根據客戶的購買來源來分析客戶。 這有助於您確定哪些市場營銷來源正在獲取客戶，並回答諸如「您的大多數客戶是通過 [!DNL Google]。 [!DNL Facebook]或其他來源&quot;
* **報表示例**:按採購來源劃分的客戶
   * **[!UICONTROL Metric Used]**: `New Customers`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's first order's source`

>[!NOTE]
>
>簽出 [這篇文章](../analysis/most-value-source-channel.md) 的子常式。

![獲取源](../../assets/acquisition_source.png)<!--{: width="929"}-->

### 按收購媒介和收購活動劃分的客戶

* **說明**:與按採購來源分析客戶類似，您還可以按客戶的第一訂單的介質和市場活動分析客戶。 這可以幫助您回答諸如「哪些市場活動正在吸引新客戶？」之類的問題。
* **報表示例**:按採購市場活動列出的客戶
   * **[!UICONTROL Metric Used]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>用於 `New Customers` metric，您可以為業務添加其它被視為「付費」媒介的媒介，如cpc或付費搜索。

![獲取介質](../../assets/acquisition_medium.png)<!--{: width="929"}-->

### 客戶購置成本(CAC)或每次購置成本(CPA)

* **說明**:分析市場活動成本的一種方法是，將所有成本僅分配給通過市場活動獲得的客戶。
* **報表示例**:各活動CAC
   * **[!UICONTROL Metric A]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Ad Spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * 選擇 `currency` 選項
   * **[!UICONTROL Group By]**:
      * 對於度量 `A`選中 `Customer's first order's campaign`
      * 對於度量 `B`選中 `campaign`

   ![新用戶。](../../assets/New_Users_Last_Month.png)

>[!NOTE]
>
>你可以 **標題** 公式為 `CTR`, **隱藏** 所有指標。 另外，請查看 [這篇文章](../analysis/roi-ad-camp.md) 的子菜單。

![CAC 1](../../assets/New_Users_Last_Month.png)

![CAC 2](../../assets/cac-2.png)

### 按獲取來源、中介和市場活動列出的生存期價值

* **說明**:除了分析每個市場活動獲得的客戶數量外，您還可以分析這些客戶的平均生命週期收入。 這有助於您識別：
   * 如果某些活動吸引了大量客戶，但這些客戶的生命週期價值較低。
   * 如果某些活動吸引的客戶數量較少，但這些客戶具有較高的生命週期價值。
* **報表示例**:首先添加 `New customers` 度量。 然後，添加 `Average lifetime revenue` 度量。 選擇所需的時間範圍，然後選擇 `interval` 如 `None`。 最後，選擇 `group by` 選項`Customer's first order's campaign`。
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` 類似「%google%」
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` 類似「%google%」
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>對於這兩個篩選器，您可以添加任何其它被視為業務「付費」介質的介質（例如cpc或付費搜索）。 您還可以添加要分析的任何其它來源，如Facebook。 簽出 [這篇文章](../analysis/roi-ad-camp.md) 詳細資訊。

![按獲取來源、中介和市場活動列出的生存期價值](../../assets/LTV_2.png)<!--{: width="929"}-->

### 投資回報(ROI)

* **說明**:按市場活動計算ROI的一種方法是分析通過市場活動下達的所有訂單。 然而，另一種方法是分析通過市場活動獲得的客戶的生命週期價值。 要分析ROI，市場活動名稱必須在您的支出資料和事務性資料中保持一致。 如果建立以下報表，並且由於市場活動名稱不匹配而不存在ROI值，則可能需要查看 [UTM標籤](../../best-practices/utm-tagging-google.md) 你已經實施了。
* **報表示例**:按市場活動列出的ROI
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` 類似「%google%」
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` 類似「%google%」
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric C]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `(B-(C/A))/(C/A)`
   * 選擇 `% `選項
   * **[!UICONTROL Group By]**:
      * 對於度量 `A` 和 `B`選中 `Customer's first order's campaign`
      * 對於度量 `C`選中 `campaign`

>[!NOTE]
>
>您可以將公式標為「ROI」，並隱藏所有度量。 此外，還可以調整度量中的篩選器以分析替代源和介質。 另外，請查看 [此主題](../analysis/roi-ad-camp.md) 詳細資訊。

![ROI 1](../../assets/ROI_1.png)<!--{: width="929"}-->

![ROI 2](../../assets/ROI_2.png)<!--{: width="929"}-->
