---
title: 格式化和導入電子商務資料
description: 瞭解用於上載電子商務資料的理想資料格式。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 格式化和導入資料

如果您使用的整合當前不受支援 [!DNL Adobe Commerce Intelligence]，您仍然可以使用 [檔案上載功能](using-file-uploader.md) 將資料導入Data Warehouse。 本主題介紹用於上載電子商務資料的理想資料格式。

## `Orders` 表

的 `orders` 表應包含業務已執行的每個事務的一行。 潛在列包括：

| 列名 | 說明 |
|----|----|
| `Order ID` | 對於表中的每一行，順序ID應是唯一的。 此外，這通常是表的主鍵。 |
| `Customer` | 下訂單的客戶。 |
| `Order total` | 訂單總數。 這可能是基於計算的列，其他列（如小計和發運）中的值構成此列的合計。 |
| `Currency` | 訂單支付的幣種。 包括（如果相關）。 |
| ` Order status` | 訂單的狀態，如 `In Progress`。 `Refunded`或 `Complete`。 此列的值將更改（如果未完成）。 可以使用 [附加資料功能](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 的 `File Uploads` 的子菜單。 |
| `Acquisition/marketing channel` | 客戶下訂單的購買或營銷渠道是從中引用的。 |
| `Order datetime` | 建立訂單的日期和時間。 |
| `Order updated at` | 對訂單記錄進行上次修改的日期和時間。 |

{style="table-layout:auto"}

## `Order detail/items` 表 {#itemstable}

的 `order_detail / items` 表中每個順序的每個不同項應包含一行。 潛在列包括：

| 列名 | 說明 |
|----|----|
| `Order item ID` | 訂單項ID應對表中的每一行是唯一的。 而且，這通常 `primary key` 的下界。 |
| `Order ID` | 訂單的ID。 |
| `Product ID` | 產品的ID。 |
| `Product name` | 產品的名稱。 |
| `Product's unit price` | 產品單一單位的價格。 |
| `Quantity` | 訂單中的產品數量。 |

## `Customers` 表 {#customerstable}

的 `customers` 每個客戶帳戶應包含一行。 潛在列包括：

| 列名 | 說明 |
|----|----|
| `Customer ID` | 客戶ID對於表中的每一行應是唯一的。 此外，這通常是表的主鍵。 |
| `Customer created at` | 建立客戶帳戶的日期和時間。 |
| `Customer modified at` | 上次修改客戶帳戶的日期和時間。 |
| `Acquisition/marketing channel source` | 客戶所參考的收購或營銷渠道。 |
| `Demographic info` | 人口結構資訊（如年齡範圍和性別）可用於分段報告。 |
| `Acquisition/marketing channel` | 客戶下訂單的購買或營銷渠道是從中引用的。 |

## `Subscription payments` 表

的 `subscriptions` 表應為每個訂閱付款包含一行。 潛在列包括：

| 列名 | 說明 |
|----|----|
| `Subscription ID` | 預訂ID對於表中的每一行應是唯一的。 此外，這通常是表的主鍵。 |
| `Customer ID` | 付款的客戶的ID。 |
| `Payment amount` | 訂閱付款的金額。 |
| `Start date` | 付款所涵蓋期間的起始日期時間。 |
| `End date` | 付款所涵蓋的期間的結束日期時間。 |
