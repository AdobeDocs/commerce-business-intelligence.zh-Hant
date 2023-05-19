---
title: quote_item表
description: 瞭解如何使用quote_item表。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# quote_item表

的 `quote_item` 表格`sales_flat_quote_item` 在M1)中，包含添加到購物車的每件物品的記錄，包括購物車是已放棄還是已轉換為採購。 每行代表一個購物車物料。 由於此表的潛在大小，Adobe建議您在滿足某些條件時定期刪除記錄，例如，如果有任何未轉換的購物車超過60天。

>[!NOTE]
>
>只有在不從中刪除記錄時，才可以分析歷史的已放棄操作站 `quote` 和 `quote_item` 的子菜單。 如果確實刪除了記錄，則只能查看尚未從資料庫中刪除的購物車。

## 通用本機列

| **列名** | **說明** |
|---|---|
| `base_price` | 在將物料添加到購物車時，產品的單位價格 [目錄價格規則、分層折扣和特價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 應用所有稅、發運或購物車折扣之前。 此值以商店的基本貨幣表示。 |
| `created_at` | 以UTC本地儲存的購物車項目的建立時間戳。 根據您在 [!DNL Commerce Intelligence]，此時間戳可轉換為 [!DNL Commerce Intelligence] 與資料庫時區不同 |
| `item_id` (PK) | 表的唯一標識符 |
| `name` | 訂單項的文本名稱 |
| `parent_item_id` | `Foreign key` 將簡單產品與其父捆綁或可配置產品相關聯。 加入到 `quote_item.item_id` 確定與簡單產品關聯的父產品屬性。 對於父購物車項目（即捆綁或可配置產品類型）, `parent_item_id` 是 `NULL` |
| `product_id` | `Foreign key` 與 `catalog_product_entity` 的子菜單。 加入到 `catalog_product_entity.entity_id` 確定與訂單物料關聯的產品屬性 |
| `product_type` | 添加到購物車的產品類型。 潛在 [產品類型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：簡單、可配置、分組、虛擬、捆綁和可下載 |
| `qty` | 購物車中包含的特定購物車物料的數量 |
| `quote_id` | `Foreign key` 與 `quote` 的子菜單。 加入到 `quote.entity_id` 確定與購物車物料關聯的購物車屬性 |
| `sku` | 購物車物料的唯一標識符 |
| `store_id` | 與 `store` 的子菜單。 加入到 `store.store_id` 確定與購物車物料關聯的商店視圖 |

{style="table-layout:auto"}

## 公用計算列

| **列名** | **說明** |
|---|---|
| `Cart creation date` | 與購物車建立日期關聯的時間戳。 通過連接計算 `quote_item.quote_id` 至 `quote.entity_id` 還給 `created_at` 時間戳 |
| `Cart is active? (1/0)` | 如果購物車是由客戶建立的，並且尚未轉換為訂單，則返回「1」的布爾欄位。 返回「0」，表示已轉換的操作站或通過管理員建立的操作站。 通過連接計算 `quote_item.quote_id` 至 `quote.entity_id` 還給 `is_active` 場 |
| `Cart item total value (qty * base_price)` | 在將物料添加到購物車時，物料的總值 [目錄價格規則、分層折扣和特價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 應用所有稅、發運或購物車折扣之前。 通過乘以 `qty` 的 `base_price` |
| `Seconds since cart creation` | 從購物車的建立日期到現在的已用時間。 通過連接計算 `quote_item.quote_id` 至 `quote.entity_id` 還給 `Seconds since cart creation` 場 |
| `Store name` | 與訂單項關聯的Commerce商店的名稱。 通過連接計算 `sales_order_item.store_id` 至 `store.store_id` 還給 `name` 場 |

{style="table-layout:auto"}

## 常用度量

| **度量名稱** | **說明** | **建築** |
|---|---|---|
| `Number of abandoned cart items` | 添加到符合特定「放棄」條件的購物車的物料總數 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>篩選器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中「x」與自建立購物車後（超過此時間被視為已放棄購物車）的已用時間（以秒為單位）相對應 |
| `Abandoned cart item value` | 與滿足特定「放棄」條件的車輛關聯的總收入 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>篩選器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中「x」與自建立購物車後（超過此時間被視為已放棄購物車）的已用時間（以秒為單位）相對應 |

{style="table-layout:auto"}

## 外鍵連接路徑

`catalog_product_entity`

* 加入到 `catalog_product_entity` 表格，用於建立返回與購物車物料關聯的產品屬性的列。
   * 路徑： `quote_item.product_id` （許多）=> `catalog_product_entity.entity_id` (1)

`quote`

* 加入到 `quote` 表，以建立與購物車物料關聯的新購物車級列。
   * 路徑： `quote_item.quote_id` （許多）=> `quote.entity_id` (1)

`quote_item`

* 加入到 `quote_item` 建立將父可配置或捆綁SKU的詳細資訊與簡單產品關聯的列。 [聯繫支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果在Data Warehouse管理器中生成，則可獲得配置這些計算的幫助。
   * 路徑： `quote_item.parent_item_id` （許多）=> `quote_item.item_id` (1)

`store`

* 加入到 `store` 表格，用於建立返回與購物車物料關聯的Commerce儲存相關的詳細資訊的列。
   * 路徑： `quote_item.store_id` （許多）=> `store.store_id` (1)
