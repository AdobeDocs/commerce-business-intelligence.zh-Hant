---
title: 格式化和匯入電子商務資料
description: 了解上傳電子商務資料時使用的理想資料格式。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 格式化和導入資料

如果您使用目前不支援的整合 [!DNL MBI]，您仍可使用 [檔案上傳功能](using-file-uploader.md) 將您的資料匯入資料倉庫。 本文主要探討上傳電子商務資料時所需的理想資料格式。

## `Orders` 表格

此 `orders` 表應包含業務已執行的每項事務的一行。 可能的列包括：

| 欄名稱 | 說明 |
|----|----|
| `Order ID` | 表格中每一列的順序ID都應是唯一的。 此外，這通常是表的主要索引鍵。 |
| `Customer` | 下訂單的客戶。 |
| `Order total` | 訂單的總計。 這可能是以計算為基礎的欄，其他欄（例如小計和發運）中的值構成此欄的總計。 |
| `Currency` | 訂單支付的幣種。 若相關則納入。 |
| ` Order status` | 訂單的狀態，例如 `In Progress`, `Refunded`，或 `Complete`. 此欄的值可能會變更（如果未完成）。 可使用 [附加資料功能](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 在 `File Uploads` 頁面。 |
| `Acquisition/marketing channel` | 系統會參照下訂單的客戶的贏取或行銷管道。 |
| `Order datetime` | 建立訂單的日期和時間。 |
| `Order updated at` | 上次修改訂單記錄的日期和時間。 |

{style=&quot;table-layout:auto&quot;}

## `Order detail/items` 表格 {#itemstable}

此 `order_detail / items` 表格應以每個順序包含每個不同項目的一列。 可能的列包括：

| 欄名稱 | 說明 |
|----|----|
| `Order item ID` | 表格中每一列的訂單項目ID都應是唯一的。 此外，這通常是 `primary key` 為了桌子。 |
| `Order ID` | 訂單ID。 |
| `Product ID` | 產品的ID。 |
| `Product name` | 產品的名稱。 |
| `Product's unit price` | 單位產品的價格。 |
| `Quantity` | 訂單中的產品數量。 |

## `Customers` 表格 {#customerstable}

此 `customers` 表格應包含每個客戶帳戶的一列。 可能的列包括：

| 欄名稱 | 說明 |
|----|----|
| `Customer ID` | 表格中每一列的客戶ID都應是唯一的。 此外，這通常是表的主要索引鍵。 |
| `Customer created at` | 建立客戶帳戶的日期和時間。 |
| `Customer modified at` | 上次修改客戶帳戶的日期和時間。 |
| `Acquisition/marketing channel source` | 客戶被轉介的贏取或行銷管道。 |
| `Demographic info` | 人口統計資訊（例如年齡範圍和性別）可用來劃分報表。 |
| `Acquisition/marketing channel` | 系統會參照下訂單的客戶的贏取或行銷管道。 |

## `Subscription payments` 表格

此 `subscriptions` 表格應包含每筆訂閱付款的一列。 可能的列包括：

| 欄名稱 | 說明 |
|----|----|
| `Subscription ID` | 表格中每一列的訂閱ID都應是唯一的。 此外，這通常是表的主要索引鍵。 |
| `Customer ID` | 付款的客戶ID。 |
| `Payment amount` | 訂閱付款的金額。 |
| `Start date` | 付款涵蓋的期間的起始日期。 |
| `End date` | 付款涵蓋的期間的結束日期。 |
