---
title: enterprise_rma表
description: 瞭解如何分析有關特定返回請求的資訊。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma表

中的每一行 `enterprise_rma` 表 `magento_rma` 在Adobe Commerce2.x中，但可以自定義該名稱)包含有關特定返回請求的資訊。

>[!NOTE]
>
>此表僅在您是Adobe Commerce帳戶的 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客戶。

## 通用本機列

| **列名** | **說明** |
|---|---|
| `entity\_id` | 表的唯一標識符。 每個 `entity\_id` 表示返回請求。 |
| `date\_requested` | 請求返回的日期。 |
| `status` | 返回的狀態。 值包括「received」、「pending」、「authorized」等。 |
| `order\_id` | 與 `sales\_flat\_order` 的子菜單。 |
| `customer\_id` | 與 `customer\_entity` 的子菜單。 |

{style="table-layout:auto"}

## 公用計算列

| **列名** | **說明** |
|---|---|
| `Order's created\_at` | 這是原始訂單的日期。 這可用於獲取訂單和退貨請求之間的時間。 |
| `Customer's order number` | 這是與原始訂單關聯的客戶訂單編號。 |
| `Seconds between order's created\_at and return's date\_requested` | 從訂單日期到退貨請求的秒數。 |
| `Return's total value` | 這是返回的總貨幣金額。 這是每個退貨項的單個退貨金額的總和。 |

{style="table-layout:auto"}

## 常用度量

| **度量名稱** | **說明** | **建築** |
|---|---|---|
| `Number of returns` | 請求的返回數。 | `Operation` 列： `entity id`<br>`Operation`: `Count`<br>`Timestamp` 列： `date requested` |
| `Total returned amount` | 退回的總貨幣金額。 | `Operation `列： `Return's total value`<br>`Operation`:和<br>`Timestamp` 列：請求日期 |
| `Average returned amount` | 返回的平均貨幣金額。 | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` 列： `date requested` |
| `Average time to return` | 從訂單到返回的平均時間。 | `Operation` 列：在請求的訂單建立日期和退貨日期之間的秒數<br>`Operation`: `Average`<br>`Timestamp` 列： `date requested` |

{style="table-layout:auto"}

## 到其他表的連接

`sale_flat_order`

* 建立聯接列，以按下列的訂單級屬性分段和篩選 `enterprise_rma` 表格：
   * 商業1.x: `enterprise_rma.order_id` （許多）=> `sales_flat_order.entity_id` (1)
   * 商業2.x: `magento_rma.order_id` （許多）=> `sales_order.entity_id` (1)

`enterprise_rma_item_entity`

* 建立多對一列，如 `Return's total value` 的 `enterprise_rma` 表格：
   * 商業1.x: `enterprise_rma_item_entity.rma_entity_id` （許多）=> `enterprise_rma.entity_id` (1)
   * 商業2.x: `magento_rma_item_entity.rma_entity_id ` （許多）=> `magento_rma.entity_id` (1)
