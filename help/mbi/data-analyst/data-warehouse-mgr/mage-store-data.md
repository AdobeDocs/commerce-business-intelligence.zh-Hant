---
title: 在Adobe Commerce中儲存資料
description: 瞭解資料如何產生、造成新列插入的原因，以及如何將動作記錄到Adobe Commerce資料庫中。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# 儲存資料於 [!DNL Adobe Commerce]

此 [!DNL Adobe Commerce] platform會記錄並整理數百個表格中的各種寶貴商業資料。 本主題說明：

* 如何產生該資料
* 導致將新列插入其中一個 [核心Commerce表格](../data-warehouse-mgr/common-mage-tables.md)
* 如何將進行購買或建立帳戶等動作記錄到 [!DNL Adobe Commerce] 資料庫

若要討論這些概念，請參閱下列範例：

`Clothes4U` 是一家同時擁有線上和實體店面的服裝零售商。 它使用 [!DNL Magento Open Source] 在其網站後收集及組織資料。

## `catalog\_product\_entity`

現在是9月22日，而且 `Clothes4U` 正在推出三個新專案至其秋季系列： `Throwback Bellbottoms`， `Straight Leg Jeans`、和 `V-Neck T-Shirts`. A `Clothes4U` 員工開啟其Commerce管理員，按一下 **[!UICONTROL Add Product]**，並輸入的所有資訊 `Throwback Bellbottoms`.

滿意的所有設定 `Throwback Bellbottoms`，員工點按 **[!UICONTROL Save]**，這會將下方的第一行插入 `catalog_product_entity` 表格。 員工重複此程式，為建立另一個Commerce產品 `Straight Leg Jeans`，然後第三個 `V-Neck T-Shirt`，將底下的第二和第三行插入 `catalog_product_entity` 表格：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id`  — 這是 `catalog_product_entity` 表格，表示表格的每一列都必須有不同的 `entity_id`. 每個 `entity_id` 在此表格上，只能與一個產品相關聯，而每個產品只能與一個產品相關聯 `entity_id`
   * 上表頂行， `entity_id` = 205，是為「Rewback Bellbottoms」建立的新列。 隨處 `entity_id` = 205出現在Commerce平台中，這指的是產品「Rewback Bellbottoms」
* `entity_type_id`  — 商務有多個物件類別（例如客戶、位址和產品，僅供少數幾個專案之用），此欄是用來表示此特定列所屬的類別。
   * 這就是 `catalog_product_entity` 表格中，每一列都有相同的實體型別： product。 在Adobe Commerce中 `entity_type_id` product為4，因此建立的所有三個新產品會針對此欄傳回4。
* `attribute_set_id`  — 屬性集是用來識別具有相同描述元的產品。
   * 表格的前兩列為 `Throwback Bellbottoms` 和 `Straight Leg Jeans` 產品，都是褲子。 這些產品會有相同的描述項（例如，名稱、內接、腰圍），因此會有相同的 `attribute_set_id`. 第三個專案， `V-Neck T-Shirt` 有不同的 `attribute_set_id` 因為沒有和褲子相同的描述項；襯衫沒有腰圍或內襯。
* `sku`  — 這些是使用者在Adobe Commerce中建立產品時指派給每個產品的唯一值。
* `created_at`  — 此欄會傳回每個產品建立時的時間戳記

## `customer\_entity`

新增三種新產品後不久，一位新客戶， `Sammy Customer`，造訪 `Clothes4U`的網站。 從 `Clothes4U` 不允許客服訂單， `Sammy Customer` 必須先在網站上建立帳戶。 客戶輸入必要的認證，然後按一下「提交」，系統就會在 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md)：

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id`  — 如同前一張表格， `entity_id` 是的主要索引鍵 `customer_entity` 表格。
   * 時間 `Sammy Customer` 已建立帳戶，且上方列已寫入 `customer_entity` 表格，客戶已指派 `entity_id` = 214. 在所有表格中，客戶識別為 `entity_id` = 214一律指使用者Sammy Customer
* `entity_type_id`  — 此資料欄會識別此表格中列出的實體型別，其功能與 `catalog_product_entity` 表格
   * 上的每一列 `customer_entity` 表格是客戶，而Commerce會將客戶定義為 `entity_type_id` 預設1
* `email`  — 此欄位由新客戶建立帳戶時輸入的電子郵件填入
* `created_at`  — 此欄傳回每個使用者加入時的時間戳記

## `sales\_flat\_order (or Sales\_order` 若您擁有 [!DNL Adobe Commerce 2.x]

帳戶建立完成後， `Sammy Customer` 已準備好開始進行購買。 在網站上，客戶新增兩組 `Throwback Bellbottoms` 和一個 `V-Neck T-Shirt` 到購物車。 對選擇感到滿意時，客戶移至結帳並提交訂單，並在 [sales flat order table （銷售平準訂單表格）](../data-warehouse-mgr/sales-flat-order-table.md)：

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id`  — 這是 `sales_flat_order` 表格。
   * 當Sammy客戶下此訂單時，上面的列已寫入 `sales_flat_order` 表格，已指派順序 `entity_id` = 227.
* `customer_id`  — 此欄是下此特定訂單之客戶的唯一識別碼
   * 此 `customer_id` 與此訂單關聯的214是Sammy客戶的 `entity_id` 於 `customer_entity` 表格。
* `subtotal`  — 此欄位是針對訂單向客戶收取的總金額
   * 兩雙「Rewback Bellbottoms」和「V領T恤」總共花費$94.85美元
* `created_at`  — 此欄會傳回建立每個訂單的時間戳記

## `sales\_flat\_order\_item ( or Sales\_order\_item`

（如果您有Commerce 2.0或更新版本）

除了 `Sales\_flat\_order` 表格，時間 `Sammy Customer` 提交訂單，該訂單中每個唯一專案的列會插入 [`sales\_flat\_order\_item` 表格](../data-warehouse-mgr/sales-flat-order-item-table.md)：

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id`  — 此欄是 `sales_flat_order_item` 表格
   * `Sammy Customer`的訂單已在此表格上建立兩個明細行，因為訂單包含兩個不同的產品
* `name`  — 此欄是產品的名稱
* `product_id`  — 此欄是此列參考之產品的唯一識別碼
   * 上面第一列有 `product_id` = 205，因為 `Throwback Bellbottoms` 具有 `entity_id` 205的 `catalog_product_entity` 表格
* `order_id`  — 此欄是 `entity_id` 包含這些特定訂單專案的訂單
   * 以上兩列都有 `order_id` = 227，因為它們都是下訂單的一部份 `Sammy Customer`，具有 `entity_id` = 227於 `sales_flat_order` 表格
* `qty_ordered`  — 此欄是包含在此特定訂單中的產品單位數
   * `Sammy Customer`的訂單包含兩對 `Throwback Bellbottoms`
* `price`  — 此欄位是訂單料號的單一單位價格
   * 此 `subtotal` 從 `Sammy Customer`中的順序 `sales_flat_order` 表格為94.85，這是兩對的 `Throwback Bellbottoms` 39.95美元/1 `V-Neck T-Shirt` 價格為$14.95美元。
