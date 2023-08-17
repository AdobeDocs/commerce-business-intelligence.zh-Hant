---
title: sales_order_item表格
description: 瞭解如何使用sales_order_item表格。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` 表格

此 `sales_order_item` 表格(`sales_flat_order_item` （在M1上）包含訂單中所購買所有產品的記錄。 每一列代表一個唯一 `sku` 包含在訂單中。 為特定購買的產品數量 `sku` 通常由 `qty_ordered` 欄位。

## 產品型別

此 `sales_order_item` 全部擷取詳細資料 [產品型別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 已購買的專案。 中的常見做法 [!DNL Adobe Commerce] 是提供可設定的產品，換句話說，就是可根據尺寸、顏色和其他產品屬性自訂的產品。 雖然可設定的產品有其專屬的 `sku`，它可與多個簡單產品相關，其中每個簡單產品代表一個獨特產品設定。 請參閱 [設定產品](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) 以取得詳細資訊。

例如，考慮可設定的產品，例如T恤。 客戶出庫時，會選取選項來變更顏色和大小。 如果客戶選取 `blue`，大小為 `small`，最後他們會購買類似以下的簡單產品 `t-shirt-blue-small` 這和的父產品有關 `t-shirt`.

當可設定的產品包含在訂單中時，中會產生兩個列 `sales_order_item` 表格：一個用於 [簡單](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` 一個用於 [可設定](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 父項。 這兩筆記錄位於 `sales_order_item` 表格可透過下列連線彼此關聯：

* （簡單） `sales_order_item.parent_item_id` => （可設定） `sales_order_item.item_id`

因此，您可以在簡單層次或可設定層次報告產品的銷售情況。 依預設，所有標準 `order-item-level` 中的量度 [!DNL Commerce Intelligence] 設定為排除簡單產品，以及 *僅限* 可設定版本的報告。 這是透過以下方式完成的： `Ordered products we count` 篩選器集，用於篩選條件 `parent_item_id` 是 `NULL`.

## 通用欄

| **欄名稱** | **說明** |
|----|----|
| `base_price` | 售出後個別產品單位在銷售時的價格 [目錄價格規則、分級折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅捐、運費或購物車折扣之前完成。 以商店的基本貨幣表示。 |
| `created_at` | 訂單專案的建立時間戳記，以UTC儲存在本機。 根據您在「 」中的設定 [!DNL Commerce Intelligence]，此時間戳記可能會轉換為中的報表時區 [!DNL Commerce Intelligence] 與您的資料庫時區不同的時間。 |
| `item_id` (PK) | 表格的唯一識別碼。 |
| `name` | 訂單專案的文字名稱。 |
| `order_id` | `Foreign key` 與 `sales_order` 表格。 加入 `sales_order.entity_id` 以決定與訂單料號關聯的訂單屬性。 |
| `parent_item_id` | `Foreign key` 將簡單產品與其上層搭售或可設定產品建立關聯。 加入 `sales_order_item.item_id` 以判斷與簡單產品相關的父產品屬性。 對於父訂單專案（亦即，搭售或可配置產品型別）， `parent_item_id` 是 `NULL`. |
| `product_id` | `Foreign key` 與 `catalog_product_entity` 表格。 加入 `catalog_product_entity.entity_id` 以決定與訂單料號相關聯的產品屬性。 |
| `product_type` | 售出的產品型別。 潛在 [產品型別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：簡單、可設定、分組、虛擬、組合和可下載。 |
| `qty_ordered` | 銷售時包含在購物車中特定訂單專案的單位數量。 |
| `sku` | 所購買訂單專案的唯一識別碼。 |
| `store_id` | `Foreign key` 與 `store` 表格。 加入 `store.store_id` 以判斷與訂單專案相關聯的Commerce商店檢視。 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Customer's email` | 下訂單客戶的電子郵件地址。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `customer_email` 欄位。 |
| `Customer's lifetime number of orders` | 此客戶下單的訂單總數。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `Customer's lifetime number of orders` 欄位。 |
| `Customer's lifetime revenue` | 此客戶下所有訂單的收入總和。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `Customer's lifetime revenue` 欄位。 |
| `Customer's order number` | 此客戶訂單的循序訂單排名。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `Customer's order number` 欄位。 |
| `Order item total value (quantity * price)` | 售出後訂單專案在銷售時的總值 [目錄價格規則、分級折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅捐、運費或購物車折扣之前完成。 將計算方式乘以 `qty_ordered` 依據 `base_price`. |
| `Order's coupon_code` | 適用於訂單的優惠券。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `coupon_code` 欄位。 |
| `Order's increment_id` | 訂單的唯一識別碼。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `increment_id` 欄位。 |
| `Order's status` | 訂單的狀態。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `status` 欄位。 |
| `Store name` | 與訂單專案相關聯的Commerce商店名稱。 透過加入計算 `sales_order_item.store_id` 至 `store.store_id` 並傳回 `name` 欄位。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建構** |
|---|---|---|
| `Products ordered` | 銷售時包含在購物車中的產品總數 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 在套用目錄價格規則、分層折扣和特殊定價之後，以及在套用任何稅捐、運費或購物車折扣之前，購物車中包含的產品總值 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` 聯結路徑

`catalog_product_entity`

* 加入 `catalog_product_entity` 此表格可建立傳回與訂單料號相關之產品屬性的資料欄。
   * 路徑： `sales_order_item.product_id` （許多） => `catalog_product_entity.entity_id` （一）

`sales_order`

* 加入 `sales_order` 表格，以建立與訂單專案關聯的新訂單層次資料欄。
   * 路徑： `sales_order_item.order_id` （許多） => `sales_order.entity_id` （一）

`sales_order_item`

* 加入 `sales_order_item` 建立將父項可設定或套件SKU的詳細資訊與簡單產品相關聯的欄。 [聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如需設定這些計算的協助，請在「Data Warehouse管理員」中建立。
   * 路徑： `sales_order_item.parent_item_id` （許多） => `sales_order_item.item_id` （一）

`store`

* 加入 `store` 此表格可建立傳回與訂單專案相關Commerce商店詳細資訊的欄。
   * 路徑： `sales_order_item.store_id` （許多） => `store.store_id` （一）
