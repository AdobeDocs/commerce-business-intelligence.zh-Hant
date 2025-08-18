---
title: Enterprise_Rma_Item_Entity表格
description: 瞭解如何從要求的傳回中分析有關特定專案的資訊。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma_item_entity表格

`enterprise_rma_item_entity`表格中的每一列(在Commerce 2.x中通常稱為`magento_rma_item_entity`，但名稱可以自訂)都包含請求傳回的特定專案相關資訊。

>[!NOTE]
>
>唯有當您是`Enterprise Edition`或`Enterprise Cloud Edition`客戶時，此表格才會與您的Commerce帳戶搭配使用。

## 通用原生欄

| **資料行名稱** | **描述** |
|---|---|
| `entity\_id` | 表格的唯一識別碼。 每個`entity\_id`代表要求傳回的專案。 |
| `rma\_entity\_id` | 與`enterprise\_rma`資料表相關聯的外部索引鍵。 |
| `status` | 專案傳回的狀態。 值包括「received」、「pending」、「authorized」等。 此狀態的值可能與整體傳回狀態的值不符。 |
| `qty\_requested` | 客戶要求退貨的數量。 |
| `qty\_approved` | 核准退貨的數量。 |
| `qty\_returned` | 退回的數量。 |
| `order\_item\_id` | 與`sales\_flat\_order\_item`資料表相關聯的外部索引鍵。 |
| `product\_sku` | 正在傳回的SKU。 |

{style="table-layout:auto"}

## 通用計算欄

| **資料行名稱** | **描述** |
|---|---|
| `Return date\_requested` | 這是客戶要求退貨的日期。 |
| `Item price` | 專案的價格。 |
| `Return item's total value (qty\_returned * price)` | 這是傳回專案的總貨幣值。 用於計算`enterprise\_rma`表格上的總退貨金額。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **描述** | **建構** |
|---|---|---|
| `Number of items returned` | 傳回的專案數。 | 作業資料行：傳回的數量<br>作業：總和<br>時間戳記資料行：要求的傳回日期 |
| `Returned items' total value` | 傳回的金額。 | 作業資料行：傳回專案的總計值（傳回數量*價格）<br>作業：總計<br>時間戳記資料行：要求的傳回日期 |

{style="table-layout:auto"}

## 連線到其他資料表

`enterprise_rma`

* 透過下列聯結，在`Return date\_requested`資料表上建立聯結資料行，例如`enterprise_rma_item_entity`：
* Commerce 1.x： `enterprise_rma_item_entity.rma_entity_id ` （許多） => `enterprise_rma.entity_id` （一個）
* Commerce 2.x： `magento_rma_item_entity.rma_entity_id ` （許多） => `magento_rma.entity_id` （一個）

`sales_flat_order_item`

* 在上建立聯結欄  透過下列聯結`enterprise_rma_item_entity`資料表：

* Commerce 1.x： `enterprise_rma_item_entity.order_item_id ` （許多） => `sales_flat_order_item.item_id` （一個）
* Commerce 2.x： `magento_rma_item_entity.order_item_id ` （許多） => `sales_order_item.item_id` （一個）
