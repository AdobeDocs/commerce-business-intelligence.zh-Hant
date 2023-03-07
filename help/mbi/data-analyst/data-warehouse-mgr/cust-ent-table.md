---
title: customer_entity表
description: 了解如何存取所有已註冊帳戶的記錄。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# customer_entity表

此 `customer_entity` 表包含所有已註冊帳戶的記錄。 無論客戶是否完成購買，如果註冊帳戶即視為已註冊。 每一列都對應至一個唯一的註冊帳戶，由該帳戶的 `entity_id`.

此表不包含通過來賓結帳下訂單的客戶記錄。 如果您的商店接受訪客結帳， [了解帳戶](../data-warehouse-mgr/guest-orders.md) 為那些顧客。

## 公用欄

| **欄名稱** | **說明** |
|---|---|
| `created_at` | 與帳戶註冊日期對應的時間戳記，以UTC儲存在本機。 視您在 [!DNL MBI]，此時間戳記可轉換為 [!DNL MBI] 與資料庫時區不同 |
| `email` | 與帳戶相關聯的電子郵件地址 |
| `entity_id` (PK) | 表的唯一標識符，通常用於與 `customer_id` 在實例內的其他表中 |
| `group_id` | 與 `customer_group` 表格。 加入 `customer_group.customer_group_id` 確定與註冊帳戶關聯的客戶組 |
| `store_id` | 與 `store` 表格。 加入 `store`.`store_id` 確定與註冊帳戶關聯的商務商店視圖 |

{style="table-layout:auto"}

## 公用計算列

| **欄名稱** | **說明** |
|---|---|
| `Customer's first 30 day revenue` | 此客戶在首次訂購日期後30天內下單的所有訂單的總收入。 通過連接計算 `customer_entity.entity_id` to `sales_order.customer_id` 和加總 `base_grand_total` 欄位，其中 `sales_order.Seconds between customer's first order date and this order` ≤ 2592000，即30天內的秒數 |
| `Customer's first order date` | 此客戶下單的首次訂單時間戳記。 通過連接計算 `customer_entity.entity_id` to `sales_order.customer_id` 並返回最小值 `sales_order`.`created_at` value |
| `Customer's first order's billing region` | 與客戶首次訂購關聯的計費區域。 通過連接計算 `customer_entity.entity_id` to `sales_order.customer_id` 並返回 `Billing address region` where `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 與客戶首次訂購相關聯的抵用券代碼。 通過連接計算 `customer_entity.entity_id` to `sales_order.customer_id` 並返回 `sales_order.coupon_code` where `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 註冊客戶的組名。 通過連接計算 `customer_entity.group_id` to `customer_group`.`customer_group_id` 並返回 `customer_group_code` 欄位 |
| `Customer's lifetime number of coupons` | 套用至此客戶所下訂單的抵用券總數。 通過連接計算 `customer_entity.entity_id` to `sales_order.customer_id` 並計算 `sales_order.coupon_code` 不是 `NULL` |
| `Customer's lifetime number of orders` | 此客戶下的訂單總數。 通過連接計算 `customer_entity.entity_id` to `sales_order.customer_id` 並計算 `sales_order` 表格 |
| `Customer's lifetime revenue` | 此客戶下的所有訂單的總收入。 通過連接計算 `customer_entity.entity_id` to `sales_order.customer_id` 和加總 `base_grand_total` 欄位，此客戶下的所有訂單 |
| `Seconds since customer's first order date` | 客戶首次訂購日期與現在之間的經過時間。 減去計算 `Customer's first order date` 從執行查詢時的伺服器時間戳記傳回，以整數秒數表示 |
| `Store name` | 與此註冊帳戶關聯的商務儲存的名稱。 通過連接計算 `customer_entity.store_id` to `store.store_id` 並返回 `name` 欄位 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建築** |
|---|---|---|
| `Avg first 30 day revenue` | 在客戶首次訂購後30天內下單的每位客戶平均收入 | 操作：平均<br/>操作數： `Customer's first 30 day revenue`<br/>時間戳記： `created_at`<br/>篩選器：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000（不包括自首次訂購後30天仍未到達的客戶） |
| `Avg lifetime coupons` | 在期限內套用至每個客戶之訂單的平均抵用券數量 | 操作：平均<br/>操作數： `Customer's lifetime number of coupons`<br/>時間戳記： `created_at` |
| `Avg lifetime orders` | 每個客戶在其期限內下的平均訂單數 | 操作：平均<br/>操作數： `Customer's lifetime number of orders`<br/>時間戳記： `created_at` |
| `Avg lifetime revenue` | 在其期限內下的所有訂單的每位客戶平均總收入 | 操作：平均<br/>操作數： `Customer's lifetime revenue`<br/>時間戳記： `created_at` |
| `New customers` | 至少有一筆訂單的客戶數量，計在其首筆訂單的日期。 不包括註冊但從未下訂單的帳戶 | 操作：計數<br/>操作數： `entity_id`<br/>時間戳記： `Customer's first order date` |
| `Registered accounts` | 註冊的帳戶數。 包括所有註冊帳戶，無論帳戶是否下過訂單 | 操作：計數<br/>操作數： `entity_id`<br/>時間戳記： `created_at` |

{style="table-layout:auto"}

## 外鍵連接路徑

`customer_group`

* 加入 `customer_group` 表，以建立返回已註冊帳戶的客戶組名的列。
   * 路徑： `customer_entity.group_id` （多個）=> `customer_group.customer_group_id` (1)

`store`

* 加入 `store` 表，以建立返回與與已註冊帳戶關聯的儲存相關的詳細資訊的列。
   * 路徑： `customer_entity.store_id` （多個）=> `store.store_id` (1)
