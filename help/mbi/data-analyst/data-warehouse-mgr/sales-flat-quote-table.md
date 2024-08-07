---
title: 報價表
description: 瞭解如何使用報價表。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 報價表

`quote`資料表（`sales_flat_quote`位於M1）包含您商店中建立的每個購物車記錄，無論這些記錄是否已被捨棄或轉換為購買。 每一列代表一個購物車。 由於此表格可能會有大小，Adobe建議您在符合某些條件時（例如有任何未轉換的購物車超過60天）定期刪除記錄。

>[!NOTE]
>
>只有當您不從`quote`資料表中刪除記錄時，才能分析歷史放棄的購物車。 如果您確實刪除記錄，則只能看到尚未從資料庫移除的購物車。

## 通用原生欄

| **資料行名稱** | **描述** |
|---|---|
| `base_currency_code` | 在`base_*`欄位中擷取的所有值的貨幣（即`base_grand_total`、`base_subtotal`等）。 這通常會反映Commerce商店的預設貨幣 |
| `base_grand_total` | 在套用所有稅捐、運費和折扣後，對購物車的客戶所報的最終價格。 雖然精確計算是可自訂的，但一般`base_grand_total`的計算方式為`base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 購物車中包含之所有專案的商品總值。 不包含稅金、運費、折扣等 |
| `created_at` | 購物車的建立時間戳記，儲存在UTC本機。 視您在[!DNL Commerce Intelligence]中的設定而定，此時間戳記可能會轉換為[!DNL Commerce Intelligence]中與您的資料庫時區不同的報表時區 |
| `customer_email` | 建立購物車的客戶的電子郵件地址 |
| `customer_id` | 與`customer_entity`資料表關聯的`Foreign key` （如果客戶已註冊）。 加入`customer_entity.entity_id`以決定與建立購物車之使用者相關聯的客戶屬性。 如果購物車是透過訪客結帳建立的，則此欄位為`NULL` |
| `entity_id` (PK) | 表格的唯一識別碼，常用於聯結Commerce執行個體內其他表格 |
| `is_active` | 如果購物車是由客戶建立且尚未轉換為訂單，則傳回「1」的布林欄位。 針對轉換後的購物車或透過管理員建立的購物車，傳回「0」 |
| `items_qty` | 購物車中包含之所有專案的總數量 |
| `reserved_order_id` | 與`sales_order`資料表關聯的`Foreign key`。 加入`sales_order.increment_id`以決定與已轉換購物車相關聯的訂單詳細資料。 若購物車未與轉換的訂單關聯，`reserved_order_id`仍為`NULL` |
| `store_id` | 與`store`資料表關聯的`Foreign key`。 加入`store`。`store_id`以判斷哪個Commerce商店檢視與購物車相關聯 |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Order date` | 反映已轉換購物車訂單建立日期的時間戳記。 透過加入`quote.reserved_order_id`至`sales_order.increment_id`並傳回`sales_order.created_at`欄位進行計算 |
| `Seconds between cart creation and order` | 從購物車建立到訂單建立之間經過的時間。 從`Order date`減去`created_at`計算，傳回為整數秒數 |
| `Seconds since cart creation` | 從購物車建立日期到現在之間經過的時間。 計算方式為在執行查詢時從伺服器時間戳記中減去`created_at`，並以整數秒數傳回。 最常用於識別購物車的年齡 |
| `Store name` | 與此訂單相關聯的Commerce商店名稱。 透過加入`quote.store_id`至`store.store_id`並傳回`name`欄位進行計算 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Number of abandoned carts` | 符合特定「放棄」條件的購物車計數 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>篩選器：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中「x」對應於自建立購物車以來經過的時間（以秒為單位），超過該時間，即視為捨棄購物車 |
| `Avg time to cart conversion` | 從購物車建立到轉換購物車訂單建立的平均時間 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 捨棄的購物車潛在收入總和，其中收入定義為`base_grand_total`欄位 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>篩選器：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中&quot;x&quot;會對應到自建立購物車以來經過的時間（以秒為單位），超過該時間，則會視為捨棄購物車 |

{style="table-layout:auto"}

## 外部索引鍵聯結路徑

`customer_entity`

* 加入`customer_entity`表格以建立與建立購物車的客戶相關聯的新客戶層級欄。
   * 路徑： `quote.customer_id` （許多） => `customer_entity.entity_id` （一個）

`sales_order`

* 加入`sales_order`資料表以建立傳回與已轉換購物車相關之訂單詳細資料的資料行。
   * 路徑：`quote.reserved_order_id` （許多） => `sales_order.increment_id` （一個）

`store`

* 加入`store`資料表以建立資料行，這些資料行會傳回與購物車相關聯的Commerce商店相關的詳細資料。
   * 路徑： `quote.store_id` （許多） => `store.store_id` （一個）
