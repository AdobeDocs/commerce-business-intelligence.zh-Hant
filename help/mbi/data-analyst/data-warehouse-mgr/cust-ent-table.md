---
title: customer_entity表
description: 瞭解如何訪問所有已註冊帳戶的記錄。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# customer_entity表

的 `customer_entity` 表包含所有已註冊帳戶的記錄。 如果帳戶註冊，則帳戶被視為已註冊，而不管他們是否完成了購買。 每行對應於一個唯一的註冊帳戶，該帳戶由 `entity_id`。

此表不包含通過來賓結帳下達訂單的客戶記錄。 如果您的商店接受來賓結帳，請參閱 [如何為來賓訂單記帳](../data-warehouse-mgr/guest-orders.md) 為那些命令。

## 公用列

| **列名** | **說明** |
|---|---|
| `created_at` | 與帳戶的註冊日期對應的時間戳，以UTC本地儲存。 根據您在 [!DNL Commerce Intelligence]，此時間戳可轉換為 [!DNL Commerce Intelligence] 與資料庫時區不同 |
| `email` | 與帳戶關聯的電子郵件地址 |
| `entity_id` (PK) | 表的唯一標識符，在與 `customer_id` 在實例中的其他表中 |
| `group_id` | 與 `customer_group` 的子菜單。 加入到 `customer_group.customer_group_id` 確定與註冊帳戶關聯的客戶組 |
| `store_id` | 與 `store` 的子菜單。 加入到 `store`。`store_id` 確定與註冊帳戶關聯的商店視圖 |

{style="table-layout:auto"}

## 公用計算列

| **列名** | **說明** |
|---|---|
| `Customer's first 30 day revenue` | 此客戶在客戶第一個訂單日期後30天內下達的所有訂單的總收入。 通過連接計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 總結 `base_grand_total` 欄位 `sales_order.Seconds between customer's first order date and this order` ≤ 2592000，即30天內的秒數 |
| `Customer's first order date` | 此客戶下單的第一個訂單的時間戳。 通過連接計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 還給最小值 `sales_order`。`created_at` 值 |
| `Customer's first order's billing region` | 與客戶的第一個訂單關聯的開單區域。 通過連接計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 還給 `Billing address region` 何處 `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 與客戶的第一訂單關聯的優惠券代碼。 通過連接計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 還給 `sales_order.coupon_code` 何處 `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 註冊客戶的組名。 通過連接計算 `customer_entity.group_id` 至 `customer_group`。`customer_group_id` 還給 `customer_group_code` 場 |
| `Customer's lifetime number of coupons` | 應用於此客戶下達的所有訂單的優惠券總數。 通過連接計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並計算訂單數 `sales_order.coupon_code` 不是 `NULL` |
| `Customer's lifetime number of orders` | 此客戶下達的訂單總數。 通過連接計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並計算 `sales_order` 表 |
| `Customer's lifetime revenue` | 此客戶下達的所有訂單的收入合計。 通過連接計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 總結 `base_grand_total` 此客戶下達的所有訂單的欄位 |
| `Seconds since customer's first order date` | 從客戶的第一個訂單日期到現在之間經過的時間。 通過減法計算 `Customer's first order date` 從執行查詢時的伺服器時間戳返回，以整數秒數返回 |
| `Store name` | 與此註冊帳戶關聯的Commerce儲存的名稱。 通過連接計算 `customer_entity.store_id` 至 `store.store_id` 還給 `name` 場 |

{style="table-layout:auto"}

## 常用度量

| **度量名稱** | **說明** | **建築** |
|---|---|---|
| `Avg first 30 day revenue` | 在客戶第一訂單後30天內下達訂單的每客戶平均收入 | 操作：平均<br/>操作數： `Customer's first 30 day revenue`<br/>時間戳： `created_at`<br/>篩選器：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000（不包括自首次訂購以來尚未達到30天的客戶） |
| `Avg lifetime coupons` | 每個客戶在其整個生命週期內應用於訂單的平均優惠券數 | 操作：平均<br/>操作數： `Customer's lifetime number of coupons`<br/>時間戳： `created_at` |
| `Avg lifetime orders` | 每個客戶在其生命週期內發出的平均訂單數 | 操作：平均<br/>操作數： `Customer's lifetime number of orders`<br/>時間戳： `created_at` |
| `Avg lifetime revenue` | 在其生命週期內下達的所有訂單的每個客戶的平均總收入 | 操作：平均<br/>操作數： `Customer's lifetime revenue`<br/>時間戳： `created_at` |
| `New customers` | 至少有一個訂單的客戶數，按其第一個訂單的日期計算。 排除註冊但從不下訂單的帳戶 | 操作：計數<br/>操作數： `entity_id`<br/>時間戳： `Customer's first order date` |
| `Registered accounts` | 已註冊的帳戶數。 包括所有註冊帳戶，無論該帳戶是否曾下訂單 | 操作：計數<br/>操作數： `entity_id`<br/>時間戳： `created_at` |

{style="table-layout:auto"}

## 外鍵連接路徑

`customer_group`

* 加入到 `customer_group` 表，以建立返回註冊帳戶的客戶組名稱的列。
   * 路徑： `customer_entity.group_id` （許多）=> `customer_group.customer_group_id` (1)

`store`

* 加入到 `store` 表，以建立返回與與已註冊帳戶關聯的儲存相關的詳細資訊的列。
   * 路徑： `customer_entity.store_id` （許多）=> `store.store_id` (1)
