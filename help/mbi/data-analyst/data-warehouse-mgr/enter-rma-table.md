---
title: enterprise_rma表格
description: 瞭解如何分析有關特定回訪請求的資訊。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: ad4dda927f0b1b2eba9596d7adfd1419676cf03d
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# enterprise_rma表格

`enterprise_rma`表格中的每一列（在Adobe Commerce 2.x中通常稱為`magento_rma`，但可自訂名稱）都包含特定回訪請求的資訊。

>[!NOTE]
>
>唯有當您是`Enterprise Edition`或`Enterprise Cloud Edition`客戶時，此表格才會與您的Adobe Commerce帳戶搭配使用。

## 通用原生欄

| **資料行名稱** | **描述** |
|---|---|
| `entity_id` | 表格的唯一識別碼。 每個`entity_id`代表一個傳回要求。 |
| `date_requested` | 要求傳回的日期。 |
| `status` | 傳回的狀態。 值包括「received」、「pending」、「authorized」等。 |
| `order_id` | 與`sales_flat_order`資料表相關聯的外部索引鍵。 |
| `customer_id` | 與`customer_entity`資料表相關聯的外部索引鍵。 |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Order's created_at` | 這是原始訂單的日期。 這可用來取得訂單與退貨要求之間的時間。 |
| `Customer's order number` | 這是與原始訂單相關聯的客戶訂單編號。 |
| `Seconds between order's created_at and return's date_requested` | 從訂購日期到退貨請求的秒數。 |
| `Return's total value` | 這是傳回的總金額。 這是每個退貨專案的個別退貨金額的總和。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Number of returns` | 要求的傳回次數。 | `Operation`欄： `entity_id`<br>`Operation`： `Count`<br>`Timestamp`欄： `date requested` |
| `Total returned amount` | 傳回的總金額。 | `Operation `資料行： `Return's total value`<br>`Operation`： Sum<br>`Timestamp`資料行：要求的日期 |
| `Average returned amount` | 傳回的平均金額。 | `Operation`` Column: Return's total value`<br>`Operation`： `Average`<br>`Timestamp`欄： `date requested` |
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
