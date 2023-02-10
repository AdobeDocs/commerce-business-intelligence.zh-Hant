---
title: sales_order_item表
description: 了解如何使用sales_order_item表。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# `sales_order_item` 表格

此 `sales_order_item` 表格(`sales_flat_order_item` on M1 1)包含訂單中購買的所有產品的記錄。 每一列代表一個唯一 `sku` 包含在訂單中。 為特定 `sku` 最常以 `qty_ordered` 欄位。

## 產品類型

此 `sales_order_item` 全部捕獲詳細資訊 [產品類型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 已購買。 Commerce中的常見做法是提供可設定的產品，換言之，可根據大小、顏色和其他產品屬性進行自訂的產品。 雖然可配置產品有自己的產品 `sku`，它可與多個簡單產品相關，其中每個簡單產品代表一個唯一的產品配置。 請參閱 [配置產品](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) 以取得更多資訊。

例如，請考慮可設定的產品，例如t恤。 當客戶簽出時，他們會選擇選項來更改顏色和大小。 如果客戶選取 `blue`，以及 `small`最後，他們購買了 `t-shirt-blue-small` 與 `t-shirt`.

當可設定產品依順序包含時， `sales_order_item` 表格：一個 [簡單](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`，和一個 [可配置](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 父級。 這兩條記錄 `sales_order_item` 表可通過以下連接相互關聯：

* （簡單） `sales_order_item.parent_item_id` =>（可設定） `sales_order_item.item_id`

因此，可以在簡單級別或可配置級別報告產品的銷售情況。 依預設，所有標準 `order-item-level` 量度 [!DNL MBI] 設定為排除簡單產品，而 *僅限* 報告可設定的版本。 這可透過 `Ordered products we count` 篩選器集，篩選條件為 `parent_item_id` is `NULL`.

## 公用欄

| **欄名稱** | **說明** |
|----|----|
| `base_price` | 產品在售後銷售時的單位價格 [目錄價格規則、分層折扣和特價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅、運費或購物車折扣之前，以商店的基本貨幣表示 |
| `created_at` | 訂單項的建立時間戳記，通常以UTC儲存在本地。 視您在 [!DNL MBI]，此時間戳記可轉換為 [!DNL MBI] 與資料庫時區不同 |
| `item_id` (PK) | 表的唯一標識符 |
| `name` | 訂單項的文本名稱 |
| `order_id` | `Foreign key` 與 `sales_order` 表格。 加入 `sales_order.entity_id` 確定與訂單物料關聯的訂單屬性 |
| `parent_item_id` | `Foreign key` 將簡單產品與其父產品組合或可配置產品相關聯。 加入 `sales_order_item.item_id` 確定與簡單產品關聯的父產品屬性。 對於父訂單項目（即捆綁或可配置產品類型）, `parent_item_id` 將 `NULL` |
| `product_id` | `Foreign key` 與 `catalog_product_entity` 表格。 加入 `catalog_product_entity.entity_id` 確定與訂單項目關聯的產品屬性 |
| `product_type` | 已銷售的產品類型。 潛在 [產品類型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：簡單、可配置、分組、虛擬、捆綁和可下載 |
| `qty_ordered` | 銷售時特定訂單項目在購物車中包含的件數 |
| `sku` | 已購買訂單項目的唯一標識符 |
| `store_id` | `Foreign key` 與 `store` 表格。 加入 `store.store_id` 要確定與訂單項關聯的商務商店視圖 |

{style=&quot;table-layout:auto&quot;}

## 公用計算列

| **欄名稱** | **說明** |
|---|---|
| `Customer's email` | 下訂單之客戶的電子郵件地址。 通過連接計算 `sales_order_item.order_id` to `sales_order.entity_id` 並返回 `customer_email` 欄位 |
| `Customer's lifetime number of orders` | 此客戶下的訂單總數。 通過連接計算 `sales_order_item.order_id` to `sales_order.entity_id` 並返回 `Customer's lifetime number of orders` 欄位 |
| `Customer's lifetime revenue` | 此客戶下的所有訂單的總收入。 通過連接計算 `sales_order_item.order_id` to `sales_order.entity_id` 並返回 `Customer's lifetime revenue` 欄位 |
| `Customer's order number` | 此客戶訂單的循序排名。 通過連接計算 `sales_order_item.order_id` to `sales_order.entity_id` 並返回 `Customer's order number` 欄位 |
| `Order item total value (quantity * price)` | 訂單項目在售後時的總值 [目錄價格規則、分層折扣和特價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅、運費或購物車折扣之前。 乘以 `qty_ordered` 按 `base_price` |
| `Order's coupon_code` | 套用至訂單的抵用券。 通過連接計算 `sales_order_item.order_id` to `sales_order.entity_id` 並返回 `coupon_code` 欄位 |
| `Order's increment_id` | 訂單的唯一識別碼。 通過連接計算 `sales_order_item.order_id` to `sales_order.entity_id` 並返回 `increment_id` 欄位 |
| `Order's status` | 訂單狀態。 通過連接計算 `sales_order_item.order_id` to `sales_order.entity_id` 並返回 `status` 欄位 |
| `Store name` | 與訂單項目關聯的商務商店名稱。 通過連接計算 `sales_order_item.store_id` to `store.store_id` 並返回 `name` 欄位 |

{style=&quot;table-layout:auto&quot;}

## 通用量度

| **量度名稱** | **說明** | **建築** |
|---|---|---|
| `Products ordered` | 銷售時購物車中包含的產品總數 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 在應用目錄價格規則、分層折扣和特價後，在應用任何稅、運費或購物車折扣之前，購物車中包含的產品在銷售時的總價值 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style=&quot;table-layout:auto&quot;}

## `Foreign Key` 連接路徑

`catalog_product_entity`

* 加入 `catalog_product_entity` 表格，以建立新欄，這些欄會傳回與訂單項目相關聯的產品屬性。
   * 路徑： `sales_order_item.product_id` （多個）=> `catalog_product_entity.entity_id` (1)

`sales_order`

* 加入 `sales_order` 表來建立與訂單項關聯的新訂單級列。
   * 路徑： `sales_order_item.order_id` （多個）=> `sales_order.entity_id` (1)

`sales_order_item`

* 加入 `sales_order_item` 建立將父可配置或捆綁SKU的詳細資訊與簡單產品關聯的新列。 請注意，您需要 [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 如需設定這些計算的協助，請參閱「Data Warehouse管理器」。
   * 路徑： `sales_order_item.parent_item_id` （多個）=> `sales_order_item.item_id` (1)

`store`

* 加入 `store` 表格，以建立新欄，這些欄會傳回與訂單項目相關聯的商務存放區詳細資料。
   * 路徑： `sales_order_item.store_id` （多個）=> `store.store_id` (1)
