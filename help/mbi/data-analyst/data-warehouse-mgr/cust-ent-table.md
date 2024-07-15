---
title: customer_entity表格
description: 瞭解如何存取所有已註冊帳戶的記錄。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# customer_entity表格

`customer_entity`資料表包含所有已註冊帳戶的記錄。 無論客戶是否完成購買，只要客戶註冊帳戶，即視為已註冊。 每一列對應一個唯一的註冊帳戶，由該帳戶的`entity_id`識別。

此表格未包含透過訪客結帳下訂單的客戶記錄。 如果您的商店接受訪客結帳，請參閱[如何為那些訂單計算訪客訂單](../data-warehouse-mgr/guest-orders.md)。

## 通用欄

| **資料行名稱** | **描述** |
|---|---|
| `created_at` | 與帳戶註冊日期對應的時間戳記，以UTC儲存在本機。 視您在[!DNL Commerce Intelligence]中的設定而定，此時間戳記可能會轉換為[!DNL Commerce Intelligence]中與您的資料庫時區不同的報表時區 |
| `email` | 與帳戶相關聯的電子郵件地址 |
| `entity_id` (PK) | 資料表的唯一識別碼，常用於執行個體內其他資料表中與`customer_id`的聯結 |
| `group_id` | 與`customer_group`資料表相關聯的外部索引鍵。 加入`customer_group.customer_group_id`以決定與註冊帳戶相關聯的客戶群組 |
| `store_id` | 與`store`資料表相關聯的外部索引鍵。 加入`store`。`store_id`以判斷哪個Commerce存放區檢視與已註冊的帳戶相關聯 |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Customer's first 30 day revenue` | 此客戶在第一個訂單日期起的30天內所下所有訂單的收入總和。 計算方式為將`customer_entity.entity_id`加入`sales_order.customer_id`並加總`sales_order.Seconds between customer's first order date and this order`≤2592000之所有訂單的`base_grand_total`欄位，即30天內的秒數 |
| `Customer's first order date` | 此客戶下第一個訂單的時間戳記。 計算方式為將`customer_entity.entity_id`加入`sales_order.customer_id`並傳回最小值`sales_order`。`created_at`值 |
| `Customer's first order's billing region` | 與客戶第一筆訂單相關聯的帳單區域。 透過加入`customer_entity.entity_id`到`sales_order.customer_id`並傳回`sales_order.Customer's order number` = 1的`Billing address region`進行計算 |
| `Customer's first order's coupon_code` | 與客戶第一筆訂單相關聯的抵用券代碼。 透過加入`customer_entity.entity_id`到`sales_order.customer_id`並傳回`sales_order.Customer's order number` = 1的`sales_order.coupon_code`進行計算 |
| `Customer's group code` | 註冊客戶的群組名稱。 透過將`customer_entity.group_id`加入`customer_group`進行計算。`customer_group_id`並傳回`customer_group_code`欄位 |
| `Customer's lifetime number of coupons` | 套用至此客戶所下所有訂單的優惠券總數。 計算方式為將`customer_entity.entity_id`加入`sales_order.customer_id`並計算`sales_order.coupon_code`不是`NULL`的訂單數 |
| `Customer's lifetime number of orders` | 此客戶下單的訂單總數。 計算方式為將`customer_entity.entity_id`加入`sales_order.customer_id`並計算`sales_order`資料表中的資料列數目 |
| `Customer's lifetime revenue` | 此客戶下所有訂單的收入總和。 計算方式為將`customer_entity.entity_id`加入`sales_order.customer_id`並加總此客戶下所有訂單的`base_grand_total`欄位 |
| `Seconds since customer's first order date` | 從客戶第一次訂購日期到現在之間的經過時間。 計算方式為在執行查詢時從伺服器時間戳記中減去`Customer's first order date`，並以整數秒數傳回 |
| `Store name` | 與此註冊帳戶相關聯的Commerce存放區名稱。 透過加入`customer_entity.store_id`至`store.store_id`並傳回`name`欄位進行計算 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Avg first 30 day revenue` | 每位客戶在客戶首次訂購後30天內所下訂單的平均收入 | 作業： Average<br/>運算元： `Customer's first 30 day revenue`<br/>時間戳記： `created_at`<br/>篩選器：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 （排除從第一次訂購起尚未達到30天的客戶） |
| `Avg lifetime coupons` | 每位客戶在其服務期限內，套用至訂單的平均優惠券數目 | 作業：平均<br/>運算元： `Customer's lifetime number of coupons`<br/>時間戳記： `created_at` |
| `Avg lifetime orders` | 每位客戶在其服務期限內的平均下單次數 | 作業：平均<br/>運算元： `Customer's lifetime number of orders`<br/>時間戳記： `created_at` |
| `Avg lifetime revenue` | 所有訂購在其期限內，每個客戶的平均總收入 | 作業：平均<br/>運算元： `Customer's lifetime revenue`<br/>時間戳記： `created_at` |
| `New customers` | 至少有一筆訂單的客戶數，計算在其第一筆訂單的日期。 不包括註冊但從未下訂單的帳戶 | 作業：計數<br/>運算元： `entity_id`<br/>時間戳記： `Customer's first order date` |
| `Registered accounts` | 註冊的帳戶數。 包含所有已註冊的帳戶，無論帳戶是否下過訂單 | 作業：計數<br/>運算元： `entity_id`<br/>時間戳記： `created_at` |

{style="table-layout:auto"}

## 外部索引鍵聯結路徑

`customer_group`

* 加入`customer_group`資料表以建立傳回已註冊帳戶之客戶群組名稱的資料行。
   * 路徑： `customer_entity.group_id` （許多） => `customer_group.customer_group_id` （一個）

`store`

* 加入`store`資料表以建立資料行，這些資料行會傳回與已登入帳戶相關聯之存放區的相關詳細資料。
   * 路徑： `customer_entity.store_id` （許多） => `store.store_id` （一個）
