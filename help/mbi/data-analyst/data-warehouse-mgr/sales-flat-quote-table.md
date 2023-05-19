---
title: 報價表
description: 瞭解如何使用報價表。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 報價表

的 `quote` 表格`sales_flat_quote` 在M1)中包含在您的商店中建立的每個購物車上的記錄，無論這些記錄是放棄還是轉換為購買。 每行代表一個購物車。 由於此表的潛在大小，Adobe建議您在滿足某些條件時定期刪除記錄，例如，如果有任何未轉換的購物車超過60天。

>[!NOTE]
>
>只有在不從中刪除記錄時，才可以分析歷史的已放棄操作站 `quote` 的子菜單。 如果確實刪除了記錄，則只能查看尚未從資料庫中刪除的購物車。

## 通用本機列

| **列名** | **說明** |
|---|---|
| `base_currency_code` | 捕獲的所有值的幣種 `base_*` 欄位(即 `base_grand_total`。 `base_subtotal`等)。 這通常反映Commerce商店的預設貨幣 |
| `base_grand_total` | 在應用所有稅、發運和折扣後，為客戶報價的最終價格。 雖然精確計算是可定製的，但通常 `base_grand_total` 按 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 購物車中所有物料的商品總值。 不包括稅、發運、折扣等 |
| `created_at` | 以UTC本地儲存的購物車的建立時間戳。 根據您在 [!DNL Commerce Intelligence]，此時間戳可轉換為 [!DNL Commerce Intelligence] 與資料庫時區不同 |
| `customer_email` | 建立購物車的客戶的電子郵件地址 |
| `customer_id` | `Foreign key` 與 `customer_entity` 的下界。 加入到 `customer_entity.entity_id` 確定與建立購物車的用戶關聯的客戶屬性。 如果購物車是通過來賓簽出建立的，則此欄位為 `NULL` |
| `entity_id` (PK) | 表的唯一標識符，在與Commerce實例中的其他表的聯接中常用 |
| `is_active` | 如果購物車是由客戶建立的，並且尚未轉換為訂單，則返回「1」的布爾欄位。 返回「0」，用於轉換的購物車或通過管理員建立的購物車 |
| `items_qty` | 購物車中包含的所有物料的總數量 |
| `reserved_order_id` | `Foreign key` 與 `sales_order` 的子菜單。 加入到 `sales_order.increment_id` 確定與已轉換的購物車關聯的訂單詳細資訊。 對於與已轉換的訂單不關聯的購物車， `reserved_order_id` 遺留 `NULL` |
| `store_id` | `Foreign key` 與 `store` 的子菜單。 加入到 `store`。`store_id` 確定與購物車關聯的商店視圖 |

{style="table-layout:auto"}

## 公用計算列

| **列名** | **說明** |
|---|---|
| `Order date` | 反映已轉換的購物車的訂單建立日期的時間戳。 通過連接計算 `quote.reserved_order_id` 至 `sales_order.increment_id` 還給 `sales_order.created_at` 場 |
| `Seconds between cart creation and order` | 從購物車建立到訂單建立之間經過的時間。 通過減法計算 `created_at` 從 `Order date`，返回為整數秒 |
| `Seconds since cart creation` | 從購物車的建立日期到現在的已用時間。 通過減法計算 `created_at` 以整數秒的形式返回。 最常用於標識購物車的年齡 |
| `Store name` | 與此訂單關聯的Commerce儲存的名稱。 通過連接計算 `quote.store_id` 至 `store.store_id` 還給 `name` 場 |

{style="table-layout:auto"}

## 常用度量

| **度量名稱** | **說明** | **建築** |
|---|---|---|
| `Number of abandoned carts` | 符合特定&quot;棄置&quot;條件的車數 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>篩選器：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中「x」與自建立購物車後（超過此時間被視為已放棄購物車）的已用時間（以秒為單位）相對應 |
| `Avg time to cart conversion` | 為已轉換的購物車建立購物車和建立訂單之間的平均時間 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 總放棄的購物車潛在收入的總和，其中收入定義為 `base_grand_total` 場 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>篩選器：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中「x」與自建立購物車後（超過此時間被視為已放棄購物車）的已用時間（以秒為單位）相對應 |

{style="table-layout:auto"}

## 外鍵連接路徑

`customer_entity`

* 加入到 `customer_entity` 表，以建立與建立購物車的客戶關聯的新客戶層列。
   * 路徑： `quote.customer_id` （許多）=> `customer_entity.entity_id` (1)

`sales_order`

* 加入到 `sales_order` 表，建立與轉換的購物車關聯的退貨單詳細資訊的列。
   * 路徑：`quote.reserved_order_id` （許多）=> `sales_order.increment_id` (1)

`store`

* 加入到 `store` 表格，用於建立返回與購物車關聯的Commerce儲存相關的詳細資訊的列。
   * 路徑： `quote.store_id` （許多）=> `store.store_id` (1)
