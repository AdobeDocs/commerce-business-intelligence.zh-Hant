---
title: 格式化及匯入電子商務資料
description: 瞭解用於上傳電子商務資料的理想資料格式。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/3Aa9DgQL0H9cNeJOJ7-qHkROOkphjzpQkDvJ0KwOIwY
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 459
ht-degree: 0%

---

# 格式化及匯入資料

如果您使用[!DNL Adobe Commerce Intelligence]目前不支援的整合，您仍可使用[檔案上傳功能](using-file-uploader.md)將您的資料匯入Data Warehouse。 本主題說明用於上傳電子商務資料的理想資料格式。

## `Orders`資料表

`orders`表格應該包含企業已執行之每筆交易的一列。 可能的欄包括：

| 欄名稱 | 說明 |
|----|----|
| `Order ID` | 表格中每一列的順序ID應是唯一的。 此外，這通常是表格的主索引鍵。 |
| `Customer` | 下訂單的客戶。 |
| `Order total` | 訂單總計。 這可能是以計算為基礎的欄，其他欄中的值（例如小計和運送）構成此欄的總計。 |
| `Currency` | 支付訂單所用的貨幣。 包含（若相關）。 |
| ` Order status` | 訂單的狀態，例如`In Progress`、`Refunded`或`Complete`。 此欄的值會變更（如果不完整）。 新的和更新的資料可以使用[頁面上的](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md)附加資料功能`File Uploads`匯入。 |
| `Acquisition/marketing channel` | 下訂單的客戶反向連結的贏取或行銷管道。 |
| `Order datetime` | 建立訂單的日期和時間。 |
| `Order updated at` | 上次修改訂單記錄的日期和時間。 |

{style="table-layout:auto"}

## `Order detail/items`資料表 {#itemstable}

`order_detail / items`表格應該在每個順序的每個不同專案中包含一列。 可能的欄包括：

| 欄名稱 | 說明 |
|----|----|
| `Order item ID` | 表格中每一列的訂單專案ID應是唯一的。 此外，這通常是表格的`primary key`。 |
| `Order ID` | 訂單的ID。 |
| `Product ID` | 產品的ID。 |
| `Product name` | 產品的名稱。 |
| `Product's unit price` | 產品的單一單位價格。 |
| `Quantity` | 訂單中的產品數量。 |

## `Customers`資料表 {#customerstable}

`customers`表格應該針對每個客戶帳戶包含一個資料列。 可能的欄包括：

| 欄名稱 | 說明 |
|----|----|
| `Customer ID` | 表格中每一列的客戶ID都應是唯一的。 此外，這通常是表格的主索引鍵。 |
| `Customer created at` | 建立客戶帳戶的日期和時間。 |
| `Customer modified at` | 上次修改客戶帳戶的日期和時間。 |
| `Acquisition/marketing channel source` | 向客戶轉介的贏取或行銷管道。 |
| `Demographic info` | 年齡範圍和性別等人口統計資訊可用於劃分報表。 |
| `Acquisition/marketing channel` | 下訂單的客戶反向連結的贏取或行銷管道。 |

## `Subscription payments`資料表

`subscriptions`表格應該針對每個訂閱付款包含一個資料列。 可能的欄包括：

| 欄名稱 | 說明 |
|----|----|
| `Subscription ID` | 表格中每一列的訂閱ID都應是唯一的。 此外，這通常是表格的主索引鍵。 |
| `Customer ID` | 付款客戶的識別碼。 |
| `Payment amount` | 訂閱付款的金額。 |
| `Start date` | 付款涵蓋期間的開始日期時間。 |
| `End date` | 付款涵蓋期間的結束日期時間。 |
