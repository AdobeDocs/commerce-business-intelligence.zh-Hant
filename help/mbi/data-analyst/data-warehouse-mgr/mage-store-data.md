---
title: 在Adobe Commerce儲存資料
description: 瞭解資料的生成方式、插入新行的原因以及操作如何記錄到Adobe Commerce資料庫。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# 將資料儲存在 [!DNL Adobe Commerce]

的 [!DNL Adobe Commerce] 平台記錄，並跨數百個表組織各種有價值的商業資料。 本主題介紹：

* 資料的生成方式
* 導致新行插入其中一行的原因 [核心商務表](../data-warehouse-mgr/common-mage-tables.md)
* 如何將進行採購或建立帳戶等操作記錄到 [!DNL Adobe Commerce] 資料庫

要討論這些概念，請參閱以下示例：

`Clothes4U` 是一家既有線上、也有實體店的服裝零售商。 它使用 [!DNL Magento Open Source] 收集和整理資料。

## `catalog\_product\_entity`

現在是9月22日 `Clothes4U` 正在向秋季系列推出三個新項目： `Throwback Bellbottoms`。 `Straight Leg Jeans`, `V-Neck T-Shirts`。 A `Clothes4U` 員工開啟其Commerce Admin，按一下 **[!UICONTROL Add Product]**，並輸入 `Throwback Bellbottoms`。

對的所有設定都滿意 `Throwback Bellbottoms`，員工按一下 **[!UICONTROL Save]**，將下面的第一行插入 `catalog_product_entity` 的子菜單。 員工重複該過程，為其建立另一個Commerce產品 `Straight Leg Jeans`，然後是 `V-Neck T-Shirt`，將下面的第二行和第三行插入 `catalog_product_entity` 表：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id`  — 這是 `catalog_product_entity` 表，表示表的每行必須具有不同的 `entity_id`。 每個 `entity_id` 在此表中，只能與一個產品關聯，並且每個產品只能與一個產品關聯 `entity_id`
   * 上表的頂線， `entity_id` = 205，是為「Throwback Bellboonts」建立的新行。 無論何處 `entity_id` = 205出現在Commerce平台中，它指的是產品「Throwback Bellbots」
* `entity_type_id` - Commerce有多個對象類別（如客戶、地址和產品，可以命名為幾個），此列用於表示此特定行所屬的類別。
   * 這是 `catalog_product_entity` 表中，每行具有相同的實體類型：產品。 在Adobe Commerce, `entity_type_id` 對於product是4 ，因此所有三個新產品都建立為此列返回4。
* `attribute_set_id`  — 屬性集用於標識具有相同描述符的產品。
   * 表的前兩行是 `Throwback Bellbottoms` 和 `Straight Leg Jeans` 都是褲子的產品。 這些產品將具有相同的描述符（例如，名稱、inseam、馬甲），因此具有相同的描述符 `attribute_set_id`。 第三項， `V-Neck T-Shirt` 有不同的 `attribute_set_id` 因為它不會有和褲子一樣的描述；襯衫沒有腰線或內褲。
* `sku`  — 這些是用戶在Adobe Commerce建立產品時為每個產品分配的唯一值。
* `created_at`  — 此列返回建立每個產品的時間戳

## `customer\_entity`

三個新產品，新客戶剛剛推出， `Sammy Customer`訪問 `Clothes4U`首次登陸網站。 自 `Clothes4U` 不允許客人訂單， `Sammy Customer` 必須先在網站上建立帳戶。 客戶輸入所需的憑據並按一下提交，從而在 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id`  — 就像前一張桌子， `entity_id` 是 `customer_entity` 的子菜單。
   * 當 `Sammy Customer` 建立了一個帳戶，並將上面的行寫入 `customer_entity` 表，分配客戶 `entity_id` = 214。 在所有表中，客戶標識為 `entity_id` = 214始終指用戶Sammy Customer
* `entity_type_id`  — 此列標識此表中列出的實體類型，並且與 `catalog_product_entity` 表
   * 上的每一行 `customer_entity` 表是客戶，而Commerce將客戶定義為 `entity_type_id` 預設為1
* `email`  — 此欄位由新客戶在建立其帳戶時輸入的電子郵件填充
* `created_at`  — 此列返回每個用戶加入時的時間戳

## `sales\_flat\_order (or Sales\_order` 如果你 [!DNL Adobe Commerce 2.x]

帳戶建立完成後， `Sammy Customer` 準備開始購買。 在網站上，客戶添加了兩對 `Throwback Bellbottoms` 一個 `V-Neck T-Shirt` 到手推車上。 客戶對選擇感到滿意，然後將移動以結帳並提交訂單，在 [銷售平面訂單表](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id`  — 這是 `sales_flat_order` 的子菜單。
   * 當Sammy Customer下訂單時，上面的行寫入 `sales_flat_order` 表，已分配順序 `entity_id` = 227。
* `customer_id`  — 此列是下達此特定訂單的客戶的唯一標識符
   * 的 `customer_id` 與此訂單相關聯的是214，即Sammy客戶 `entity_id` 的 `customer_entity` 的子菜單。
* `subtotal`  — 此列是訂單中向客戶收取的總金額
   * 這兩雙「Throwback Bellboands」和「V領T恤」總共花費94.85美元
* `created_at`  — 此列返回建立每個訂單的時間戳

## `sales\_flat\_order\_item ( or Sales\_order\_item`

（如果您有Commerce 2.0或更高版本）

除了 `Sales\_flat\_order` 表格 `Sammy Customer` 提交順序，該順序中每個唯一項的行將插入到 [`sales\_flat\_order\_item` 表](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id`  — 此列是 `sales_flat_order_item` 表
   * `Sammy Customer`s訂單已在此表上建立兩行，因為訂單包含兩個不同的產品
* `name`  — 此列是產品的名稱
* `product_id`  — 此列是此行引用的產品的唯一標識符
   * 上面第一行 `product_id` = 205，因為 `Throwback Bellbottoms` 有 `entity_id` 205年第 `catalog_product_entity` 表
* `order_id`  — 此列是 `entity_id` 包含這些特定訂單物料的訂單
   * 上面兩行都有 `order_id` = 227，因為它們都是由 `Sammy Customer`, `entity_id` = 227 `sales_flat_order` 表
* `qty_ordered`  — 此列是包含在此特定訂單中的產品單位數
   * `Sammy Customer`s順序包含兩對 `Throwback Bellbottoms`
* `price`  — 此列是訂單物料的單位價格
   * 的 `subtotal` 從 `Sammy Customer`的順序 `sales_flat_order` 表為94.85，即兩對 `Throwback Bellbottoms` 39.95美元/張 `V-Neck T-Shirt` 14.95美元。
