---
title: 計算列類型
description: 瞭解如何建立列以補充和優化資料以進行分析。
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# 計算列類型

* [相同的表計算](#sametable)
* [一對多計算](#onetomany)
* [多對一計算](#manytoone)
* [方便的參考地圖](#map)
* [高級計算列](#advanced)

在 [Data Warehouse管理器](../data-warehouse-mgr/tour-dwm.md)，可以建立列來補充和優化資料以進行分析。 [此功能](../data-warehouse-mgr/creating-calculated-columns.md) 可通過選擇「Data Warehouse管理器」中的任何表並按一下 **[!UICONTROL Create New Column]**。

本主題介紹了可以使用Data Warehouse管理器建立的列的類型。 它還包括描述、該欄目的視覺瀏覽，以及 [參考地圖](#map) 建立列所需的所有輸入。 有三種方法可建立計算列：

1. [相同的表計算列](#sametable)
1. [一對多計算列](#onetomany)
1. [多對一計算列](#manytoone)

## 相同的表計算列 {#sametable}

這些列是使用同一表中的輸入列構建的。

### 年齡 {#age}

年齡計算列返回當前時間和某些輸入時間之間的秒數。

下面的示例建立 `Seconds since customer's most recent order` 的 `customers` 的子菜單。 這可用於構建未在內部進行採購（有時稱為「轉移」）的客戶的用戶清單 `X days`。

![](../../assets/age.gif)

### 貨幣轉換器

貨幣轉換器計算的列將列的本幣轉換為所需的新貨幣。

下面的示例建立 `base\_grand\_total In AED`，轉換 `base\_grand\_total` 從本幣到AED `sales\_flat\_order` 的子菜單。 此列適用於希望以本幣報告的多種貨幣的商店。

對於Commerce客戶， `base\_currency\_code` 欄位通常儲存本幣。 的 `Spot Time` 欄位應與度量中使用的日期匹配。

![](../../assets/currency_converter.png)

## 一對多計算列 {#onetomany}

`One-to-Many` 列 [使用兩個表之間的路徑](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)。 此路徑始終意味著一個表（屬性位於其中）和多個表（屬性將「重新定位」到中）。 路徑可以描述為 `foreign key--primary key` 關係。

### 聯接列 {#joined}

聯接列在一個表上重新定位屬性 *至* 很多桌子。 客戶(1)和訂單（多）是「一/多」的經典示例。

在下面的示例中， `Customer's group\_id` 維被下聯到 `orders` 的子菜單。

![](../../assets/joined_column.gif)

## 多對一計算列 {#manytoone}

這些列使用與一對多列相同的路徑，但它們指向相反的方向。 該列在路徑的一側建立，而不是在多側建立。 由於這種關係，列中的值需要是聚合，即對多端資料點執行的數學操作。 這有許多使用案例，下面列出了一些。

### 計數 {#count}

此類型的計算列返回多個表上的值計數 *上* 一張桌子。

在下面的示例中，維 `Customer's lifetime number of canceled orders` 建立 `customers` 表(帶過濾器 `orders.status`)。

![](../../assets/many_to_one.gif){:width=&quot;699&quot; height=&quot;351&quot;}

### 和 {#sum}

求和計算列是 `many` 桌子上。

這可用於建立客戶級維，如 `Customer's lifetime revenue`。

### 最小或最大 {#minmax}

最小或最大計算列返回多端存在的最小或最大記錄。

這可用於建立客戶級維，如 `Customer's first order date`。

### 存在 {#exists}

計算列是確定記錄在多側存在的二進位test。 換句話說，新列返回 `1` 如果路徑連接每個表中至少一行， `0` 的下界。

此類型的維可能確定客戶是否曾購買過特定產品。 在 `customers` 表格和 `orders` 表，特定產品的篩選器，維 `Customer has purchased Product X?` 可以建造。

## 方便的參考地圖 {#map}

如果您在建立計算列時難以記住所有輸入內容，請在構建時保持此引用映射的方便性：

![](../../assets/merged_reference_map.png)

## 高級計算列 {#advanced}

在您分析和回答有關業務的問題時，可能會遇到無法構建您想要的準確列的情況。

為確保快速週轉，Adobe建議 [高級計算列類型](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) 指南，以查看Adobe支援團隊可以構建的列類型。 該主題還涵蓋建立列所需的資訊 — 將其包括在您的請求中。

## 相關文檔

* [建立計算列](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [建立/刪除計算列的路徑](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [瞭解和評估表關係](../../data-analyst/data-warehouse-mgr/table-relationships.md)
