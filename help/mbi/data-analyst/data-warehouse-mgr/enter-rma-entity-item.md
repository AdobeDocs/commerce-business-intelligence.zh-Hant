---
title: Enterprise_Rma_Item_Entity表
description: 了解如何從請求的回訪分析特定項目的相關資訊。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# enterprise_rma_item_entity表

中的每一列 `enterprise_rma_item_entity` 表格(通常稱為 `magento_rma_item_entity` 在商務2.x中，但可自訂名稱)包含來自請求傳回之特定項目的相關資訊。

>[!NOTE]
>
>只有在您是 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客戶。

## 通用本機欄

| **欄名稱** | **說明** |
|---|---|
| `entity\_id` | 表的唯一標識符。 每個 `entity\_id` 表示已請求返回的項目。 |
| `rma\_entity\_id` | 與 `enterprise\_rma` 表格。 |
| `status` | 項目返回的狀態。 值包括「已接收」、「待定」、「已授權」等。 此狀態中的值可能與整體返回狀態的值不匹配。 |
| `qty\_requested` | 客戶要求退貨的數量。 |
| `qty\_approved` | 批准退貨的數量。 |
| `qty\_returned` | 退回的數量。 |
| `order\_item\_id` | 與 `sales\_flat\_order\_item` 表格。 |
| `product\_sku` | 傳回的SKU。 |

{style="table-layout:auto"}

## 公用計算列

| **欄名稱** | **說明** |
|---|---|
| `Return date\_requested` | 這是客戶請求退貨的日期。 |
| `Item price` | 項目的價格。 |
| `Return item's total value (qty\_returned * price)` | 這是傳回項目的總貨幣值。 這可用來計算 `enterprise\_rma` 表格。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建築** |
|---|---|---|
| `Number of items returned` | 傳回的項目數。 | 工序列：返回數量<br>操作：總和<br>時間戳列：請求的返回日期 |
| `Returned items' total value` | 返回的貨幣金額。 | 操作列：退貨項目的總值（退貨數量*價格）<br>操作：總和<br>時間戳列：請求的返回日期 |

{style="table-layout:auto"}

## 連接到其他表

`enterprise_rma`

* 建立聯接列，例如 `Return date\_requested` 在 `enterprise_rma_item_entity` 表格（透過下列連結）:
* 商務1.x: `enterprise_rma_item_entity.rma_entity_id ` （多個）=> `enterprise_rma.entity_id` (1)
* 商務2.x: `magento_rma_item_entity.rma_entity_id ` （多個）=> `magento_rma.entity_id` (1)

`sales_flat_order_item`

* 在  `enterprise_rma_item_entity` 表格（透過下列連結）:

* 商務1.x: `enterprise_rma_item_entity.order_item_id ` （多個）=> `sales_flat_order_item.item_id` (1)
* 商務2.x: `magento_rma_item_entity.order_item_id ` （多個）=> `sales_order_item.item_id` (1)
