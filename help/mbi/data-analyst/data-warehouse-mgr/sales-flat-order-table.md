---
title: sales_order表
description: 瞭解如何使用sales_order表。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# `sales_order` 表格

的 `sales_order` 表格`sales_flat_order` 在M1上)是捕獲每個訂單的位置。 通常，每行都代表一個唯一的順序，儘管有一些Commerce的自定義實現會導致將順序拆分為單獨的行。

此表包括所有客戶訂單，無論該訂單是否通過來賓結帳處理。 如果您的商店接受來賓結帳，您可以找到有關此的詳細資訊 [用例](../data-warehouse-mgr/guest-orders.md)。

## 公用列

| **列名** | **說明** |
|---|---|
| `base_currency_code` | 捕獲的所有值的幣種 `base_*` 欄位(即 `base_grand_total`。 `base_subtotal`等)。 這通常反映Commerce商店的預設貨幣 |
| `base_discount_amount` | 應用於訂單的折扣值 |
| `base_grand_total` | 應用所有稅、發運和折扣後，客戶在訂單上支付的最終價格。 雖然精確計算是可定製的，但通常 `base_grand_total` 按 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 訂單中所有項目的商品總值。 不包括稅、發運、折扣等 |
| `base_shipping_amount` | 應用於訂單的發運值 |
| `base_tax_amount` | 應用於訂單的稅值 |
| `billing_address_id` | `Foreign key` 與 `sales_order_address` 的子菜單。 加入到 `sales_order_address.entity_id` 確定與訂單關聯的開單地址詳細資訊 |
| `coupon_code` | 優惠券應用於訂單。 如果未應用優惠券，則此欄位為 `NULL` |
| `created_at` | 以UTC本地儲存的訂單的建立時間戳。 根據您在 [!DNL Commerce Intelligence]，此時間戳可轉換為 [!DNL Commerce Intelligence] 與資料庫時區不同 |
| `customer_email` | 下訂單的客戶的電子郵件地址。 在所有情況下都會填充此內容，包括通過來賓結帳處理的訂單 |
| `customer_group_id` | 與 `customer_group` 的子菜單。 加入到 `customer_group.customer_group_id` 確定與訂單關聯的客戶組 |
| `customer_id` | `Foreign key` 與 `customer_entity` 的下界。 加入到 `customer_entity.entity_id` 確定與訂單關聯的客戶屬性。 如果訂單是通過來賓簽出而下達的，則此欄位為 `NULL` |
| `entity_id` (PK) | 表的唯一標識符，在與Commerce實例中的其他表的聯接中常用 |
| `increment_id` | 訂單的唯一標識符，通常稱為 `order_id` 在Adobe Commerce。 的 `increment_id` 最常用於連接到外部源，如 [!DNL Google Ecommerce] |
| `shipping_address_id` | 與 `sales_order_address` 的子菜單。 加入到 `sales_order_address.entity_id` 確定與訂單關聯的發運地址詳細資訊 |
| `status` | 訂單狀態。 可以返回諸如「complete」、「processing」、「canceled」、「recanced」和在Commerce實例上實現的任何自定義狀態等值。 在處理訂單時進行更改 |
| `store_id` | `Foreign key` 與 `store` 的子菜單。 加入到 `store`。`store_id` 確定與訂單關聯的商店視圖 |

{style="table-layout:auto"}

## 公用計算列

| **列名** | **說明** |
|---|---|
| `Billing address city` | 為訂單開單城市。 通過連接計算 `sales_order`。`billing_address_id` 至 `sales_order_address`。`entity_id` 還給 `city` 場 |
| `Billing address country` | 訂單的開單國家/地區代碼。 通過連接計算 `sales_order`。`billing_address_id` 至 `sales_order_address`。`entity_id` 還給 `country_id` |
| `Billing address region` | 訂單的計費區域（通常為州或省）。 通過連接計算 `sales_order`。`billing_address_id` 至 `sales_order_address`。`entity_id` 還給 `region` 場 |
| `Customer's first order date` | 此客戶下單的第一個訂單的時間戳。 通常被視為客戶的「收購日期」。 通過返回最小值計算 `sales_order`。`created_at` 每個唯一客戶的價值 |
| `Customer's first order's billing region` | 下達訂單的客戶的購置開單區域。 通過返回 `Billing address region` 與客戶的第一訂單關聯 |
| `Customer's first order's coupon_code` | 下達此訂單的客戶的購買優惠券代碼。 通過返回 `coupon_code` 與客戶的第一訂單關聯 |
| `Customer's group code` | 下達此訂單的客戶的組名稱。 通過連接計算 `sales_order`。`customer_group_id` 至 `customer_group`。`customer_group_id` 還給 `customer_group_code` 場 |
| `Customer's lifetime number of coupons` | 應用於此客戶下達的所有訂單的優惠券總數。 計算方式為： `coupon_code` 不是 `NULL` 針對每個獨特客戶 |
| `Customer's lifetime number of orders` | 此客戶下達的訂單總數。 通過計算 `sales_order` 每個唯一客戶的表 |
| `Customer's lifetime revenue` | 此客戶下達的所有訂單的收入合計。 通過求和計算 `base_grand_total` 每個唯一客戶的所有訂單欄位 |
| `Customer's order number` | 此客戶訂單的順序排序。 通過標識客戶下達的所有訂單，並按 `created_at` 時間戳，並為每個順序分配增量整數值。 例如，客戶的第一訂單返回 `Customer's order number` 1，客戶的第二訂單返回 `Customer's order number` 2號等等。 |
| `Customer's order number (previous-current)` | 客戶上一訂單的級別與此訂單的級別級別級聯，以 `-` 字元。 通過連接(&quot;`Customer's order number` - 1&quot;，帶&quot;`-`&quot;後跟&quot;`Customer's order number`。 例如，對於與客戶的第二次採購關聯的訂單，此列返回的值為 `1-2`。 在表示兩個訂單事件之間的時間（即「訂單之間的時間」圖表中）時最常使用 |
| `Is customer's last order?` | 確定訂單是否與客戶的上一訂單或最近訂單相對應。 通過比較 `Customer's order number` 值 `Customer's lifetime number of orders`。 當這兩個欄位對於給定順序相等時，此列將返回 `Yes`;否則返回 `No` |
| `Number of items in order` | 訂單中包括的物料總數量。 通過連接計算 `sales_order`。`entity_id` 至 `sales_order_item`。`order_id` 總結 `sales_order_item`。`qty_ordered` 場 |
| `Seconds between customer's first order date and this order` | 此訂單與客戶第一訂單之間的經過時間。 通過減法計算 `Customer's first order date` 從 `created_at` 對於每個訂單，以整數秒數返回 |
| `Seconds since previous order` | 此訂單與客戶前一訂單之間的經過時間。 通過減去 `created_at` 上一訂單 `created_at` 以整數秒數返回。 例如，對於與客戶的第三訂單對應的訂單記錄，此列返回客戶的第二訂單和第三訂單之間的秒數。 對於客戶的第一個訂單，此欄位返回 `NULL` |
| `Shipping address city` | 訂單的裝運城市。 通過連接計算 `sales_order`。`shipping_address_id` 至 `sales_order_address`。`entity_id` 還給 `city` 場 |
| `Shipping address country` | 訂單的裝運國家/地區代碼。 通過連接計算 `sales_order`。`Shipping_address_id` 至 `sales_order_address`。`entity_id` 還給 `country_id` |
| `Shipping address region` | 訂單的裝運區域（通常為州或省）。 通過連接計算 `sales_order`。`shipping_address_id` 至 `sales_order_address`。`entity_id` 還給 `region` 場 |
| `Store name` | 與此訂單關聯的Commerce儲存的名稱。 通過連接計算 `sales_order`。`store_id` 至 `store`。`store_id` 還給 `name` 場 |

## 常用度量

| **度量名稱** | **說明** | **建築** |
|---|---|---|
| `Avg order value` | 每個訂單的平均收入，其中收入定義為 `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 客戶(n-1)訂單與第n訂單之間的平均時間，適用於所有客戶和訂單 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 所有訂單（其中GMV定義為小計）在應用所有稅和折扣之前的總商品價值 | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 所有客戶和訂單的客戶(n-1)訂單和第n訂單之間的中值時間 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 下達訂單總數 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 所有訂單的收入總和（其中收入定義為客戶支付的最終價格），在應用所有稅、折扣、發運等之後 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 所有訂單的發運金額總和 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 應用於所有訂單的稅總和 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 在給定報告時間間隔內下訂單的唯一客戶數。 例如，如果報表的間隔是每週，則在給定周內至少下一個訂單的每個客戶將準確計算一次，而不管他們在該周內下了多少訂單 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` 連接路徑

`customer_entity`

* 加入到 `customer_entity` 表，以建立與下訂單的客戶關聯的新客戶層列。
   * 路徑： `sales_order.customer_id` （許多）=> `customer_entity.entity_id` (1)

`customer_group`

* 加入到 `customer_group` 表，以建立可返回訂單客戶的客戶組名稱的列。
   * 路徑： `sales_order.customer_group_id` （許多）=> `customer_group.customer_group_id` (1)

`sales_order_address`

* 加入到 `sales_order_address` 表，用於建立與訂單關聯的返回開單和發運位置的列。 根據是否需要開單或發運詳細資訊，可以使用兩條連接路徑。
   * 路徑：
      * 裝運： `sales_order.shipping_address_id`（許多）=> `sales_order_address.entity_id` (1)
      * 計費： `sales_order.billing_address_id`（許多）=> `sales_order_address.entity_id` (1)

`store`

* 加入到 `store` 表格，用於建立返回與訂單關聯的Commerce儲存相關的詳細資訊的列。
   * 路徑： `sales_order.store_id` （許多）=> `store.store_id` (1)
