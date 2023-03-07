---
title: sales_order表
description: 了解如何使用sales_order表。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# `sales_order` 表格

此 `sales_order` 表格(`sales_flat_order` 在M1)，是擷取每筆訂單的位置。 雖然有些商務的自訂實施會導致將訂單分割為個別列，但每一列通常代表一個唯一順序。

此表包含所有客戶訂單，無論該訂單是否通過訪客結帳處理。 如果您的商店接受來賓結帳，您可以找到有關此的更多資訊 [使用案例](../data-warehouse-mgr/guest-orders.md).

## 公用欄

| **欄名稱** | **說明** |
|---|---|
| `base_currency_code` | 所有擷取值的貨幣 `base_*` 欄位(即 `base_grand_total`, `base_subtotal`等)。 這通常會反映商務商店的預設貨幣 |
| `base_discount_amount` | 套用至訂單的折扣值 |
| `base_grand_total` | 在應用所有稅、運費和折扣後，客戶在訂單上支付的最終價格。 雖然精確的計算方式可自訂，但一般而言， `base_grand_total` 計算方式為 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 訂單中所有項目的總商品價值。 稅、運費、折扣等均不包括在內 |
| `base_shipping_amount` | 套用至訂單的發運值 |
| `base_tax_amount` | 套用至訂單的稅值 |
| `billing_address_id` | `Foreign key` 與 `sales_order_address` 表格。 加入 `sales_order_address.entity_id` 要確定與訂單關聯的開單地址詳細資訊，請執行以下操作 |
| `coupon_code` | 套用至訂單的抵用券。 如果未套用抵用券，此欄位為 `NULL` |
| `created_at` | 建立訂單的時間戳記，以UTC儲存於本機。 視您在 [!DNL MBI]，此時間戳記可轉換為 [!DNL MBI] 與資料庫時區不同 |
| `customer_email` | 下訂單之客戶的電子郵件地址。 這會在所有情況下填入，包括透過訪客結帳處理的訂單 |
| `customer_group_id` | 與 `customer_group` 表格。 加入 `customer_group.customer_group_id` 確定與訂單關聯的客戶組 |
| `customer_id` | `Foreign key` 與 `customer_entity` 表中，如果已註冊客戶。 加入 `customer_entity.entity_id` 確定與訂單關聯的客戶屬性。 如果訂單是透過訪客結帳下達，則此欄位為 `NULL` |
| `entity_id` (PK) | 表的唯一標識符，常用於連接到Commerce實例內的其他表 |
| `increment_id` | 訂單的唯一識別碼，通常稱為 `order_id` 在Adobe Commerce。 此 `increment_id` 最常用於連接到外部源，例如 [!DNL Google Ecommerce] |
| `shipping_address_id` | 與 `sales_order_address` 表格。 加入 `sales_order_address.entity_id` 確定與訂單關聯的發運地址詳細資訊 |
| `status` | 訂單狀態。 可能會傳回「complete」、「processing」、「cancelled」、「requed」等值，以及在商務執行個體上實作的任何自訂狀態。 在處理訂單時可能會有所變更 |
| `store_id` | `Foreign key` 與 `store` 表格。 加入 `store`.`store_id` 確定與訂單關聯的商務商店視圖 |

{style="table-layout:auto"}

## 公用計算列

| **欄名稱** | **說明** |
|---|---|
| `Billing address city` | 訂單的計費城市。 通過連接計算 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 並返回 `city` 欄位 |
| `Billing address country` | 訂單的帳單國家/地區代碼。 通過連接計算 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 並返回 `country_id` |
| `Billing address region` | 訂單的計費區域（通常為州或省）。 通過連接計算 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 並返回 `region` 欄位 |
| `Customer's first order date` | 此客戶下單的首次訂單時間戳記。 通常被視為客戶的「贏取日期」。 透過傳回最小值來計算 `sales_order`.`created_at` 每個不重複客戶的價值 |
| `Customer's first order's billing region` | 下訂單的客戶的贏取帳單區域。 透過傳回 `Billing address region` 與客戶的首筆訂單關聯 |
| `Customer's first order's coupon_code` | 下此訂單之客戶的贏取抵用券代碼。 透過傳回 `coupon_code` 與客戶的首筆訂單關聯 |
| `Customer's group code` | 下此訂單的客戶的組名。 通過連接計算 `sales_order`.`customer_group_id` to `customer_group`.`customer_group_id` 並返回 `customer_group_code` 欄位 |
| `Customer's lifetime number of coupons` | 套用至此客戶下達之所有訂單的抵用券總數。 透過計算 `coupon_code` 不是 `NULL` 每個不重複客戶 |
| `Customer's lifetime number of orders` | 此客戶下的訂單總數。 透過計算 `sales_order` 每個不重複客戶的表格 |
| `Customer's lifetime revenue` | 此客戶下的所有訂單的總收入。 加總計算 `base_grand_total` 每個唯一客戶的所有訂單欄位 |
| `Customer's order number` | 此客戶訂單的循序排名。 識別客戶下的所有訂單，依 `created_at` 時間戳記，並為每個順序指派遞增的整數值。 例如，客戶的首筆訂單會傳回 `Customer's order number` 1，則客戶的二次訂單傳回 `Customer's order number` 2等。 |
| `Customer's order number (previous-current)` | 客戶先前訂單的排名與此訂單的排名串連，以 `-` 字元。 串連(&quot;`Customer's order number` - 1&quot;)`-`&quot;後跟&quot;`Customer's order number`」。 例如，對於與客戶第二次購買相關聯的訂單，此欄會傳回值為 `1-2`. 最常用於代表兩個訂單事件之間的時間（即「訂單之間的時間」圖表中） |
| `Is customer's last order?` | 確定訂單是否與客戶的最後一個訂單或最近的訂單相對應。 透過比較 `Customer's order number` 值 `Customer's lifetime number of orders`. 當這兩個欄位在指定順序中相等時，此欄會傳回「是」；否則會傳回「否」 |
| `Number of items in order` | 訂單中包含的物料總數。 通過連接計算 `sales_order`.`entity_id` to `sales_order_item`.`order_id` 和加總 `sales_order_item`.`qty_ordered` 欄位 |
| `Seconds between customer's first order date and this order` | 此訂單與客戶首次訂購之間的間隔時間。 減去計算 `Customer's first order date` 從 `created_at` 對於每個訂單，以整數秒數傳回 |
| `Seconds since previous order` | 此訂單與客戶之前訂單之間的間隔時間。 減去 `created_at` 從 `created_at` ，以整數秒數傳回。 例如，對於與客戶第三筆訂單相對應的訂單記錄，此欄會傳回客戶第二筆訂單與第三筆訂單之間的秒數。 對於客戶的首筆訂單，此欄位會傳回 `NULL` |
| `Shipping address city` | 訂貨的貨運城。 通過連接計算 `sales_order`.`shipping_address_id` to `sales_order_address`.`entity_id` 並返回 `city` 欄位 |
| `Shipping address country` | 訂單的發運國家/地區代碼。 通過連接計算 `sales_order`.`Shipping_address_id` to `sales_order_address`.`entity_id` 並返回 `country_id` |
| `Shipping address region` | 訂單的裝運地區（通常為州或省）。 通過連接計算 `sales_order`.`shipping_address_id` to `sales_order_address`.`entity_id` 並返回 `region` 欄位 |
| `Store name` | 與此訂單關聯的商務商店的名稱。 通過連接計算 `sales_order`.`store_id` to `store`.`store_id` 並返回 `name` 欄位 |

## 通用量度

| **量度名稱** | **說明** | **建築** |
|---|---|---|
| `Avg order value` | 每筆訂單的平均收入，其中收入定義為 `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 客戶(n-1)訂單與第n訂單之間的平均時間，適用於所有客戶和訂單 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 所有訂單（其中GMV定義為小計）在應用所有稅和折扣之前的總商品價值 | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 客戶(n-1)訂單與第n訂單之間的中間時間，適用於所有客戶和訂單 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 下單總數 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 所有訂單的收入總和（其中收入定義為客戶支付的最終價格，在應用所有稅、折扣、發運等之後） | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 所有訂單的發運金額總和 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 應用於所有訂單的稅總和 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 在指定報告時間間隔內下訂單的不重複客戶數。 例如，如果報表的間隔是每週，則在指定周內至少下一筆訂單的每個客戶，無論在該周內下了多少訂單，都只會計算一次 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` 連接路徑

`customer_entity`

* 加入 `customer_entity` 表格，以建立與下訂單的客戶關聯的新客戶層級欄。
   * 路徑： `sales_order.customer_id` （多個）=> `customer_entity.entity_id` (1)

`customer_group`

* 加入 `customer_group` 表格，以建立可傳回下訂單之客戶的客戶群組名稱的欄。
   * 路徑： `sales_order.customer_group_id` （多個）=> `customer_group.customer_group_id` (1)

`sales_order_address`

* 加入 `sales_order_address` 表，用於建立與訂單關聯的退貨和發貨地點的列。 根據需要計費還是發運詳細資訊，可以使用兩個連接路徑。
   * 路徑：
      * 裝運： `sales_order.shipping_address_id`（多個）=> `sales_order_address.entity_id` (1)
      * 帳單： `sales_order.billing_address_id`（多個）=> `sales_order_address.entity_id` (1)

`store`

* 加入 `store` 表格，以建立與訂單關聯的商務存放區相關的詳細資料欄。
   * 路徑： `sales_order.store_id` （多個）=> `store.store_id` (1)
