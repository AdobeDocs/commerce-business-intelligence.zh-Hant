---
title: 報價表
description: 了解如何使用報價表。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 報價表

此 `quote` 表格(`sales_flat_quote` on M1)包含您商店中建立之每個購物車的記錄，無論這些記錄是放棄或轉換為購買。 每一列代表一個購物車。 由於此表的潛在大小，Adobe建議您在符合某些標準時（例如，如果有任何未轉換的購物車超過60天）定期刪除記錄。

>[!NOTE]
>
>只有在您未從 `quote` 表格。 如果刪除記錄，則只能看到尚未從資料庫中刪除的購物車。

## 通用本機欄

| **欄名稱** | **說明** |
|---|---|
| `base_currency_code` | 所有擷取值的貨幣 `base_*` 欄位(即 `base_grand_total`, `base_subtotal`等)。 這通常會反映商務商店的預設貨幣 |
| `base_grand_total` | 在套用所有稅、運費和折扣後，向客戶報價的購物車最終價格。 雖然精確的計算方式可自訂，但一般而言， `base_grand_total` 計算方式為 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 購物車中所包含所有項目的商品總值。 稅、運費、折扣等均不包括在內 |
| `created_at` | 購物車的建立時間戳記，以UTC儲存於本機。 視您在 [!DNL MBI]，此時間戳記可轉換為 [!DNL MBI] 與資料庫時區不同 |
| `customer_email` | 建立購物車之客戶的電子郵件地址 |
| `customer_id` | `Foreign key` 與 `customer_entity` 表中，如果已註冊客戶。 加入 `customer_entity.entity_id` 以決定與建立購物車的使用者相關聯的客戶屬性。 如果購物車是透過訪客結帳建立，則此欄位為 `NULL` |
| `entity_id` (PK) | 表的唯一標識符，常用於連接到Commerce實例內的其他表 |
| `is_active` | 如果購物車是由客戶建立，且尚未轉換為訂單，則布林值欄位會傳回「1」。 針對轉換的購物車或透過管理員建立的購物車傳回&quot;0&quot; |
| `items_qty` | 購物車中包含的所有項目的總數量 |
| `reserved_order_id` | `Foreign key` 與 `sales_order` 表格。 加入 `sales_order.increment_id` 以確定與轉換的購物車相關聯的訂單詳細資訊。 若購物車未與轉換的訂單相關聯，則 `reserved_order_id` 保留 `NULL` |
| `store_id` | `Foreign key` 與 `store` 表格。 加入 `store`.`store_id` 確定與購物車關聯的商務商店視圖 |

{style="table-layout:auto"}

## 公用計算列

| **欄名稱** | **說明** |
|---|---|
| `Order date` | 反映轉換購物車訂單建立日期的時間戳記。 通過連接計算 `quote.reserved_order_id` to `sales_order.increment_id` 並返回 `sales_order.created_at` 欄位 |
| `Seconds between cart creation and order` | 從購物車建立到訂單建立之間的經過時間。 減去計算 `created_at` 從 `Order date`，以整數秒數傳回 |
| `Seconds since cart creation` | 從購物車建立日期到現在的經過時間。 減去計算 `created_at` 從執行查詢時的伺服器時間戳記，以整數秒數傳回。 最常用於識別購物車的年齡 |
| `Store name` | 與此訂單關聯的商務商店的名稱。 通過連接計算 `quote.store_id` to `store.store_id` 並返回 `name` 欄位 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建築** |
|---|---|---|
| `Number of abandoned carts` | 符合特定「放棄」條件的購物車計數 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>篩選器：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中&quot;x&quot;對應至建立購物車後經過的時間（以秒為單位），超過該時間購物車即被視為放棄 |
| `Avg time to cart conversion` | 轉換購物車的購物車建立和訂單建立之間的平均時間 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 放棄的購物車潛在收入總和，其中收入定義為 `base_grand_total` 欄位 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>篩選器：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中&quot;x&quot;對應至建立購物車後經過的時間（以秒為單位），超過該時間購物車即被視為放棄 |

{style="table-layout:auto"}

## 外鍵連接路徑

`customer_entity`

* 加入 `customer_entity` 表格來建立與建立購物車之客戶相關聯的新客戶層級欄。
   * 路徑： `quote.customer_id` （多個）=> `customer_entity.entity_id` (1)

`sales_order`

* 加入 `sales_order` 表格，以建立與轉換的購物車相關聯的退貨詳細資料欄。
   * 路徑：`quote.reserved_order_id` （多個）=> `sales_order.increment_id` (1)

`store`

* 加入 `store` 表格，以建立傳回與購物車相關聯的商務商店詳細資料的欄。
   * 路徑： `quote.store_id` （多個）=> `store.store_id` (1)
