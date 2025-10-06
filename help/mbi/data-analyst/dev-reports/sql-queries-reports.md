---
title: 將SQL查詢轉譯為Commerce Intelligence報表
description: 瞭解如何將SQL查詢轉譯為您在Commerce Intelligence中使用的計算量度。
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---

# 在Commerce Intelligence中翻譯SQL查詢

曾經想過如何將SQL查詢轉譯為您在[中使用的](../data-warehouse-mgr/creating-calculated-columns.md)計算資料行[、](../../data-user/reports/ess-manage-data-metrics.md)量度[和](../../tutorials/using-visual-report-builder.md)報表[!DNL Commerce Intelligence]？ 如果您是大量的SQL使用者，瞭解[!DNL Commerce Intelligence]中的SQL轉譯方式可讓您更聰明地在[Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md)中工作，並充分利用[!DNL Commerce Intelligence]平台。

在本主題結束時，您找到SQL查詢子句和&#x200B;**專案的**&#x200B;轉譯矩陣[!DNL Commerce Intelligence]。

從檢視一般查詢開始：

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | 報告`group by` |
| `SUM(b)` | `Aggregate function` （欄） |
| `FROM c` | `Source`資料表 |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 報告`time frame` |
| `GROUP BY a` | 報告`group by` |

此範例涵蓋大部分的翻譯案例，但有一些例外。 從`aggregate`函式的轉譯方式開始深入研究。

## 彙總函式

查詢中的彙總函式（例如，`count`、`sum`、`average`、`max`、`min`）採用&#x200B;**中的**&#x200B;量度彙總&#x200B;**或**&#x200B;資料行彙總[!DNL Commerce Intelligence]的形式。 差異因子是執行彙總是否需要聯結。

檢視上述每個專案的範例。

## 量度彙總 {#aggregate}

彙總`within a single table`時需要量度。 因此，以上查詢的`SUM(b)`彙總函式最可能由加總資料行`B`的量度表示。 

檢視`Total Revenue`量度在[!DNL Commerce Intelligence]中如何定義的特定範例。 檢視您嘗試翻譯的下方查詢：

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` （欄） |
| `FROM orders` | `Metric source`資料表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度`filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 量度`timestamp` （及報告`time range`） |

按一下「**[!UICONTROL Manage Data** > **&#x200B;量度&#x200B;**> **建立新量度]**」以瀏覽至量度產生器，您必須先選取適當的`source`表格（在此例中為`orders`表格）。 之後會設定量度，如下所示：

![量度彙總](../../assets/Metric_aggregation.png)

## 欄彙總

彙總從另一個表格聯結的欄時，需要計算欄。 舉例來說，您可能會在`customer`表格中建置名稱為`Customer LTV`的欄，其加總為`orders`表格中與該客戶相關聯的所有訂單的總值。

此彙總的查詢可能如下所示：

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | 彙總擁有者 |
| `SUM(o.order_total) as "Customer LTV"` | 彙總操作（欄） |
| `FROM customers c` | 彙總擁有者表格 |
| `JOIN orders o` | 彙總來源表格 |
| `ON c.customer_id = o.customer_id` | 路徑 |
| `WHERE o.status = 'success'` | 彙總篩選器 |

在[!DNL Commerce Intelligence]中設定此專案需要使用您的Data Warehouse管理員，您可以在其中建立`orders`與`customers`資料表之間的路徑，然後在客戶資料表中建立名為`Customer LTV`的資料行。

檢視如何在`customers`和`orders`之間建立新路徑。 最終目標是在`customers`資料表中建立新的彙總資料行，因此請先導覽至Data Warehouse中的`customers`資料表，然後按一下&#x200B;**[!UICONTROL Create a Column** > **&#x200B;選取定義&#x200B;**> **SUM]**。

接下來，您需要選取來源表格。 如果`orders`表格的路徑存在，只要從下拉式清單中選取它即可。 不過，如果您正在建立新路徑，請按一下「**[!UICONTROL Create new path]**」，下列畫面會顯示您：

![建立新路徑](../../assets/Create_new_path.png)

在此，您需要仔細考慮您嘗試加入的兩個表格之間的關係。 在此案例中，可能有`Many`個訂單與`One`客戶相關聯，因此`orders`表格列於`Many`側，而`customers`表格則列於`One`側。

>[!NOTE]
>
>在[!DNL Commerce Intelligence]中，`path`相當於SQL中的`Join`。

儲存路徑之後，您就可以建立`Customer LTV`欄！ 請參閱下文：

![使用SQL的客戶期限值分析動畫示範](../../assets/Customer_LTV.gif)

現在您已在`Customer LTV`資料表中建立新的`customers`資料行，您已準備好使用此資料行建立[量度彙總](#aggregate) （例如，找出每位客戶的平均LTV）。 您也可以`group by`或`filter`，依報表中的計算資料行，使用建置在`customers`資料表上的現有量度。

>[!NOTE]
>
>對於後者，無論何時建立新的計算資料行，您都必須[將維度新增至現有的量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)，才能將其用作`filter`或`group by`。

請參閱[使用您的Data Warehouse管理員建立計算資料行](../data-warehouse-mgr/creating-calculated-columns.md)。

## `Group By`子句

查詢中的`Group By`函式通常在[!DNL Commerce Intelligence]中表示為用來劃分或篩選視覺報表的欄。 例如，讓我們重新造訪您先前探索的`Total Revenue`查詢，但這次依`coupon\_code`劃分收入區段，以更清楚哪些優惠券產生最多收入。

從下列查詢開始：

| | |
|--- |--- |
| `SELECT coupon_code,` | 報告`group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`（欄） |
| `FROM orders` | `Metric source`資料表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度`filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 量度`timestamp` （及報告`time range`） |
| `GROUP BY coupon_code` | 報告`group by` |

>[!NOTE]
>
>與您之前開始的查詢唯一的差異在於新增「coupon\_code」作為群組依據。_

使用您先前建立的相同`Total Revenue`量度，您現在已準備好建立依優惠券代碼分段的收入報表！ 請看下方的gif，其中顯示如何設定此視覺報表，檢視9月至11月的資料：

![依據優惠券代碼收入](../../assets/Revenue_by_coupon_code.gif)

## 公式

有時候，為了計算不同欄之間的關係，查詢可能涉及多個彙總。 例如，您可以透過下列兩種方式之一計算查詢中的平均訂單值：

* `AVG('order\_total')`或
* `SUM('order\_total')/COUNT('order\_id')`

前一個方法會涉及建立新度量，該度量會在`order\_total`欄上執行平均值。 不過，後一種方法可以直接在Report Builder中建立，假設您已設定量度以計算`Total Revenue`和`Number of orders`。

後退一步，檢視`Average order value`的整體查詢：

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 量度`operation` （欄） |
| `COUNT(order_id) as "Number of orders"` | 量度`operation` （欄） |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 量度`operation` （欄） /量度作業（欄） |
| `FROM orders` | 量度`source`表格 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度`filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 量度時間戳記（以及報表時間範圍） |

現在假設您已設定量度以計算`Total Revenue`和`Number of orders`。 由於這些量度存在，您只需開啟`Report Builder`並使用`Formula`功能建立隨選計算即可：

![AOV公式](../../assets/AOV_forumula.gif)

## 正在結束

如果您是大量的SQL使用者，考慮如何在[!DNL Commerce Intelligence]中翻譯查詢可讓您建立計算欄、度量和報表。

如需快速參考，請檢視下方的矩陣。 這會顯示SQL子句的對等[!DNL Commerce Intelligence]專案，以及它如何對應至多個專案，這取決於查詢中如何使用該專案。

## Commerce Intelligence元素

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` （含時間元素） | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
