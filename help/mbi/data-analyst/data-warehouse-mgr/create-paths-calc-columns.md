---
title: 為計算列建立或刪除路徑
description: 瞭解如何定義路徑，說明您要在其上建立列的表如何與要從中提取資訊的表相關。
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# 為計算列建立或刪除路徑

## 計算列刷新程式

當 [建立計算列](../data-warehouse-mgr/creating-calculated-columns.md) 在您的Data Warehouse中，系統要求您定義一個路徑，該路徑描述您正在建立的列的表如何與要從中提取資訊的表相關。 要成功建立路徑，您需要瞭解兩件事：

1. 資料庫中的表如何相互關聯
1. 定義此關係的主鍵和外鍵

如果您知道此資訊，則可以按照本主題中的說明輕鬆建立路徑。 您可能希望向組織中的技術專家咨詢，或與 [專業服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## 表關係和鍵類型的刷新程式 {#refresher}

### 表關係 {#relationships}

此概念在 [瞭解和評估表關係項目](../../data-analyst/data-warehouse-mgr/table-relationships.md)但簡短的摘要不會傷害任何人，對吧？

表可以通過以下三種方式之一相互關聯：

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 人與駕照號碼的關係。 一個人只能有一個駕駛證號，一個駕駛證號只屬於一個人。 |
| **`one-to-many`** | 訂單和物料之間的關係 — 訂單可以包含許多物料，但物料屬於單個訂單。 在這種情況下，訂單表是一方，物料表是多方。 |
| **`many-to-many`** | 產品與類別之間的關係：一個產品可以屬於多個類別，一個類別可以包含多個產品。 |

{style="table-layout:auto"}

當瞭解兩個表之間的關係時，可以用它來確定應建立什麼路徑來將資訊從一個錶帶到另一個表。 下一步需要瞭解有助於表關係的主鍵和外鍵。

### 主鍵和外鍵 {#keys}

A `Primary Key` 是一個不變的列或一組在表中產生唯一值的列。 例如，當客戶在網站上訂單時，將向 `orders` 購物車中的桌子， `order_id`。 此 `order_id` 允許客戶和企業跟蹤特定訂單的進度。 由於訂單ID是唯一的，因此 `Primary Key` 的 `orders` 的子菜單。

A `Foreign Key` 是在表內建立的列，該表連結到 `Primary Key` 列。 外鍵在表之間建立引用，使分析員能夠輕鬆查找並將記錄連結在一起。 說你想知道你每個顧客的訂單。 的 `customer id` 列(`Primary Key` 的 `customers` 表)和 `order_id` 列(`Foreign Key` 的 `customers` 表，引用 `Primary Key` 的 `orders` 表)允許我們連結和分析此資訊。 建立路徑時，系統會要求您定義 `Primary Key` 和 `Foreign Key`。

## 建立路徑 {#createpath}

在Data Warehouse中建立列時，必須定義將資訊從一個錶帶到另一個表的路徑。 有時，由於表之間存在路徑，因此預填充路徑，但如果不存在，則必須建立路徑。

使用 **客戶** 和 **訂單** 來給你看看是怎麼做的。 分解：

* 關係是 `one-to-many`  — 客戶可以有多個訂單，但訂單只能有一個客戶。 這將告訴我們關係的方向，或應在何處建立計算列。 在本例中，它意味著 `orders` 可以把桌子帶進 `customers` 的子菜單。
* 的 `primary key` 你想用的是 `customers.customerid`，或 `customer ID` 列 `customers` 的子菜單。
* 的 `foreign key` 你想用的是 `orders.customerid`，或 `customer ID` 列 `orders` 的子菜單。

現在，您可以建立路徑。

1. 按一下 **[!UICONTROL Data > Data Warehouse]**。
1. 在表清單中，按一下要在其中建立列的表。 在本例中，它是 `customers` 的子菜單。
1. 將顯示表架構。 按一下 **[!UICONTROL Create New Column]**。
1. 給列一個名稱，例如， `Customer's orders`。
1. 選擇列的定義。 查看 [計算列指南](../data-warehouse-mgr/creating-calculated-columns.md) 找份方便的作弊單。
1. 在 [!UICONTROL Select table and column] 下拉菜單，按一下 **[!UICONTROL Create new path]** 的雙曲餘切值。

   ![為計算列模式建立路徑](../../assets/Creating_Paths_modal.png)

1. 使用下拉清單，為每個表選擇主鍵和外鍵。

   在 `Many` 側，選擇 `orders.customerid`  — 請記住，客戶可以有許多訂單。

   在 `One` 側，選擇 `customers.customerid`  — 訂單只能有一個客戶。

1. 按一下 **[!UICONTROL Save]** 以保存路徑並完成列的建立。

### 建立路徑的限制 {#limits}

* **[!DNL Commerce Intelligence]無法猜測主鍵關係**。 您不想在帳戶中引入不正確的資料，因此必須手動建立路徑。

* **當前，只能在兩個不同的表之間指定路徑**。 您嘗試重新建立的邏輯是否涉及兩個以上的表？ 然後，(1)先將列連接到中間表，然後再連接到「最終目標」表，或(2)與 [專業服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 找到實現目標的最佳方法。

* **列一次只能是ONE路徑的外鍵引用**。 例如，如果 `order_items.order_id` 指向 `orders.id`，則 `order_items.order_id` 不能指向其他任何東西。

* **`Many-to-many`路徑可以在技術上建立，但通常會產生壞資料，因為兩者都不是真的 `one-to-many` 外鍵**。 接近這些路徑的最佳方法總是取決於特定的期望分析。 請咨詢RJ分析團隊，以發現最佳解決方案。

如果由於上述一個或多個限制而無法建立計算列，請與支援人員聯繫，瞭解您所在列的說明

## 刪除計算列路徑 {#delete}

在Data Warehouse中建立了錯誤路徑？ 或者你在做彈簧清理，想收拾一下？ 如果需要從帳戶中刪除路徑，您可以 [給Adobe支援分析師發票](../../guide-overview.md#Submitting-a-Support-Ticket)。 **請確保包含路徑的名稱！**

## 收尾 {#wrapup}

現在，您可以輕鬆地在Data Warehouse中為計算列建立路徑。 如果您仍不確定特定路徑，請記住，您始終可以按一下 **[!UICONTROL Support]** 在 [!DNL Commerce Intelligence] 帳戶以獲得幫助。

## 相關

* [瞭解和評估表關係](../data-warehouse-mgr/table-relationships.md)
* [為計算列建立路徑](../data-warehouse-mgr/create-paths-calc-columns.md)
* [計算列類型](../data-warehouse-mgr/calc-column-types.md) 嘗試建立。
