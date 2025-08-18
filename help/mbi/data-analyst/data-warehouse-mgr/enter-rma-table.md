---
title: enterprise_rma表格
description: 瞭解如何分析有關特定回訪請求的資訊。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# enterprise_rma表格

`enterprise_rma`表格中的每一列(在Adobe Commerce 2.x中通常稱為`magento_rma`，但可自訂名稱)都包含特定回訪請求的資訊。

>[!NOTE]
>
>唯有當您是`Enterprise Edition`或`Enterprise Cloud Edition`客戶時，此表格才會與您的Adobe Commerce帳戶搭配使用。

## 通用原生欄

| **資料行名稱** | **描述** |
|---|---|
| `entity\_id` | 表格的唯一識別碼。 每個`entity\_id`代表一個傳回要求。 |
| `date\_requested` | 要求傳回的日期。 |
| `status` | 傳回的狀態。 值包括「received」、「pending」、「authorized」等。 |
| `order\_id` | 與`sales\_flat\_order`資料表相關聯的外部索引鍵。 |
| `customer\_id` | 與`customer\_entity`資料表相關聯的外部索引鍵。 |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Order's created\_at` | 這是原始訂單的日期。 這可用來取得訂單與退貨要求之間的時間。 |
| `Customer's order number` | 這是與原始訂單相關聯的客戶訂單編號。 |
| `Seconds between order's created\_at and return's date\_requested` | 從訂購日期到退貨請求的秒數。 |
| `Return's total value` | 這是傳回的總金額。 這是每個退貨專案的個別退貨金額的總和。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Number of returns` | 要求的傳回次數。 | `Operation`欄： `entity id`<br>`Operation`： `Count`<br>`Timestamp`欄： `date requested` |
| `Total returned amount` | 傳回的總金額。 | `Operation `資料行： `Return's total value`<br>`Operation`： Sum<br>`Timestamp`資料行：要求的日期 |
| `Average returned amount` | 傳回的平均金額。 | `Operation` ` Column: Return's total value`<br>`Operation`： `Average`<br>`Timestamp`欄： `date requested` |
| `Average time to return` | 從訂單到退貨的平均時間。 | `Operation`欄：訂單建立日期與傳回請求日期之間的秒數<br>`Operation`： `Average`<br>`Timestamp`欄： `date requested` |

{style="table-layout:auto"}

## 連線到其他資料表

`sale_flat_order`

* 建立聯結資料行，以透過下列聯結依據`enterprise_rma`資料表的訂單層級屬性進行區段和篩選：
   * Commerce 1.x： `enterprise_rma.order_id` （許多） => `sales_flat_order.entity_id` （一個）
   * Commerce 2.x： `magento_rma.order_id` （許多） => `sales_order.entity_id` （一個）

`enterprise_rma_item_entity`

* 透過下列聯結，在`Return's total value`資料表上建立多對一資料行，例如`enterprise_rma`：
   * Commerce 1.x： `enterprise_rma_item_entity.rma_entity_id` （許多） => `enterprise_rma.entity_id` （一個）
   * Commerce 2.x： `magento_rma_item_entity.rma_entity_id ` （許多） => `magento_rma.entity_id` （一個）
