---
title: quote_item表格
description: 瞭解如何使用quote_item表格。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# quote_item表格

`quote_item`資料表（`sales_flat_quote_item`位於M1）包含每個新增至購物車的專案的記錄，無論購物車是否捨棄或轉換為購買。 每一列代表一個購物車專案。 由於此表格可能會有相當的大小，Adobe建議您在符合某些條件時（例如有任何未轉換的購物車超過60天）定期刪除記錄。

>[!NOTE]
>
>只有當您不從`quote`和`quote_item`資料表中刪除記錄時，才能分析歷史放棄的購物車。 如果您確實刪除記錄，則只能看到尚未從資料庫移除的購物車。

## 通用原生欄

| **資料行名稱** | **描述** |
|---|---|
| `base_price` | 在套用[目錄價格規則、分層折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hant)之後，以及在套用任何稅捐、運費或購物車折扣之前，將專案新增到購物車時產品的個別單位價格。 以商店的基本貨幣表示。 |
| `created_at` | 購物車專案的建立時間戳記，以UTC儲存在本機。 視您在[!DNL Commerce Intelligence]中的設定而定，此時間戳記可能會轉換為[!DNL Commerce Intelligence]中與您的資料庫時區不同的報表時區 |
| `item_id` (PK) | 表格的唯一識別碼 |
| `name` | 訂單專案的文字名稱 |
| `parent_item_id` | 將簡單產品與其上層組合或可設定產品相關的`Foreign key`。 加入`quote_item.item_id`以決定與簡單產品相關聯的父產品屬性。 對於上層購物車專案（也就是套件或可設定的產品型別），`parent_item_id`是`NULL` |
| `product_id` | 與`Foreign key`資料表關聯的`catalog_product_entity`。 加入`catalog_product_entity.entity_id`以決定與訂單專案相關聯的產品屬性 |
| `product_type` | 已新增至購物車的產品型別。 潛在的[產品型別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=zh-Hant#product-types)包括：簡單、可設定、群組、虛擬、套件組合和可下載 |
| `qty` | 特定購物車專案包含在購物車中的單位數量 |
| `quote_id` | 與`Foreign key`資料表關聯的`quote`。 加入`quote.entity_id`以決定與購物車專案相關聯的購物車屬性 |
| `sku` | 適用於購物車專案的唯一識別碼 |
| `store_id` | 與`store`資料表相關聯的外部索引鍵。 加入`store.store_id`以判斷哪個Commerce商店檢視與購物車專案相關聯 |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Cart creation date` | 與購物車建立日期相關聯的時間戳記。 將`quote_item.quote_id`加入`quote.entity_id`並傳回`created_at`時間戳記即可計算 |
| `Cart is active? (1/0)` | 如果購物車是由客戶建立且尚未轉換為訂單，則傳回「1」的布林欄位。 針對轉換後的購物車或透過管理員建立的購物車，傳回「0」。 透過加入`quote_item.quote_id`至`quote.entity_id`並傳回`is_active`欄位進行計算 |
| `Cart item total value (qty * base_price)` | 在套用[目錄價格規則、階層折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hant)之後，以及在套用任何稅捐、運費或購物車折扣之前，將專案新增至購物車時的專案總值。 計算方式為`qty`乘以`base_price` |
| `Seconds since cart creation` | 從購物車建立日期到現在之間經過的時間。 透過加入`quote_item.quote_id`至`quote.entity_id`並傳回`Seconds since cart creation`欄位進行計算 |
| `Store name` | 與訂單專案相關聯的Commerce商店名稱。 透過加入`sales_order_item.store_id`至`store.store_id`並傳回`name`欄位進行計算 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Number of abandoned cart items` | 新增到符合特定「放棄」條件的購物車的專案總數 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>篩選器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中「x」對應到自建立購物車以來經過的時間（以秒為單位），超過該時間，便視為捨棄購物車 |
| `Abandoned cart item value` | 與符合特定「放棄」條件的購物車相關聯的總收入 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>篩選器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中「x」對應於自建立購物車以來經過的時間（以秒為單位），超過該時間，便視為捨棄購物車 |

{style="table-layout:auto"}

## 外部索引鍵聯結路徑

`catalog_product_entity`

* 加入`catalog_product_entity`資料表以建立傳回與購物車專案相關聯之產品屬性的資料行。
   * 路徑： `quote_item.product_id` （許多） => `catalog_product_entity.entity_id` （一個）

`quote`

* 加入`quote`資料表以建立與購物車專案關聯的新購物車層級資料行。
   * 路徑： `quote_item.quote_id` （許多） => `quote.entity_id` （一個）

`quote_item`

* 加入`quote_item`以建立將上層可設定或套件SKU的詳細資訊與簡單產品關聯的資料行。 若是在Data Warehouse管理員中建置，請[連絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)以取得設定這些計算的協助。
   * 路徑： `quote_item.parent_item_id` （許多） => `quote_item.item_id` （一個）

`store`

* 加入`store`資料表以建立資料行，這些資料行會傳回與購物車專案相關聯的Commerce商店相關的詳細資料。
   * 路徑： `quote_item.store_id` （許多） => `store.store_id` （一個）
