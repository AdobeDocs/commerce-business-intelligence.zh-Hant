---
title: enterprise_rma表
description: 了解如何分析特定回訪請求的相關資訊。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# enterprise_rma表

中的每一列 `enterprise_rma` 表格(通常稱為 `magento_rma` 在商務2.x中，但可自訂名稱)包含特定傳回請求的相關資訊。

>[!NOTE]
>
>只有在您是 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客戶。

## 通用本機欄

| **欄名稱** | **說明** |
|---|---|
| `entity\_id` | 表的唯一標識符。 每個 `entity\_id` 代表傳回請求。 |
| `date\_requested` | 請求返回的日期。 |
| `status` | 返回的狀態。 值包括「已接收」、「待定」、「已授權」等。 |
| `order\_id` | 與 `sales\_flat\_order` 表格。 |
| `customer\_id` | 與 `customer\_entity` 表格。 |

{style=&quot;table-layout:auto&quot;}

## 公用計算列

| **欄名稱** | **說明** |
|---|---|
| `Order's created\_at` | 這是原始訂單的日期。 這可用來取得訂單與回訪請求之間的時間。 |
| `Customer's order number` | 這是與原始訂單關聯的客戶訂單編號。 |
| `Seconds between order's created\_at and return's date\_requested` | 從訂單日期到傳回請求的秒數。 |
| `Return's total value` | 這是傳回的總貨幣金額。 這將是每個退貨項目的個別退貨金額的總和。 |

{style=&quot;table-layout:auto&quot;}

## 通用量度

| **量度名稱** | **說明** | **建築** |
|---|---|---|
| `Number of returns` | 請求的返回數。 | `Operation` 欄： `entity id`<br>`Operation`: `Count`<br>`Timestamp` 欄： `date requested` |
| `Total returned amount` | 傳回的總貨幣金額。 | `Operation `欄： `Return's total value`<br>`Operation`:總和<br>`Timestamp` 列：請求的日期 |
| `Average returned amount` | 傳回的平均貨幣金額。 | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` 欄： `date requested` |
| `Average time to return` | 從訂單到返回的平均時間。 | `Operation` 欄：請求的訂單日期和退貨日期之間的秒數<br>`Operation`: `Average`<br>`Timestamp` 欄： `date requested` |

{style=&quot;table-layout:auto&quot;}

## 連接到其他表

`sale_flat_order`

* 建立連結欄，以依 `enterprise_rma` 表格（透過下列連結）:
   * 商務1.x: `enterprise_rma.order_id` （多個）=> `sales_flat_order.entity_id` (1)
   * 商務2.x: `magento_rma.order_id` （多個）=> `sales_order.entity_id` (1)

`enterprise_rma_item_entity`

* 建立多對一欄，例如 `Return's total value` 在 `enterprise_rma` 表格（透過下列連結）:
   * 商務1.x: `enterprise_rma_item_entity.rma_entity_id` （多個）=> `enterprise_rma.entity_id` (1)
   * 商務2.x: `magento_rma_item_entity.rma_entity_id ` （多個）=> `magento_rma.entity_id` (1)
