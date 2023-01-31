---
title: 建立或刪除計算欄的路徑
description: 了解如何定義路徑，以說明您要在上建立欄的表格如何與您要從中提取資訊的表格相關。
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# 建立或刪除計算列的路徑

## 計算列刷新器

當 [建立計算列](../data-warehouse-mgr/creating-calculated-columns.md) 在您的Data Warehouse中，系統會要求您定義路徑，說明您要在上建立欄的表格與您要從中提取資訊的表格有何關聯。 若要成功建立路徑，您必須了解兩件事：

1. 資料庫中的表如何彼此關聯
1. 定義此關係的主鍵和外鍵

如果您知道此資訊，便可依照本文的指示輕鬆建立路徑。 如果您有點不確定，我們提供了這些概念的概述，但您可能想要詢問貴組織的技術專家，或聯絡我們的支援團隊。

## 表關係和鍵類型的刷新器 {#refresher}

### 表關係 {#relationships}

我們在我們的 [了解和評估表關係文章](../../data-analyst/data-warehouse-mgr/table-relationships.md)但簡短的總結從不傷害任何人，對吧？

表可以通過以下三種方式之一相互關聯：

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 人與駕照號之間的關係。 一個人只能擁有一個駕照號碼，而駕照號碼只屬於一個人。 |
| **`one-to-many`** | 訂單與物料之間的關係 — 訂單可以包含許多物料，但物料屬於單個訂單。 在這種情況下，訂單表是一側，項目表是多側。 |
| **`many-to-many`** | 產品與類別之間的關係：產品可以屬於許多類別，而類別可以包含許多產品。 |

{style=&quot;table-layout:auto&quot;}

了解兩個表之間的關係後，就可以用它來確定應建立哪條路徑，以將資訊從一個錶帶到另一個表。 下一步需要了解有助於表關係的主鍵和外鍵。

### 主鍵和外鍵 {#keys}

A `Primary Key` 是不會改變的列或一組列，在表內生成唯一值。 例如，當客戶在網站上下訂單時，會將新列新增至 `orders` 購物車中的表格，新 `order_id`. 此 `order_id` 允許客戶和企業跟蹤特定訂單的進度。 由於訂單ID是唯一的，因此通常是 `Primary Key` a `orders` 表格。

A `Foreign Key` 是在表內建立的欄，連結至 `Primary Key` 欄。 外鍵在表之間建立引用，使分析人員能夠輕鬆查找並將記錄連結在一起。 讓我們說，我們想知道哪些訂單屬於每個客戶。 此 `customer id` 欄()`Primary Key` 的 `customers` 表格)和 `order_id` 欄()`Foreign Key` 在 `customers` 表，引用 `Primary Key` 的 `orders` 表格)可讓我們連結及分析此資訊。 建立路徑時，系統會要求您定義 `Primary Key` 和 `Foreign Key`.

## 建立路徑 {#createpath}

在資料倉庫中建立欄時，您需要定義將資料從一個表格引入另一個表格的路徑。 有時，路徑會因為表之間已存在路徑而預先填入，但若未發生此情況，您將需要建立路徑。

我們利用 **客戶** 和 **訂購** 讓你看看是怎麼做的。 劃分：

* 這種關係 `one-to-many`  — 客戶可以有許多訂單，但訂單只能有一個客戶。 這會告訴我們關係的方向，或應建立計算欄的位置。 在此情況下，這表示 `orders` 表格可以帶入 `customers` 表格。
* 此 `primary key` 我們想用的是 `customers.customerid`，或 `customer ID` 欄中 `customers` 表格。
* 此 `foreign key` 我們想用的是 `orders.customerid`，或 `customer ID` 欄中 `orders` 表格。

現在，我們帶你們走過這條路。

1. 按一下 **[!UICONTROL Data > Data Warehouse]**.
1. 在表清單中，按一下要在中建立列的表。 在我們的範例中，這是 `customers` 表格。
1. 將顯示表架構。 按一下 **[!UICONTROL Create New Column]**.
1. 為欄命名，例如 `Customer's orders`.
1. 選取欄的定義。 查看 [計算欄指南](../data-warehouse-mgr/creating-calculated-columns.md) 找個方便的作弊證。
1. 在 [!UICONTROL Select table and column] 下拉式清單，按一下 **[!UICONTROL Create new path]** 選項。

   ![建立計算欄強制回應的路徑](../../assets/Creating_Paths_modal.png)

1. 使用下拉式清單，選取每個表格的主要和外鍵。

   在 `Many` 側選 `orders.customerid`  — 請記住，客戶可以有許多訂單。

   在 `One` 側選 `customers.customerid`  — 訂單只能有一個客戶。

1. 按一下 **[!UICONTROL Save]** 以保存路徑並完成建立列。

### 建立路徑的限制 {#limits}

* **[!DNL MBI]無法猜測主密鑰關係**. 我們不想在您的帳戶中引入不正確的資料，因此必須手動建立路徑。
* **目前，只能在兩個不同的表之間指定路徑**. 您嘗試重新建立的邏輯是否涉及兩個以上的表？ 然後，(1)先將欄加入中間表格，再將欄加入「最終目的地」表格，或(2)與我們的團隊協商，以找出最佳的方式達成您的目標，這可能是有意義的。
* **列一次只能是ONE路徑的外鍵引用**. 例如，若 `order_items.order_id` 指向 `orders.id`，然後 `order_items.order_id` 不能指向其他任何內容。
* **`Many-to-many`路徑在技術上是可以建立的，但經常會產生不良資料，因為兩者皆非真 `one-to-many` 外鍵**. 接近這些路徑的最佳方式一律取決於所需的特定分析。 請洽詢RJ分析團隊，找出最佳解決方案。

如果您因上述一或多個限制而無法建立計算欄，請聯絡支援人員，提供您所在欄的說明

## 刪除計算列路徑 {#delete}

在您的Data Warehouse中建立錯誤的路徑？ 或者你在做春洗，想整理一下？ 如果您需要從帳戶刪除路徑，您可以 [將票證發送給我們的支援分析員](../../guide-overview.md). **請務必包含路徑的名稱！**

## 包裝 {#wrapup}

您現在應已熟悉如何在Data Warehouse中建立計算欄的路徑。 如果您仍不確定特定路徑，請記住，您隨時可以按一下 **[!UICONTROL Support]** 在 [!DNL MBI] 帳戶以取得協助。

## 相關

* [了解和評估表關係](../data-warehouse-mgr/table-relationships.md)
* [建立計算欄的路徑](../data-warehouse-mgr/create-paths-calc-columns.md)
* [計算的列類型](../data-warehouse-mgr/calc-column-types.md) 嘗試建立。
