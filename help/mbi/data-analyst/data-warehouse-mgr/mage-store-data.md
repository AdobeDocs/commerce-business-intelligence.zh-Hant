---
title: 在商務中儲存資料
description: 了解資料的產生方式、確切導致新列插入其中一個核心商務表格的原因，以及購買或建立帳戶等動作記錄在商務資料庫中的方式。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 3%

---

# 將資料儲存在 [!DNL Adobe Commerce]

Adobe Commerce平台可記錄並組織數百個表格中各種寶貴的商務資料。 在本主題中，您將了解該資料的產生方式，以及確切導致將新列插入其中一個 [核心商務表格](../data-warehouse-mgr/common-mage-tables.md)，以及購買或建立帳戶等動作如何記錄到商務資料庫中。 若要說明這些概念，請參閱下列範例：

`Clothes4U` 是一家線上和實體店的服裝零售商。 它使用網站背後的Magento Open Source來收集和整理資料。

## `catalog\_product\_entity`

9月22日， `Clothes4U` 會推出三個新項目至其秋季系列： `Throwback Bellbottoms`, `Straight Leg Jeans`，和 `V-Neck T-Shirts`. A `Clothes4U` 員工開啟其商務管理員，按一下 **[!UICONTROL Add Product]**，並輸入 `Throwback Bellbottoms`.

對 `Throwback Bellbottoms`，員工點按 **[!UICONTROL Save]**，會將下方的第一行插入 `catalog_product_entity` 表格。 員工重複此過程，為 `Straight Leg Jeans`，然後第三個 `V-Neck T-Shirt`，將下方的第二行和第三行插入 `catalog_product_entity` 表格：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id`  — 這是 `catalog_product_entity` 表格，表示表格的每一列都必須有不同的 `entity_id`. 每個 `entity_id` 在此表中，只能與一個產品關聯，而且每個產品只能與一個產品關聯 `entity_id`
   * 上表的頂線， `entity_id` = 205，是為「Throwback Bellbotts」建立的新行。 無論何處 `entity_id` = 205會出現在Commerce平台中，它會指的是產品「Throwback Bellbotts」
* `entity_type_id`  — 商務有多個對象類別（例如客戶、地址和產品，以及一些），此列用於表示此特定行所屬的類別。
   * 這是 `catalog_product_entity` 表格中，每一列的實體類型都相同：產品。 在Adobe Commerce, `entity_type_id` 針對產品為4，因此，此欄中所有三個新產品都會傳回4。
* `attribute_set_id`  — 屬性集用於標識具有相同描述符的產品。
   * 表格的前兩列為 `Throwback Bellbottoms` 和 `Straight Leg Jeans` 產品，都是褲子。 這些產品會有相同的描述符（例如名稱、內嵌、腰圍），因此會有相同的描述符 `attribute_set_id`. 第三項， `V-Neck T-Shirt` 有不同的 `attribute_set_id` 因為它沒有和褲子一樣的標籤；襯衫沒有馬甲或縫線。
* `sku`  — 這些是使用者在Adobe Commerce中建立新產品時，指派給每個產品的不重複值。
* `created_at`  — 此欄會傳回每個產品建立時的時間戳記

## `customer\_entity`

三款新產品，新客戶， `Sammy Customer`，瀏覽 `Clothes4U`的網站。 自 `Clothes4U` 不允許來賓訂單， `Sammy Customer` 必須先在網站上建立帳戶。 她輸入認證並按一下提交，在 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id`  — 就像前桌一樣， `entity_id` 是 `customer_entity` 表格。
   * 當 `Sammy Customer` 建立了她的帳戶，上面的一行寫入 `customer_entity` 表格，她被指派 `entity_id` = 214。 在所有表中，將客戶識別為 `entity_id` = 214一律指Sammy客戶
* `entity_type_id`  — 此列標識此表中列出的實體類型，其功能與 `catalog_product_entity` 表格
   * 在 `customer_entity` 表格將是客戶，而商務將客戶定義為 `entity_type_id` 預設為1
* `email`  — 此欄位會由新客戶建立帳戶時輸入的電子郵件填入
* `created_at`  — 此欄會傳回每位使用者加入時的時間戳記

## `sales\_flat\_order (or Sales\_order` 如果您有Commerce 2.0或更新版本)

隨著她的賬戶建立完成， `Sammy Customer` 準備開始購買。 當她瀏覽網站時，她添加了兩組 `Throwback Bellbottoms` 一 `V-Neck T-Shirt` 她的車。 她對自己的選擇感到滿意，於是開始結帳並提交訂單，在 [銷售平面訂單表](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id`  — 這是 `sales_flat_order` 表格。
   * 當Sammy客戶下此訂單時，上面的行寫入 `sales_flat_order` 表中，已分配順序 `entity_id` = 227。
* `customer_id`  — 此列是下此特定訂單的客戶的唯一標識符
   * 此 `customer_id` 與此訂單相關聯的是214，這是Sammy客戶的 `entity_id` 在 `customer_entity` 表格。
* `subtotal`  — 此列是為訂單向客戶收取的總金額
   * 這兩對「翻背褲」和「V領T恤」總共花了94.85美元
* `created_at`  — 此欄會傳回每次建立訂單時的時間戳記

## `sales\_flat\_order\_item ( or Sales\_order\_item` 如果您有Commerce 2.0或更新版本)

除了 `Sales\_flat\_order` 表格，當 `Sammy Customer` 提交訂單，該訂單中每個唯一項的行將插入到 [`sales\_flat\_order\_item` 表格](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id`  — 此欄是 `sales_flat_order_item` 表格
   * `Sammy Customer`s訂單已在此表上建立兩行，因為她的訂單包含兩個不同的產品
* `name`  — 此欄是產品的名稱
* `product_id`  — 此欄是此列引用的產品的唯一標識符
   * 上方的第一列有 `product_id` = 205，因為 `Throwback Bellbottoms` 有 `entity_id` 205年的 `catalog_product_entity` 表格
* `order_id`  — 此欄為 `entity_id` 包含這些特定訂單項的訂單
   * 以上兩列皆已 `order_id` = 227，因為它們都是 `Sammy Customer`, `entity_id` = 227 `sales_flat_order` 表格
* `qty_ordered`  — 此列是此特定訂單中包含的產品件數
   * `Sammy Customer`&#39;s順序包含2對 `Throwback Bellbottoms`
* `price`  — 此列是訂單項的單位價格
   * 此 `subtotal` 從 `Sammy Customer`的順序 `sales_flat_order` 表為94.85，即2對之和 `Throwback Bellbottoms` 39.95美元/1 `V-Neck T-Shirt` 14.95美元。
