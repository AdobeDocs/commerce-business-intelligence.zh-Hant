---
title: quote_item table
description: Learn how to work with the quote_item table.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/wLNm1g1L6-0Ded-bZT991KvJi3dVO6zA4i2qftiX2J0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 646
ht-degree: 0%

---

# quote_item Table

The `quote_item` table (`sales_flat_quote_item` on M1) contains records on every item added to a shopping cart, whether the cart was abandoned or converted to a purchase. Each row represents one cart item. Due to the potential size of this table, Adobe recommends you periodically delete records if certain criteria are met, such as if there are any unconverted carts older than 60 days.

>[!NOTE]
>
>Analyzing historical, abandoned carts is only possible if you do not delete records from the `quote` and `quote_item` table. 如果您確實刪除記錄，則只能看到尚未從資料庫移除的購物車。

## 通用原生欄

| **資料行名稱** | **描述** |
|---|---|
| `base_price` | Price of an individual unit of a product at the time the item was added to a cart, after [catalog price rules, tiered discounts, and special pricing](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hant) are applied and before any taxes, shipping, or cart discounts are applied. 以商店的基本貨幣表示。 |
| `created_at` | Creation timestamp of the cart item, stored locally in UTC. Depending on your configuration in [!DNL Commerce Intelligence], this timestamp may be converted to a reporting time zone in [!DNL Commerce Intelligence] that differs from your database time zone |
| `item_id` (PK) | Unique identifier for the table |
| `name` | Text name of the order item |
| `parent_item_id` | 將簡單產品與其上層組合或可設定產品相關的`Foreign key`。 加入`quote_item.item_id`以決定與簡單產品相關聯的父產品屬性。 For parent cart items (that is, bundle or configurable product types), the `parent_item_id` is `NULL` |
| `product_id` | 與`Foreign key`資料表關聯的`catalog_product_entity`。 Join to `catalog_product_entity.entity_id` to determine product attributes associated with the order item |
| `product_type` | Type of product that was added to the cart. Potential [product types](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=zh-Hant#product-types) include: simple, configurable, grouped, virtual, bundle, and downloadable |
| `qty` | Quantity of units included in the cart for the particular cart item |
| `quote_id` | 與`Foreign key`資料表關聯的`quote`。 Join to `quote.entity_id` to determine cart attributes associated with the cart item |
| `sku` | Unique identifier for the cart item |
| `store_id` | 與`store`資料表相關聯的外部索引鍵。 Join to `store.store_id` to determine which Commerce store view is associated with the cart item |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Cart creation date` | Timestamp associated with the cart creation date. Calculated by joining `quote_item.quote_id` to `quote.entity_id` and returning the `created_at` timestamp |
| `Cart is active? (1/0)` | Boolean field that returns &quot;1&quot; if the cart was created by a customer and has not yet converted to an order. Returns &quot;0&quot; for converted carts, or carts created through the admin. 透過加入`quote_item.quote_id`至`quote.entity_id`並傳回`is_active`欄位進行計算 |
| `Cart item total value (qty * base_price)` | Total value of an item at the time the item was added to a cart, after [catalog price rules, tiered discounts, and special pricing](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hant) are applied and before any taxes, shipping, or cart discounts are applied. Calculated by multiplying the `qty` by the `base_price` |
| `Seconds since cart creation` | Elapsed time between the cart&#39;s creation date and now. 透過加入`quote_item.quote_id`至`quote.entity_id`並傳回`Seconds since cart creation`欄位進行計算 |
| `Store name` | 與訂單專案相關聯的Commerce商店名稱。 透過加入`sales_order_item.store_id`至`store.store_id`並傳回`name`欄位進行計算 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Number of abandoned cart items` | Total quantity of items added to carts that meet specific &quot;abandonment&quot; conditions | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filters:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, where &quot;x&quot; corresponds to the elapsed time (in seconds) since cart creation beyond which a cart is considered abandoned |
| `Abandoned cart item value` | Sum of total revenue associated with carts that meet specific &quot;abandonment&quot; conditions | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filters:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, where &quot;x&quot; corresponds to the elapsed time (in seconds) since cart creation beyond which a cart is considered abandoned |

{style="table-layout:auto"}

## Foreign Key Joining Paths

`catalog_product_entity`

* Join to `catalog_product_entity` table to create columns that return product attributes associated with the cart item.
   * 路徑： `quote_item.product_id` （許多） => `catalog_product_entity.entity_id` （一個）

`quote`

* Join to `quote` table to create new cart-level columns associated with the cart item.
   * 路徑： `quote_item.quote_id` （許多） => `quote.entity_id` （一個）

`quote_item`

* 加入`quote_item`以建立將上層可設定或套件SKU的詳細資訊與簡單產品關聯的資料行。 若是在Data Warehouse管理員中建置，請[連絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)以取得設定這些計算的協助。
   * 路徑： `quote_item.parent_item_id` （許多） => `quote_item.item_id` （一個）

`store`

* Join to `store` table to create columns that return details related to the Commerce store associated with the cart item.
   * 路徑： `quote_item.store_id` （許多） => `store.store_id` （一個）
