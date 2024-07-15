---
title: sales_order_item表格
description: 瞭解如何使用sales_order_item表格。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# `sales_order_item`資料表

`sales_order_item`資料表（`sales_flat_order_item`位於M1）包含訂單中購買之所有產品的記錄。 每一列代表順序中包含的唯一`sku`。 為特定`sku`購買的單位數量通常由`qty_ordered`欄位表示。

## 產品型別

`sales_order_item`會擷取已購買之所有[產品型別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types)的詳細資料。 [!DNL Adobe Commerce]的常見作法是提供可設定的產品，換句話說，就是可根據大小、顏色和其他產品屬性自訂的產品。 雖然可設定的產品有自己的`sku`，但它可以和多個簡單產品相關，其中每個簡單產品代表一個獨特的產品組態。 如需詳細資訊，請參閱[設定產品](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/)。

例如，考慮可設定的產品，例如T恤。 客戶出庫時，會選取選項來變更顏色和大小。 如果客戶選取`blue`的顏色和`small`的大小，他們最終會購買簡單產品，例如`t-shirt-blue-small`，其與`t-shirt`的上層產品有關。

當可設定的產品包含在訂單中時，`sales_order_item`表格中會產生兩個資料列：一個用於[簡單](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`，另一個用於[可設定](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html)父級。 `sales_order_item`資料表中的這兩個記錄可以透過下列聯結相互關聯：

* （簡單） `sales_order_item.parent_item_id` => （可設定） `sales_order_item.item_id`

因此，您可以在簡單層次或可設定層次報告產品的銷售情況。 根據預設，[!DNL Commerce Intelligence]中的所有標準`order-item-level`量度都設定為排除簡單產品，並且&#x200B;*僅*&#x200B;報告可設定的版本。 這是透過`Ordered products we count`篩選器集完成的，該篩選器集篩選條件`parent_item_id`為`NULL`。

## 通用欄

| **資料行名稱** | **描述** |
|----|----|
| `base_price` | 在套用[目錄價格規則、分層折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)之後，以及在套用任何稅捐、運費或購物車折扣之前，銷售時產品的個別單位價格。 以商店的基本貨幣表示。 |
| `created_at` | 訂單專案的建立時間戳記，以UTC儲存在本機。 視您在[!DNL Commerce Intelligence]中的設定而定，此時間戳記可能會轉換為[!DNL Commerce Intelligence]中與您的資料庫時區不同的報表時區。 |
| `item_id` (PK) | 表格的唯一識別碼。 |
| `name` | 訂單專案的文字名稱。 |
| `order_id` | 與`sales_order`資料表關聯的`Foreign key`。 加入`sales_order.entity_id`以決定與訂單專案相關聯的訂單屬性。 |
| `parent_item_id` | 將簡單產品與其上層組合或可設定產品相關的`Foreign key`。 加入`sales_order_item.item_id`以決定與簡單產品相關聯的父產品屬性。 對於父訂單專案（亦即套件組合或可設定的產品型別），`parent_item_id`為`NULL`。 |
| `product_id` | 與`catalog_product_entity`資料表關聯的`Foreign key`。 加入`catalog_product_entity.entity_id`以決定與訂單專案相關聯的產品屬性。 |
| `product_type` | 售出的產品型別。 潛在的[產品型別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types)包括：簡單、可設定、已分組、虛擬、套件組合和可下載。 |
| `qty_ordered` | 銷售時包含在購物車中特定訂單專案的單位數量。 |
| `sku` | 所購買訂單專案的唯一識別碼。 |
| `store_id` | 與`store`資料表關聯的`Foreign key`。 加入`store.store_id`以決定與訂單專案相關聯的Commerce商店檢視。 |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Customer's email` | 下訂單客戶的電子郵件地址。 透過加入`sales_order_item.order_id`至`sales_order.entity_id`並傳回`customer_email`欄位進行計算。 |
| `Customer's lifetime number of orders` | 此客戶下單的訂單總數。 透過加入`sales_order_item.order_id`至`sales_order.entity_id`並傳回`Customer's lifetime number of orders`欄位進行計算。 |
| `Customer's lifetime revenue` | 此客戶下所有訂單的收入總和。 透過加入`sales_order_item.order_id`至`sales_order.entity_id`並傳回`Customer's lifetime revenue`欄位進行計算。 |
| `Customer's order number` | 此客戶訂單的循序訂單排名。 透過加入`sales_order_item.order_id`至`sales_order.entity_id`並傳回`Customer's order number`欄位進行計算。 |
| `Order item total value (quantity * price)` | 在套用[目錄價格規則、分層折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)之後，以及在套用任何稅捐、運費或購物車折扣之前，訂單專案在銷售時的總值。 計算方式為`qty_ordered`乘以`base_price`。 |
| `Order's coupon_code` | 適用於訂單的優惠券。 透過加入`sales_order_item.order_id`至`sales_order.entity_id`並傳回`coupon_code`欄位進行計算。 |
| `Order's increment_id` | 訂單的唯一識別碼。 透過加入`sales_order_item.order_id`至`sales_order.entity_id`並傳回`increment_id`欄位進行計算。 |
| `Order's status` | 訂單的狀態。 透過加入`sales_order_item.order_id`至`sales_order.entity_id`並傳回`status`欄位進行計算。 |
| `Store name` | 與訂單專案相關聯的Commerce商店名稱。 透過加入`sales_order_item.store_id`至`store.store_id`並傳回`name`欄位進行計算。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Products ordered` | 銷售時包含在購物車中的產品總數 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 在套用目錄價格規則、分層折扣和特殊定價之後，以及在套用任何稅捐、運費或購物車折扣之前，購物車中包含的產品總值 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key`個加入路徑

`catalog_product_entity`

* 加入`catalog_product_entity`資料表以建立傳回與訂單專案相關聯之產品屬性的資料行。
   * 路徑： `sales_order_item.product_id` （許多） => `catalog_product_entity.entity_id` （一個）

`sales_order`

* 加入`sales_order`資料表以建立與訂單專案關聯的新訂單層級資料行。
   * 路徑： `sales_order_item.order_id` （許多） => `sales_order.entity_id` （一個）

`sales_order_item`

* 加入`sales_order_item`以建立將上層可設定或套件SKU的詳細資訊與簡單產品關聯的資料行。 如果是在Data Warehouse管理員中建置，請[連絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)以取得設定這些計算的協助。
   * 路徑： `sales_order_item.parent_item_id` （許多） => `sales_order_item.item_id` （一個）

`store`

* 加入`store`資料表以建立資料行，這些資料行會傳回與訂單專案相關聯的Commerce存放區相關的詳細資料。
   * 路徑： `sales_order_item.store_id` （許多） => `store.store_id` （一個）
