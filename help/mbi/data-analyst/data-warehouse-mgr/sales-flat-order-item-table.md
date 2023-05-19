---
title: sales_order_item表
description: 瞭解如何使用sales_order_item表。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` 表格

的 `sales_order_item` 表格`sales_flat_order_item` M1)包含按訂單購買的所有產品的記錄。 每行代表一個唯一 `sku` 包含在訂單中。 為特定對象採購的單位數量 `sku` 通常由 `qty_ordered` 的子菜單。

## 產品類型

的 `sales_order_item` 捕獲所有詳細資訊 [產品類型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 是被買來的。 在 [!DNL Adobe Commerce] 即提供可配置產品，或者換句話說，提供可根據大小、顏色和其他產品屬性進行定製的產品。 儘管可配置產品有其自己的 `sku`，它可以與多個簡單產品相關，其中每個簡單產品都表示一個唯一的產品配置。 請參閱 [配置產品](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) 的子菜單。

例如，請考慮可配置的產品，如T恤衫。 當客戶簽出時，他們會選擇選項來更改顏色和大小。 如果客戶選擇的顏色 `blue`，以及 `small`他們最後買了一個簡單的產品 `t-shirt-blue-small` 它與 `t-shirt`。

當可配置產品按順序包含時， `sales_order_item` 表：一個 [簡單](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` 一個 [可配置](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 父項。 這兩條記錄 `sales_order_item` 表可通過以下連接相互關聯：

* （簡單） `sales_order_item.parent_item_id` =>（可配置） `sales_order_item.item_id`

因此，可以在簡單級別或可配置級別報告產品的銷售情況。 預設情況下，所有標準 `order-item-level` 度量 [!DNL Commerce Intelligence] 配置為排除簡單產品， *僅* 報告可配置版本。 這是通過 `Ordered products we count` 篩選器集，該篩選器在 `parent_item_id` 是 `NULL`。

## 公用列

| **列名** | **說明** |
|----|----|
| `base_price` | 產品在售後時的單位價格 [目錄價格規則、分層折扣和特價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 應用所有稅、發運或購物車折扣之前。 此值以商店的基本貨幣表示。 |
| `created_at` | 以UTC本地儲存的訂單項的建立時間戳。 根據您在 [!DNL Commerce Intelligence]，此時間戳可轉換為 [!DNL Commerce Intelligence] 與資料庫時區不同。 |
| `item_id` (PK) | 表的唯一標識符。 |
| `name` | 訂單項的文本名稱。 |
| `order_id` | `Foreign key` 與 `sales_order` 的子菜單。 加入到 `sales_order.entity_id` 確定與訂單物料關聯的訂單屬性。 |
| `parent_item_id` | `Foreign key` 將簡單產品與其父捆綁或可配置產品相關聯。 加入到 `sales_order_item.item_id` 確定與簡單產品關聯的父產品屬性。 對於父訂單項（即捆綁或可配置產品類型）, `parent_item_id` 是 `NULL`。 |
| `product_id` | `Foreign key` 與 `catalog_product_entity` 的子菜單。 加入到 `catalog_product_entity.entity_id` 確定與訂單物料關聯的產品屬性。 |
| `product_type` | 已銷售的產品類型。 潛在 [產品類型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：簡單、可配置、分組、虛擬、捆綁和可下載。 |
| `qty_ordered` | 在銷售時特定訂單物料的購物車中包含的單位數量。 |
| `sku` | 採購的訂單物料的唯一標識符。 |
| `store_id` | `Foreign key` 與 `store` 的子菜單。 加入到 `store.store_id` 確定與訂單項關聯的Commerce儲存視圖。 |

{style="table-layout:auto"}

## 公用計算列

| **列名** | **說明** |
|---|---|
| `Customer's email` | 下訂單的客戶的電子郵件地址。 通過連接計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 還給 `customer_email` 的子菜單。 |
| `Customer's lifetime number of orders` | 此客戶下達的訂單總數。 通過連接計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 還給 `Customer's lifetime number of orders` 的子菜單。 |
| `Customer's lifetime revenue` | 此客戶下達的所有訂單的收入合計。 通過連接計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 還給 `Customer's lifetime revenue` 的子菜單。 |
| `Customer's order number` | 此客戶訂單的順序排序。 通過連接計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 還給 `Customer's order number` 的子菜單。 |
| `Order item total value (quantity * price)` | 銷售後訂單物料的總值 [目錄價格規則、分層折扣和特價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 應用所有稅、發運或購物車折扣之前。 通過乘以 `qty_ordered` 的 `base_price`。 |
| `Order's coupon_code` | 應用於訂單的優惠券。 通過連接計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 還給 `coupon_code` 的子菜單。 |
| `Order's increment_id` | 訂單的唯一標識符。 通過連接計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 還給 `increment_id` 的子菜單。 |
| `Order's status` | 訂單的狀態。 通過連接計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 還給 `status` 的子菜單。 |
| `Store name` | 與訂單項關聯的Commerce商店的名稱。 通過連接計算 `sales_order_item.store_id` 至 `store.store_id` 還給 `name` 的子菜單。 |

{style="table-layout:auto"}

## 常用度量

| **度量名稱** | **說明** | **建築** |
|---|---|---|
| `Products ordered` | 銷售時包含在購物車中的產品總數 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 在應用目錄價格規則、分層折扣和特殊定價之後，以及在應用任何稅、發運或購物車折扣之前，在銷售時包含在購物車中的產品總值 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` 連接路徑

`catalog_product_entity`

* 加入到 `catalog_product_entity` 表格，用於建立返回與訂單物料關聯的產品屬性的列。
   * 路徑： `sales_order_item.product_id` （許多）=> `catalog_product_entity.entity_id` (1)

`sales_order`

* 加入到 `sales_order` 表，以建立與訂單項關聯的新訂單層列。
   * 路徑： `sales_order_item.order_id` （許多）=> `sales_order.entity_id` (1)

`sales_order_item`

* 加入到 `sales_order_item` 建立將父可配置或捆綁SKU的詳細資訊與簡單產品關聯的列。 [聯繫支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果在Data Warehouse管理器中生成，則可獲得配置這些計算的幫助。
   * 路徑： `sales_order_item.parent_item_id` （許多）=> `sales_order_item.item_id` (1)

`store`

* 加入到 `store` 表格，用於建立返回與與訂單項關聯的Commerce儲存相關的詳細資訊的列。
   * 路徑： `sales_order_item.store_id` （許多）=> `store.store_id` (1)
