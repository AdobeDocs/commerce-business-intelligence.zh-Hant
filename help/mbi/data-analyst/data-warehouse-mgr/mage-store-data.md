---
title: 在Adobe Commerce中儲存資料
description: 瞭解資料如何產生、造成新列插入的原因，以及如何將動作記錄到Adobe Commerce資料庫中。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# 在[!DNL Adobe Commerce]中儲存資料

[!DNL Adobe Commerce]平台會記錄並整理數百個表格中的各種寶貴商業資料。 本主題說明：

* 如何產生該資料
* 導致新資料列插入[核心Commerce資料表](../data-warehouse-mgr/common-mage-tables.md)之一的原因
* 如何將購買或建立帳戶等動作記錄到[!DNL Adobe Commerce]資料庫中

若要討論這些概念，請參閱下列範例：

`Clothes4U`是服裝retailer，具有線上和實體存在。 它在其網站後使用[!DNL Magento Open Source]來收集及組織資料。

## `catalog\_product\_entity`

現在是9月22日，且`Clothes4U`正在推出三個新專案至其秋季行： `Throwback Bellbottoms`、`Straight Leg Jeans`和`V-Neck T-Shirts`。 `Clothes4U`員工開啟其Commerce管理員、按一下「**[!UICONTROL Add Product]**」並輸入`Throwback Bellbottoms`的所有資訊。

對`Throwback Bellbottoms`的所有設定感到滿意，員工按一下&#x200B;**[!UICONTROL Save]**，這會在`catalog_product_entity`表格中插入下方的第一行。 該員工重複此程式，針對`Straight Leg Jeans`建立另一個Commerce產品，然後針對`V-Neck T-Shirt`建立第三行，將下方的第二行和第三行插入`catalog_product_entity`表格：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | 褲子10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | 褲子11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | 襯衫6 | 2016/09/22 09:24:02 |

* `entity_id` — 這是`catalog_product_entity`資料表的主索引鍵，表示資料表的每一列都必須有不同的`entity_id`。 此資料表上的每個`entity_id`只能與一個產品相關聯，而且每個產品只能與一個`entity_id`相關聯
   * 上表的頂行，`entity_id` = 205，是為「Rewback Bellbottoms」建立的新列。 `entity_id` = 205出現在Commerce平台的任何位置，指的是產品「Rewback Bellbottoms」
* `entity_type_id` - Commerce有多個物件類別（例如客戶、地址及產品等等），此欄是用來表示此特定列所屬的類別。
   * 這是`catalog_product_entity`資料表，每一列都有相同的實體型別： product。 在Adobe Commerce中，產品的`entity_type_id`為4，因此建立的所有三個新產品都會針對此欄傳回4。
* `attribute_set_id` — 屬性集是用來識別具有相同描述元的產品。
   * 表格的前兩列為`Throwback Bellbottoms`和`Straight Leg Jeans`產品，兩者均為褲子。 這些產品會有相同的描述項（例如，名稱、內接、腰圍），因此會有相同的`attribute_set_id`。 第三個專案`V-Neck T-Shirt`有不同的`attribute_set_id`，因為它沒有和褲子相同的描述元；襯衫沒有腰圍或內襯。
* `sku` — 這些是使用者在Adobe Commerce中建立產品時指派給每個產品的唯一值。
* `created_at` — 此欄會傳回每個產品建立時的時間戳記

## `customer\_entity`

新增三個新產品後不久，新客戶`Sammy Customer`首次造訪`Clothes4U`的網站。 由於`Clothes4U`不允許訪客訂單，因此`Sammy Customer`必須先在網站上建立帳戶。 客戶輸入必要的認證，然後按一下[提交]，在[`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md)上產生下列新專案：

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` — 如同先前的資料表，`entity_id`是`customer_entity`資料表的主索引鍵。
   * 當`Sammy Customer`建立帳戶，且上述資料列寫入`customer_entity`資料表時，已指派客戶`entity_id` = 214。 在所有表格中，識別為`entity_id` = 214的客戶一律會參照使用者Sammy Customer
* `entity_type_id` — 此資料行會識別此資料表中列出的實體型別，其功能與`catalog_product_entity`資料表中相同
   * `customer_entity`表格上的每一列都是客戶，Commerce預設會將客戶定義為`entity_type_id` 1
* `email` — 此欄位會由新客戶建立帳戶時輸入的電子郵件填入
* `created_at` — 此欄傳回每個使用者加入時的時間戳記

## `sales\_flat\_order (or Sales\_order` （如果您有[!DNL Adobe Commerce 2.x]）

帳戶建立完成後，`Sammy Customer`已準備好開始進行購買。 在網站上，客戶將兩組`Throwback Bellbottoms`和一個`V-Neck T-Shirt`新增到購物車。 客戶滿意您的選擇，移至結帳並提交訂單，在[銷售平準訂單表](../data-warehouse-mgr/sales-flat-order-table.md)上建立下列專案：

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` — 這是`sales_flat_order`資料表的主索引鍵。
   * 當Sammy客戶下此訂單，且將上列寫入`sales_flat_order`表格時，已指派訂單`entity_id` = 227。
* `customer_id` — 此欄是下此特定訂單之客戶的唯一識別碼
   * 與此訂單關聯的`customer_id`為214，這是`entity_id`資料表上Sammy客戶的`customer_entity`。
* `subtotal` — 此欄是針對訂單向客戶收取的總金額
   * 兩雙「Rewback Bellbottoms」和「V領T恤」總共花費$94.85美元
* `created_at` — 此欄傳回每個訂單建立時的時間戳記

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(如果您有Commerce 2.0或更新版本)

除了`Sales\_flat\_order`資料表上的單一資料列，當`Sammy Customer`提交訂單時，會將該訂單中每個唯一專案的資料列插入[`sales\_flat\_order\_item`資料表](../data-warehouse-mgr/sales-flat-order-item-table.md)中：

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` — 此資料行是`sales_flat_order_item`資料表的主索引鍵
   * `Sammy Customer`的訂單已在此資料表上建立兩行，因為訂單包含兩個不同的產品
* `name` — 此欄是產品的名稱
* `product_id` — 此欄是此列所參考之產品的唯一識別碼
   * 上方的第一列有`product_id` = 205，因為`Throwback Bellbottoms`在`entity_id`資料表上有`catalog_product_entity` / 205
* `order_id` — 此欄是包含這些特定訂單專案的訂單的`entity_id`
   * 以上兩個資料列都有`order_id` = 227，因為它們都是`Sammy Customer`所下訂單的一部分，`entity_id`資料表上有`sales_flat_order` = 227
* `qty_ordered` — 此欄是包含在此特定訂單中的產品單位數
   * `Sammy Customer`的訂單包含兩對`Throwback Bellbottoms`
* `price` — 此欄是訂單專案的單一單位價格
   * 在`subtotal`資料表中來自`Sammy Customer`順序的`sales_flat_order`為94.85，這是兩個`Throwback Bellbottoms` （每個$39.95）和1 `V-Neck T-Shirt` (1$14.95)的配對總和。
