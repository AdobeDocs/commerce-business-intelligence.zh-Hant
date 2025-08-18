---
title: 建立或刪除計算欄的路徑
description: 瞭解如何定義路徑，描述您建立欄的表格如何與您從中提取資訊的表格相關。
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 建立或刪除計算欄的路徑

## 計算欄重新整理程式

在Data Warehouse中[建立計算資料行](../data-warehouse-mgr/creating-calculated-columns.md)時，系統會要求您定義一個路徑，描述您正在建立資料行的資料表如何與您正在擷取資訊的資料表相關。 若要成功建立路徑，您必須知道兩件事：

1. 資料庫中的資料表如何相互關聯
1. 定義此關係的主要和外部索引鍵

如果您知道此資訊，可以依照本主題中的指示輕鬆建立路徑。 您可能想要詢問貴組織的技術專家，或聯絡[Professional Services團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)。

## 重新整理表格關係和索引鍵型別 {#refresher}

### 表格關係 {#relationships}

此概念包含在[瞭解與評估資料表關聯性文章](../../data-analyst/data-warehouse-mgr/table-relationships.md)中，但快速摘要不會傷害任何人，對吧？

表格可以透過下列三種方式之一相互關聯：

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 人員與駕照號碼之間的關係。 一個人只能有一個駕駛執照號碼，而且一個駕駛執照號碼只屬於一個人。 |
| **`one-to-many`** | 訂單與料號之間的關係 — 一個訂單可以包含許多料號，但一個料號屬於單一訂單。 在這種情況下，訂單表格是一面，而料號表格是多面。 |
| **`many-to-many`** | 產品與類別之間的關係：產品可屬於許多類別，而類別可包含許多產品。 |

{style="table-layout:auto"}

瞭解兩個表格之間的關係時，就可使用它來決定應該建立哪個路徑，以將資訊從一個表格帶入另一個表格。 此下一個步驟需要瞭解有助於建立表格關係的主要和外部索引鍵。

### 主索引鍵和外部索引鍵 {#keys}

`Primary Key`是未變更的資料行或資料行集，會在資料表中產生唯一值。 例如，當客戶在網站上訂購時，購物車的`orders`表格中會新增一列，並附上新的`order_id`。 此`order_id`可讓客戶與企業追蹤該特定訂單的進度。 由於訂單ID是唯一的，因此它通常是`Primary Key`資料表的`orders`。

`Foreign Key`是在資料表內建立的資料行，連結到另一個資料表的`Primary Key`資料行。 外部索引鍵會建立表格之間的參考，讓分析師輕鬆查閱並連結記錄。 假設您想知道哪些訂單屬於您的每位客戶。 `customer id`資料行（`Primary Key`資料表的`customers`）與`order_id`資料行（`Foreign Key`資料表中的`customers`，參考`Primary Key`資料表的`orders`）可讓我們連結及分析此資訊。 建立路徑時，系統會要求您同時定義`Primary Key`和`Foreign Key`。

## 建立路徑 {#createpath}

在Data Warehouse中建立欄時，您必須定義將資訊從一個表格帶入另一個表格的路徑。 有時候，路徑會預先填入，因為表格之間存在路徑，但如果無法預先填入，則必須建立路徑。

使用&#x200B;**客戶**&#x200B;和&#x200B;**訂單**&#x200B;之間的關係來顯示如何完成它。 劃分：

* 關聯性為`one-to-many` — 客戶可以有多個訂單，但一個訂單只能有一個客戶。 這會告訴我們關係的方向，或是應該建立計算欄的位置。 在此情況下，這表示來自`orders`表格的資訊可以匯入`customers`表格。
* 您要使用的`primary key`是`customers.customerid`，或`customer ID`資料表中的`customers`資料行。
* 您要使用的`foreign key`是`orders.customerid`，或`customer ID`資料表中的`orders`資料行。

現在，您可以建立路徑。

1. 按一下&#x200B;**[!UICONTROL Data > Data Warehouse]**。
1. 在表格清單中，按一下要建立欄的表格。 在此範例中，它是`customers`資料表。
1. 表格結構描述隨即顯示。 按一下&#x200B;**[!UICONTROL Create New Column]**。
1. 為欄命名，例如`Customer's orders`。
1. 選取欄的定義。 檢視[計算資料行指南](../data-warehouse-mgr/creating-calculated-columns.md)以取得方便速查表。
1. 在[!UICONTROL Select table and column]下拉式清單中，按一下&#x200B;**[!UICONTROL Create new path]**&#x200B;選項。

   ![建立計算資料行的路徑模式](../../assets/Creating_Paths_modal.png)

1. 使用下拉式清單，選取每個表格的主要和外部索引鍵。

   在`Many`側，您選取`orders.customerid` — 請記住，客戶可以有許多訂單。

   在`One`端，您選取`customers.customerid` — 訂單只能有一個客戶。

1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以儲存路徑並完成欄的建立。

### 建立路徑的限制 {#limits}

* **[!DNL Commerce Intelligence]無法猜測主要/外部索引鍵關係**。 您不想將不正確的資料帶入帳戶，因此建立路徑必須手動完成。

* **目前只能在兩個不同的資料表**&#x200B;之間指定路徑。 您嘗試重新建立的邏輯是否涉及兩個以上的表格？ 然後(1)先將資料行聯結至中介表格，然後再聯結至「最終目的地」表格，或(2)洽詢[專業服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)，以找出達成目標的最佳方法，這樣做可能會有意義。

* **資料行一次只能是ONE路徑的外部索引鍵參考**。 例如，如果`order_items.order_id`指向`orders.id`，則`order_items.order_id`無法指向任何其他專案。

* 技術上可以建立&#x200B;**`Many-to-many`個路徑，但經常產生錯誤的資料，因為任何一方都不是真正的`one-to-many`外部索引鍵**。 接近這些路徑的最佳方式一律取決於所需的特定分析。 請洽詢RJ分析人員團隊，找出最佳解決方案。

如果由於上述一個或多個限制而無法建立計算欄，請聯絡支援人員並提供您目前所在欄的說明

## 刪除計算欄路徑 {#delete}

在您的Data Warehouse中建立了不正確的路徑？ 或者你正在做一些春季清潔工作，想整理一下？ 如果您需要刪除帳戶的路徑，您可以[傳送票證給Adobe支援分析師](../../guide-overview.md#Submitting-a-Support-Ticket)。 **請確定包含路徑的名稱！**

## 正在結束 {#wrapup}

現在您已熟悉如何在Data Warehouse中建立計算欄的路徑。 如果您仍不確定特定路徑，請記住，您隨時都可以按一下&#x200B;**[!UICONTROL Support]**&#x200B;帳戶中的[!DNL Commerce Intelligence]以取得協助。

## 相關

* [瞭解並評估表格關係](../data-warehouse-mgr/table-relationships.md)
* [建立計算欄的路徑](../data-warehouse-mgr/create-paths-calc-columns.md)
* [計算資料行型別](../data-warehouse-mgr/calc-column-types.md)正在嘗試建立。
