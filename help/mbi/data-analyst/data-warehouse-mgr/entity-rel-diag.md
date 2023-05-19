---
title: 實體關係圖
description: 瞭解幾個ER圖，以幫助您直觀地顯示幾個常用Commerce資料庫表之間的關係。
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 實體關係圖

什麼是 **[!UICONTROL entity relationship (ER) diagram]**? 安 [!UICONTROL ER] 圖是資料庫中表的可視化，以及表與表之間的關係。 本主題包含 [!UICONTROL ER] 圖，幫助您直觀顯示幾個常用的Adobe Commerce資料庫表之間的關係。

>[!NOTE]
>
>在整個主題中，您可以看到 **加入**。 **關係**, **路徑**。 這些詞都用於描述兩個表的連接方式。

## 核心商務 [!UICONTROL ER] 圖

![4_資料庫_圖表](../../assets/4_DB_Chart.png)

此 `ER` 圖表表示Commerce資料庫中核心表之間的關係。 通過一次查看多個關係，您可以看到資料在多個表之間如何關聯。

以下各節包含 `ER` 一次特定於兩個表的圖。 要查看圖及其附帶說明，請按一下該節的標題。

## `customer\_entity & sales\_flat\_order`

![一個客戶多訂單](../../assets/2_OneCustomerManyOrders.png)

一個客戶可以下很多訂單。 這兩個表之間的關係是 `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` 不等於 `sales\_flat\_order.entity\_id`。 第一個可以認為 `customer\_id` 第二個可以認為 `order\_id.`

在 [!DNL Commerce Intelligence]，如果這兩個表之間的路徑不存在，則 [建立路徑](../data-warehouse-mgr/create-paths-calc-columns.md) Data Warehouse。 準備好建立路徑時，將按如下方式定義：

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

一個訂單可以包含多個項。 這兩個表之間的關係是 `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`。

在 [!DNL Commerce Intelligence]，如果這兩個表之間的路徑不存在，則 [建立路徑](../data-warehouse-mgr/create-paths-calc-columns.md) 的子菜單。 準備建立路徑時，定義路徑，如下所示。

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

一個產品可以購買多種產品。 這兩個表之間的關係是 `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`。

在 [!DNL Commerce Intelligence]，如果這兩個表之間的路徑不存在，則 [建立路徑](../data-warehouse-mgr/create-paths-calc-columns.md) Data Warehouse。 準備建立路徑時，定義路徑，如下所示。

![](../../assets/SFOI___CPE_path.png)
