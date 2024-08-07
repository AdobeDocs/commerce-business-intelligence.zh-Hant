---
title: sales_order表格
description: 瞭解如何使用sales_order表格。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# `sales_order`資料表

`sales_order`資料表（`sales_flat_order`在M1）是擷取每個訂單的位置。 雖然Commerce有一些自訂實作，會導致將訂單分割為個別的列，但通常每一列代表一個不重複的順序。

此表格包含所有客戶訂單，無論該訂單是否透過訪客結帳處理。 如果您的商店接受訪客結帳，您可以找到有關此[使用案例](../data-warehouse-mgr/guest-orders.md)的更多資訊。

## 通用欄

| **資料行名稱** | **描述** |
|---|---|
| `base_currency_code` | 在`base_*`欄位中擷取的所有值的貨幣（即`base_grand_total`、`base_subtotal`等）。 這通常會反映Commerce商店的預設貨幣 |
| `base_discount_amount` | 套用至訂單的折扣值 |
| `base_grand_total` | 套用所有稅捐、運費和折扣後，客戶在訂單上支付的最終價格。 雖然精確計算是可自訂的，但一般`base_grand_total`的計算方式為`base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 訂單中包含之所有專案的商品總值。 不包含稅金、運費、折扣等 |
| `base_shipping_amount` | 套用至訂單的送貨值 |
| `base_tax_amount` | 套用至訂單的稅捐值 |
| `billing_address_id` | 與`sales_order_address`資料表關聯的`Foreign key`。 加入`sales_order_address.entity_id`以決定與訂單相關聯的帳單地址詳細資料 |
| `coupon_code` | 適用於訂單的優惠券。 若未套用任何抵用券，此欄位為`NULL` |
| `created_at` | 訂單的建立時間戳記，以UTC儲存在本機。 視您在[!DNL Commerce Intelligence]中的設定而定，此時間戳記可能會轉換為[!DNL Commerce Intelligence]中與您的資料庫時區不同的報表時區 |
| `customer_email` | 下訂單客戶的電子郵件地址。 所有情況下都會填入此值，包括透過訪客結帳處理的訂單 |
| `customer_group_id` | 與`customer_group`資料表相關聯的外部索引鍵。 加入`customer_group.customer_group_id`以決定與訂單相關聯的客戶群組 |
| `customer_id` | 與`customer_entity`資料表關聯的`Foreign key` （如果客戶已註冊）。 加入`customer_entity.entity_id`以決定與訂單相關聯的客戶屬性。 如果訂單是透過訪客結帳下單，則此欄位為`NULL` |
| `entity_id` (PK) | 表格的唯一識別碼，常用於聯結Commerce執行個體內其他表格 |
| `increment_id` | 訂單的唯一識別碼，在Adobe Commerce中通常稱為`order_id`。 `increment_id`最常用於聯結至外部來源，例如[!DNL Google Ecommerce] |
| `shipping_address_id` | 與`sales_order_address`資料表相關聯的外部索引鍵。 加入`sales_order_address.entity_id`以決定與訂單關聯的送貨地址詳細資料 |
| `status` | 訂單的狀態。 可能會傳回「完成」、「處理」、「已取消」、「已退款」等值，以及在Commerce執行個體上實作的任何自訂狀態。 訂單處理時可能會有所變更 |
| `store_id` | 與`store`資料表關聯的`Foreign key`。 加入`store`。`store_id`以判斷與訂單相關聯的Commerce商店檢視 |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Billing address city` | 訂單的帳單城市。 透過加入`sales_order`計算。`billing_address_id`至`sales_order_address`。`entity_id`並傳回`city`欄位 |
| `Billing address country` | 訂單的帳單國家/地區代碼。 透過加入`sales_order`計算。`billing_address_id`至`sales_order_address`。`entity_id`並傳回`country_id` |
| `Billing address region` | 訂單的帳單區域（通常為州或省）。 透過加入`sales_order`計算。`billing_address_id`至`sales_order_address`。`entity_id`並傳回`region`欄位 |
| `Customer's first order date` | 此客戶下第一個訂單的時間戳記。 通常被認為是客戶的「贏取日期」。 透過傳回最小值`sales_order`計算。每個唯一客戶的`created_at`值 |
| `Customer's first order's billing region` | 下訂單之客戶的贏取帳單區域。 傳回與客戶第一筆訂單相關聯的`Billing address region`進行計算 |
| `Customer's first order's coupon_code` | 下此訂單的客戶的贏取優惠券代碼。 傳回與客戶第一筆訂單相關聯的`coupon_code`進行計算 |
| `Customer's group code` | 下此訂單的客戶的群組名稱。 透過加入`sales_order`計算。`customer_group_id`至`customer_group`。`customer_group_id`並傳回`customer_group_code`欄位 |
| `Customer's lifetime number of coupons` | 套用至此客戶所有訂單的優惠券總數。 計算每個唯一客戶的`coupon_code`不是`NULL`的訂單數 |
| `Customer's lifetime number of orders` | 此客戶下單的訂單總數。 計算方式為計算`sales_order`表格中每個唯一客戶的列數 |
| `Customer's lifetime revenue` | 此客戶下所有訂單的收入總和。 計算方式為加總每個唯一客戶之所有訂單的`base_grand_total`欄位 |
| `Customer's order number` | 此客戶訂單的循序訂單排名。 透過識別客戶下的所有訂單、依`created_at`時間戳記依遞增順序排序，並為每個訂單指派遞增整數值進行計算。 例如，客戶的第一個訂單傳回`Customer's order number` （共1個），客戶的第二個訂單傳回`Customer's order number` （共2個），依此類推。 |
| `Customer's order number (previous-current)` | 客戶先前訂單的排名與此訂單的排名串連，以`-`字元分隔。 計算方式為將(&quot;`Customer's order number` - 1&quot;)與&quot;`-`&quot;串連，然後是&quot;`Customer's order number`&quot;。 例如，對於與客戶第二次購買相關聯的訂單，此欄會傳回`1-2`的值。 最常用於表示兩個訂單事件之間的時間（即在「訂單之間的時間」圖表中） |
| `Is customer's last order?` | 決定訂單是否對應至客戶的上次或最近訂單。 比較`Customer's order number`值與`Customer's lifetime number of orders`進行計算。 當這兩個欄位在指定的順序中相等時，此欄會傳回`Yes`；否則會傳回`No` |
| `Number of items in order` | 訂單中包含的料號總數。 透過加入`sales_order`計算。`entity_id`至`sales_order_item`。`order_id`並加總`sales_order_item`。`qty_ordered`欄位 |
| `Seconds between customer's first order date and this order` | 此訂單與客戶第一筆訂單之間的經過時間。 計算方式為從每個訂單的`created_at`中減去`Customer's first order date`，並以整數秒數傳回 |
| `Seconds since previous order` | 此訂單與客戶之前訂單之間經過的時間。 計算方式是將此順序的`created_at`減去先前順序的`created_at`，傳回為整數秒數。 例如，針對與客戶第三筆訂單相對應的訂單記錄，此欄會傳回客戶第二筆訂單與第三筆訂單之間的秒數。 對於客戶的第一筆訂單，此欄位會傳回`NULL` |
| `Shipping address city` | 訂單的送貨城市。 透過加入`sales_order`計算。`shipping_address_id`至`sales_order_address`。`entity_id`並傳回`city`欄位 |
| `Shipping address country` | 訂單的出貨國家/地區代碼。 透過加入`sales_order`計算。`Shipping_address_id`至`sales_order_address`。`entity_id`並傳回`country_id` |
| `Shipping address region` | 訂單的送貨地區（通常為州或省）。 透過加入`sales_order`計算。`shipping_address_id`至`sales_order_address`。`entity_id`並傳回`region`欄位 |
| `Store name` | 與此訂單相關聯的Commerce商店名稱。 透過加入`sales_order`計算。`store_id`至`store`。`store_id`並傳回`name`欄位 |

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Avg order value` | 每筆訂單的平均收入，其中收入定義為`base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 客戶的(n-1)訂單與所有客戶和訂單的第n筆訂單之間的平均時間 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 在套用所有稅捐與折扣之前，所有訂單的商品總值（其中GMV定義為小計） | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 適用於所有客戶和訂單的客戶(n-1)訂單與第n筆訂單之間的中位時間 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 訂購總數 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 所有訂單的收入總和，其中收入定義為客戶支付的最終價格，扣除所有稅捐、折扣、出貨等之後予以套用 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 所有訂單的出貨金額總和 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 套用至所有訂單的稅額總和 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 在指定的報告時間間隔內下訂單的不重複客戶數。 例如，如果報表的間隔為每週，則在指定周內至少下過一次訂單的每位客戶都會計算一次，無論該周內的訂單數量為何 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key`個加入路徑

`customer_entity`

* 加入`customer_entity`表格以建立與下訂單的客戶相關聯的新客戶層級欄。
   * 路徑： `sales_order.customer_id` （許多） => `customer_entity.entity_id` （一個）

`customer_group`

* 加入`customer_group`資料表以建立傳回下訂單之客戶的客戶群組名稱的資料行。
   * 路徑： `sales_order.customer_group_id` （許多） => `customer_group.customer_group_id` （一個）

`sales_order_address`

* 加入`sales_order_address`資料表以建立傳回與訂單相關之帳單與出貨地點的資料行。 視需要帳單或送貨詳細資料而定，可能會有兩個聯結路徑。
   * 路徑：
      * 送貨： `sales_order.shipping_address_id`（許多） => `sales_order_address.entity_id` （一個）
      * 帳單： `sales_order.billing_address_id`（許多） => `sales_order_address.entity_id` （一個）

`store`

* 加入`store`資料表以建立資料行，這些資料行會傳回與訂單相關聯的Commerce存放區相關的詳細資料。
   * 路徑： `sales_order.store_id` （許多） => `store.store_id` （一個）
