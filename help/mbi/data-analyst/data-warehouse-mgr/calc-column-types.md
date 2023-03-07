---
title: 計算的列類型
description: 了解如何建立欄來擴大和最佳化您的資料以進行分析。
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# 計算的列類型

* [相同的表計算](#sametable)
* [一對多計算](#onetomany)
* [多對一計算](#manytoone)
* [實用的參考圖](#map)
* [進階計算欄](#advanced)

在 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md)，您可以建立欄來擴大和最佳化資料以進行分析。 [此功能](../data-warehouse-mgr/creating-calculated-columns.md) 可在「Data Warehouse管理器」中選取任何表格，然後按一下「 **[!UICONTROL Create New Column]**.

本文說明您可以透過「Data Warehouse管理員」建立的欄類型。 它也涵蓋說明、該欄的視覺逐步說明，以及 [參考圖](#map) 建立列所需的所有輸入。 建立計算欄的方式有三種：

* [相同的表計算列](#sametable)
* [一對多計算欄](#onetomany)
* [多對一計算欄](#manytoone)

## 相同的表計算列 {#sametable}

這些列是使用同一表中的輸入列構建的。

### 年齡 {#age}

年齡計算欄會傳回目前時間與某些輸入時間之間的秒數。

以下範例會建立 `Seconds since customer's most recent order` 在 `customers` 表格。 這可用來建立未在內進行購買（有時稱為轉手）的客戶使用者清單 `X days`.

![](../../assets/age.gif)

### 貨幣轉換工具

貨幣轉換器計算列將列的本地貨幣轉換為所需的新貨幣。

以下範例會建立 `base\_grand\_total In AED`，轉換 `base\_grand\_total` 從本幣到AED `sales\_flat\_order` 表格。 此欄適用於想以當地貨幣報告的多種貨幣的商店。

若為商務客戶， `base\_currency\_code` 欄位通常會儲存原生貨幣。 此 `Spot Time` 欄位應符合量度中使用的日期。

![](../../assets/currency_converter.png)

## 一對多計算欄 {#onetomany}

`One-to-Many` 欄 [使用兩個表之間的路徑](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). 此路徑始終表示一個表，一個屬性在其中生存，而一個多表，該屬性被「重新定位」到。 路徑可描述為 `foreign key--primary key` 關係。

### 連結列 {#joined}

聯接列在一個表上重新定位屬性 *to* 多張桌子。 一/多的傳統範例是客戶（一）和訂單（多）。

在以下範例中， `Customer's group\_id` 維度會加入 `orders` 表格。

![](../../assets/joined_column.gif)

## 多對一計算欄 {#manytoone}

這些欄使用的路徑與一對多欄相同，但它們將資料指向相反的方向。 欄會在路徑的一側建立，而非在多側。 由於此關係，列中的值需要是聚合，即對資料點在多邊上執行的數學運算。 此功能有許多使用案例，下方列出幾個。

### 計數 {#count}

此類型的計算列返回許多表上的值計數 *onto* 一張桌子。

在以下範例中，維度 `Customer's lifetime number of canceled orders` 是在 `customers` 表格(具有 `orders.status`)。

![](../../assets/many_to_one.gif){:width=&quot;699&quot; height=&quot;351&quot;}

### 總和 {#sum}

總計計算欄是 `many` 桌子上。

這可用來建立客戶層級維度，例如 `Customer's lifetime revenue`.

### 最小值或最大值 {#minmax}

最小或最大計算列返回存在於多側的最小或最大記錄。

這可用來建立客戶層級維度，例如 `Customer's first order date`.

### 存在 {#exists}

存在的計算列是一個二進位測試，它確定記錄在多邊的存在。 換句話說，新欄會傳回 `1` 如果路徑在每個表中至少連接一行，則 `0` 如果無法進行連線。

此類型的維度可能會判斷（例如）客戶是否曾購買特定產品。 在 `customers` 表格和 `orders` 表格、特定產品的篩選器、維度 `Customer has purchased Product X?` 可以建立。

## 實用的參考圖 {#map}

如果您在建立計算欄時記住所有輸入內容有些困難，請在建立時試著讓此參考圖保持便利：

![](../../assets/merged_reference_map.png)

## 進階計算欄 {#advanced}

在分析和回答有關您業務的問題時，您可能會遇到無法建立所需確切欄的情況。

為確保快速週轉，Adobe建議查看 [高級計算列類型](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) 指南，了解Adobe支援團隊可以建立哪些欄。 該文章也涵蓋您建立欄所需的資訊，包括在您的請求中。

## 相關檔案

* [建立計算列](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [建立/刪除計算列的路徑](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [了解和評估表關係](../../data-analyst/data-warehouse-mgr/table-relationships.md)
