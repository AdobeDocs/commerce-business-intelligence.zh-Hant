---
title: 企業_RMA_物料_實體表
description: 瞭解如何從請求的返回中分析有關特定項的資訊。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# enterprise_rma_item_entity表

中的每一行 `enterprise_rma_item_entity` 表 `magento_rma_item_entity` 在Commerce 2.x中，但可以自定義名稱)包含有關請求返回的特定項的資訊。

>[!NOTE]
>
>只有在您是Commerce帳戶的 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客戶。

## 通用本機列

| **列名** | **說明** |
|---|---|
| `entity\_id` | 表的唯一標識符。 每個 `entity\_id` 表示已請求返回的項。 |
| `rma\_entity\_id` | 與 `enterprise\_rma` 的子菜單。 |
| `status` | 物料返回的狀態。 值包括「received」、「pending」、「authorized」等。 此狀態中的值可能與總返回狀態的值不匹配。 |
| `qty\_requested` | 客戶要求退貨的數量。 |
| `qty\_approved` | 批准退貨的數量。 |
| `qty\_returned` | 返回的數量。 |
| `order\_item\_id` | 與 `sales\_flat\_order\_item` 的子菜單。 |
| `product\_sku` | 正在返回的sku。 |

{style="table-layout:auto"}

## 公用計算列

| **列名** | **說明** |
|---|---|
| `Return date\_requested` | 這是客戶請求退貨的日期。 |
| `Item price` | 物料的價格。 |
| `Return item's total value (qty\_returned * price)` | 這是返回的項的總貨幣值。 此值用於計算 `enterprise\_rma` 的子菜單。 |

{style="table-layout:auto"}

## 常用度量

| **度量名稱** | **說明** | **建築** |
|---|---|---|
| `Number of items returned` | 返回的項目數。 | 工序列：返回的數量<br>工序：總計<br>時間戳列：請求的返回日期 |
| `Returned items' total value` | 返回的貨幣金額。 | 操作列：退貨項的總值（退貨數量x價格）<br>操作：和<br>時間戳列：請求的返回日期 |

{style="table-layout:auto"}

## 到其他表的連接

`enterprise_rma`

* 建立聯接列，如 `Return date\_requested` 的 `enterprise_rma_item_entity` 表格：
* 商業1.x: `enterprise_rma_item_entity.rma_entity_id ` （許多）=> `enterprise_rma.entity_id` (1)
* 商業2.x: `magento_rma_item_entity.rma_entity_id ` （許多）=> `magento_rma.entity_id` (1)

`sales_flat_order_item`

* 在  `enterprise_rma_item_entity` 表格：

* 商業1.x: `enterprise_rma_item_entity.order_item_id ` （許多）=> `sales_flat_order_item.item_id` (1)
* 商業2.x: `magento_rma_item_entity.order_item_id ` （許多）=> `sales_order_item.item_id` (1)
