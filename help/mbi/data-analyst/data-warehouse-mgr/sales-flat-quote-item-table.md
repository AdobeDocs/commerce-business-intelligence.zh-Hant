---
title: quote_item表格
description: 瞭解如何使用quote_item表格。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# quote_item表格

此 `quote_item` 表格(`sales_flat_quote_item` （在M1上）包含新增至購物車的每個專案的記錄，無論購物車是捨棄或轉換為購買。 每一列代表一個購物車專案。 由於此表格可能會有大小，Adobe建議您在符合某些條件時（例如有任何未轉換的購物車超過60天）定期刪除記錄。

>[!NOTE]
>
>只有在您不刪除記錄的情況下，才可能分析歷史放棄的購物車。 `quote` 和 `quote_item` 表格。 如果您確實刪除記錄，則只能看到尚未從資料庫移除的購物車。

## 通用原生欄

| **欄名稱** | **說明** |
|---|---|
| `base_price` | 將專案新增至購物車時，產品在之後的個別單位價格 [目錄價格規則、分級折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅捐、運費或購物車折扣之前完成。 以商店的基本貨幣表示。 |
| `created_at` | 購物車專案的建立時間戳記，以UTC儲存在本機。 根據您在「 」中的設定 [!DNL Commerce Intelligence]，此時間戳記可能會轉換為中的報表時區 [!DNL Commerce Intelligence] 與您的資料庫時區不同 |
| `item_id` (PK) | 表格的唯一識別碼 |
| `name` | 訂單專案的文字名稱 |
| `parent_item_id` | `Foreign key` 將簡單產品與其上層搭售或可設定產品建立關聯。 加入 `quote_item.item_id` 以判斷與簡單產品相關的父產品屬性。 對於上層購物車專案（即套件或可設定的產品型別），請 `parent_item_id` 是 `NULL` |
| `product_id` | `Foreign key` 與 `catalog_product_entity` 表格。 加入 `catalog_product_entity.entity_id` 以決定與訂單料號相關聯的產品屬性 |
| `product_type` | 已新增至購物車的產品型別。 潛在 [產品型別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：簡單、可設定、分組、虛擬、套件組合和可下載 |
| `qty` | 特定購物車專案包含在購物車中的單位數量 |
| `quote_id` | `Foreign key` 與 `quote` 表格。 加入 `quote.entity_id` 以決定與購物車專案相關聯的購物車屬性 |
| `sku` | 適用於購物車專案的唯一識別碼 |
| `store_id` | 與關聯的外部索引鍵 `store` 表格。 加入 `store.store_id` 以判斷哪個Commerce商店檢視與購物車專案相關聯 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Cart creation date` | 與購物車建立日期相關聯的時間戳記。 透過加入計算 `quote_item.quote_id` 至 `quote.entity_id` 並傳回 `created_at` timestamp |
| `Cart is active? (1/0)` | 如果購物車是由客戶建立且尚未轉換為訂單，則傳回「1」的布林欄位。 針對轉換後的購物車或透過管理員建立的購物車，傳回「0」。 透過加入計算 `quote_item.quote_id` 至 `quote.entity_id` 並傳回 `is_active` 欄位 |
| `Cart item total value (qty * base_price)` | 將專案新增至購物車時的專案總值，之後 [目錄價格規則、分級折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅捐、運費或購物車折扣之前完成。 將計算方式乘以 `qty` 依據 `base_price` |
| `Seconds since cart creation` | 從購物車建立日期到現在之間經過的時間。 透過加入計算 `quote_item.quote_id` 至 `quote.entity_id` 並傳回 `Seconds since cart creation` 欄位 |
| `Store name` | 與訂單專案相關聯的Commerce商店名稱。 透過加入計算 `sales_order_item.store_id` 至 `store.store_id` 並傳回 `name` 欄位 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建構** |
|---|---|---|
| `Number of abandoned cart items` | 新增到符合特定「放棄」條件的購物車的專案總數 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>篩選器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中「x」對應於自建立購物車後經過的時間（以秒為單位），超過該時間，購物車會被視為捨棄 |
| `Abandoned cart item value` | 與符合特定「放棄」條件的購物車相關聯的總收入 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>篩選器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中「x」對應於自建立購物車後經過的時間（以秒為單位），超過該時間，購物車會被視為捨棄 |

{style="table-layout:auto"}

## 外部索引鍵聯結路徑

`catalog_product_entity`

* 加入 `catalog_product_entity` 此表格可建立傳回與購物車專案相關聯之產品屬性的欄。
   * 路徑： `quote_item.product_id` （許多） => `catalog_product_entity.entity_id` （一）

`quote`

* 加入 `quote` 建立與購物車專案關聯的新購物車層級欄的表格。
   * 路徑： `quote_item.quote_id` （許多） => `quote.entity_id` （一）

`quote_item`

* 加入 `quote_item` 建立將父項可設定或套件SKU的詳細資訊與簡單產品相關聯的欄。 [聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如需設定這些計算的協助，請在「Data Warehouse管理員」中建立。
   * 路徑： `quote_item.parent_item_id` （許多） => `quote_item.item_id` （一）

`store`

* 加入 `store` 此表格可建立傳回與購物車專案相關Commerce商店詳細資訊的欄。
   * 路徑： `quote_item.store_id` （許多） => `store.store_id` （一）
