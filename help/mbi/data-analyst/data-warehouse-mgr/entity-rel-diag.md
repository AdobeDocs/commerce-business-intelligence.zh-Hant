---
title: 實體關係圖
description: 了解幾個ER圖表，以幫助您直觀地了解幾個常見的Commerce資料庫表之間的關係。
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 實體關係圖

什麼是 **[!UICONTROL entity relationship (ER) diagram]**? 安 `ER` 圖表是資料庫內表格及其彼此間關係的視覺效果。 本文包含一些ER圖表，可幫助您直觀地顯示幾個常見的Commerce資料庫表之間的關係。

>[!NOTE]
>
>在本文中，您會看到 **加入**, **關係** 和 **路徑**. 這些詞都用於描述兩個表的連接方式。

## 核心商務 `ER` 圖表

![4_DB_Chart](../../assets/4_DB_Chart.png)

此 `ER` 圖表表示Commerce資料庫內核心表之間的關係。 通過一次查看多個關係，您可以了解資料在多個表之間的關聯。

以下各節包含 `ER` 一次對兩個表的特定圖表。 若要檢視圖表及其隨附說明，請按一下該區段的標題。

## `customer\_entity & sales\_flat\_order`

![一個客戶多訂單](../../assets/2_OneCustomerManyOrders.png)

一個客戶可以下很多訂單。 這兩個表之間的關係是 `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` 不等於 `sales\_flat\_order.entity\_id`. 第一個可以認為 `customer\_id` 第二個可以被認為 `order\_id.` 您可以在 [`entity\_id` 節](https://support.magento.com/hc/en-us/articles/360016729951) 我們 _[!DNL Magento]:常見誤解_ 文章。

內 [!DNL MBI]，如果這兩個表之間的路徑尚未存在，則您可以 [建立路徑](../data-warehouse-mgr/create-paths-calc-columns.md) 在「Data Warehouse」標籤中。 準備好建立路徑時，其定義如下：

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

一個訂單可以包含許多項目。 這兩個表之間的關係是 `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

內 [!DNL MBI]，如果這兩個表之間的路徑尚未存在，則您可以 [建立路徑](../data-warehouse-mgr/create-paths-calc-columns.md) 在「Data Warehouse」標籤中。 準備好建立路徑時，其定義如下：

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

一個產品可以購買許多項目。 這兩個表之間的關係是 `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

內 [!DNL MBI]，如果這兩個表之間的路徑尚未存在，則您可以 [建立路徑](../data-warehouse-mgr/create-paths-calc-columns.md) 在「Data Warehouse」標籤中。 準備好建立路徑時，其定義如下：

![](../../assets/SFOI___CPE_path.png)
