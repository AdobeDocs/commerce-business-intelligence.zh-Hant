---
title: quote_item表
description: 了解如何使用quote_item表。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# quote_item表

此 `quote_item` 表格(`sales_flat_quote_item` on M1)1)包含新增至購物車的每個項目的記錄，無論該購物車是放棄還是轉換為購買。 每一列代表一個購物車項目。 由於此表的潛在大小，Adobe建議您在符合某些標準時（例如，如果有任何未轉換的購物車超過60天）定期刪除記錄。

>[!NOTE]
>
>只有在您未從 `quote` 和 `quote_item` 表格。 如果刪除記錄，則只能看到尚未從資料庫中刪除的購物車。

## 通用本機欄

| **欄名稱** | **說明** |
|---|---|
| `base_price` | 在將項目新增至購物車時，產品的個別單位價格，之後 [目錄價格規則、分層折扣和特價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅、運費或購物車折扣之前。 以商店的基本貨幣表示。 |
| `created_at` | 購物車項目的建立時間戳記，以UTC儲存於本機。 視您在 [!DNL MBI]，此時間戳記可轉換為 [!DNL MBI] 與資料庫時區不同 |
| `item_id` (PK) | 表的唯一標識符 |
| `name` | 訂單項的文本名稱 |
| `parent_item_id` | `Foreign key` 將簡單產品與其父產品組合或可配置產品相關聯。 加入 `quote_item.item_id` 確定與簡單產品關聯的父產品屬性。 對於父購物車項目（即捆綁或可設定的產品類型）, `parent_item_id` is `NULL` |
| `product_id` | `Foreign key` 與 `catalog_product_entity` 表格。 加入 `catalog_product_entity.entity_id` 確定與訂單項目關聯的產品屬性 |
| `product_type` | 已新增至購物車的產品類型。 潛在 [產品類型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：簡單、可配置、分組、虛擬、捆綁和可下載 |
| `qty` | 購物車中包含的特定購物車項目的件數 |
| `quote_id` | `Foreign key` 與 `quote` 表格。 加入 `quote.entity_id` 要確定與購物車項目關聯的購物車屬性 |
| `sku` | 購物車項目的唯一識別碼 |
| `store_id` | 與 `store` 表格。 加入 `store.store_id` 確定與購物車項目關聯的商務商店視圖 |

{style="table-layout:auto"}

## 公用計算列

| **欄名稱** | **說明** |
|---|---|
| `Cart creation date` | 與購物車建立日期相關聯的時間戳記。 通過連接計算 `quote_item.quote_id` to `quote.entity_id` 並返回 `created_at` timestamp |
| `Cart is active? (1/0)` | 如果購物車是由客戶建立，且尚未轉換為訂單，則布林值欄位會傳回「1」。 針對轉換的購物車或透過管理員建立的購物車傳回&quot;0&quot;。 通過連接計算 `quote_item.quote_id` to `quote.entity_id` 並返回 `is_active` 欄位 |
| `Cart item total value (qty * base_price)` | 項目新增至購物車時（之後）的項目總值 [目錄價格規則、分層折扣和特價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅、運費或購物車折扣之前。 乘以 `qty` 按 `base_price` |
| `Seconds since cart creation` | 從購物車建立日期到現在的經過時間。 通過連接計算 `quote_item.quote_id` to `quote.entity_id` 並返回 `Seconds since cart creation` 欄位 |
| `Store name` | 與訂單項目關聯的商務商店名稱。 通過連接計算 `sales_order_item.store_id` to `store.store_id` 並返回 `name` 欄位 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建築** |
|---|---|---|
| `Number of abandoned cart items` | 符合特定「放棄」條件的新增至購物車的項目總數 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>篩選器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中&quot;x&quot;對應至建立購物車後經過的時間（以秒為單位），超過該時間購物車即被視為放棄 |
| `Abandoned cart item value` | 符合特定「放棄」條件之購物車的相關總收入 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>篩選器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中&quot;x&quot;對應至建立購物車後經過的時間（以秒為單位），超過該時間購物車即被視為放棄 |

{style="table-layout:auto"}

## 外鍵連接路徑

`catalog_product_entity`

* 加入 `catalog_product_entity` 表格，以建立傳回與購物車項目相關聯的產品屬性的欄。
   * 路徑： `quote_item.product_id` （多個）=> `catalog_product_entity.entity_id` (1)

`quote`

* 加入 `quote` 表格，建立與購物車項目相關聯的新購物車層級欄。
   * 路徑： `quote_item.quote_id` （多個）=> `quote.entity_id` (1)

`quote_item`

* 加入 `quote_item` 建立將父可配置或捆綁SKU的詳細資訊與簡單產品關聯的列。 [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 如需設定這些計算的協助，請參閱「Data Warehouse管理器」。
   * 路徑： `quote_item.parent_item_id` （多個）=> `quote_item.item_id` (1)

`store`

* 加入 `store` 表格，以建立與購物車項目相關聯的商務商店相關的詳細資料欄。
   * 路徑： `quote_item.store_id` （多個）=> `store.store_id` (1)
