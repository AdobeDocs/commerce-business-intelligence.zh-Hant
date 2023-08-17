---
title: 將SQL查詢轉譯為Commerce Intelligence報表
description: 瞭解如何將SQL查詢轉譯為您在Commerce Intelligence中使用的計算量度。
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 在Commerce Intelligence中翻譯SQL查詢

曾經想知道如何將SQL查詢轉譯為 [已計算的欄](../data-warehouse-mgr/creating-calculated-columns.md)， [量度](../../data-user/reports/ess-manage-data-metrics.md)、和 [報表](../../tutorials/using-visual-report-builder.md) 您使用於 [!DNL Commerce Intelligence]？ 如果您是大量的SQL使用者，請瞭解SQL的轉譯方式 [!DNL Commerce Intelligence] 可讓您更聰明地在 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md) 並充分利用 [!DNL Commerce Intelligence] 平台。

在本主題結束時，您會找到 **翻譯矩陣** 用於SQL查詢子句和 [!DNL Commerce Intelligence] 元素。

從檢視一般查詢開始：

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | 報告 `group by` |
| `SUM(b)` | `Aggregate function` （欄） |
| `FROM c` | `Source` 表格 |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 報告 `time frame` |
| `GROUP BY a` | 報告 `group by` |

此範例涵蓋大部分的翻譯案例，但有一些例外。 深入瞭解，從如何 `aggregate` 函式已翻譯。

## 彙總函式

彙總函式(例如 `count`， `sum`， `average`， `max`， `min`)在查詢中，可以採用以下形式 **量度彙總** 或 **欄彙總** 在 [!DNL Commerce Intelligence]. 差異因子是執行彙總是否需要聯結。

檢視上述每個專案的範例。

## 量度彙總 {#aggregate}

彙總時需要量度 `within a single table`. 舉例來說， `SUM(b)` 來自上述查詢的彙總函式很可能以總和欄的量度表示 `B`. 

檢視特定範例，瞭解如何 `Total Revenue` 量度可定義於 [!DNL Commerce Intelligence]. 檢視您嘗試翻譯的下方查詢：

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` （欄） |
| `FROM orders` | `Metric source` 表格 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 量度 `timestamp` （和報表） `time range`) |

按一下「 」，導覽至量度產生器 **[!UICONTROL Manage Data** > **&#x200B;量度&#x200B;**> **建立新量度]**，您必須先選取適當的 `source` 表格，在此例中為 `orders` 表格。 之後會設定量度，如下所示：

![量度彙總](../../assets/Metric_aggregation.png)

## 欄彙總

彙總從另一個表格聯結的欄時，需要計算欄。 舉例來說，您可能已內建一欄， `customer` 已呼叫的資料表 `Customer LTV`，會加總與該客戶相關聯的所有訂單在 `orders` 表格。

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

在中設定此專案 [!DNL Commerce Intelligence] 需要使用Data Warehouse管理員，您可在此處建立 `orders` 和 `customers` 然後建立名為的欄 `Customer LTV` 在您客戶的表格中。

瞭解如何在 `customers` 和 `orders`. 最終目標是在以下位置建立新的彙總欄： `customers` 表格，因此請先導覽至 `customers` Data Warehouse表格，然後按一下 **[!UICONTROL Create a Column** > **&#x200B;選取定義&#x200B;**> **SUM]**.

接下來，您需要選取來源表格。 如果路徑存在 `orders` 表格，只要從下拉式清單中選取它即可。 不過，如果您要建立新路徑，請按一下 **[!UICONTROL Create new path]** 而且畫面如下：

![建立新路徑](../../assets/Create_new_path.png)

在此，您需要仔細考慮您嘗試加入的兩個表格之間的關係。 在此情況下，潛在 `Many` 訂單關聯至 `One` 客戶，因此 `orders` 表格會列於 `Many` 側，而 `customers` 表格選取於 `One` 側。

>[!NOTE]
>
>在 [!DNL Commerce Intelligence]， a `path` 相當於 `Join` 在SQL中。

儲存路徑後，您可以建立 `Customer LTV` 欄！ 請參閱下文：

![](../../assets/Customer_LTV.gif)

現在您已建置新的 `Customer LTV` 中的欄 `customers` 表格，您已準備建立 [量度彙總](#aggregate) 使用此欄（例如，找出每位客戶的平均LTV）。 您也可以 `group by` 或 `filter` 的計算欄劃分(使用建立在 `customers` 表格。

>[!NOTE]
>
>對於後者，無論何時建立新的計算欄，您都必須 [將維度新增至現有量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 在它可用作 `filter` 或 `group by`.

另請參閱 [建立計算欄](../data-warehouse-mgr/creating-calculated-columns.md) 與您的Data Warehouse管理員。

## `Group By` 子句

`Group By` 查詢中的函式通常以下列表示： [!DNL Commerce Intelligence] 作為用來劃分或篩選視覺報表的欄。 例如，讓我們重新造訪 `Total Revenue` 您先前探索的查詢，但這次是依 `coupon\_code` 以更清楚哪些優惠券產生最多收入。

從下列查詢開始：

| | |
|--- |--- |
| `SELECT coupon_code,` | 報告 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`（欄） |
| `FROM orders` | `Metric source` 表格 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 量度 `timestamp` （和報表） `time range`) |
| `GROUP BY coupon_code` | 報告 `group by` |

>[!NOTE]
>
>與您之前開始的查詢唯一的差異在於新增「coupon\_code」作為群組依據。_

使用相同的 `Total Revenue` 您先前建立的量度，現在已準備好建立依優惠券代碼分段的收入報表！ 請看下方的gif，其中顯示如何設定此視覺報表，檢視9月至11月的資料：

![依優惠券代碼收入](../../assets/Revenue_by_coupon_code.gif)

## 公式

有時候，為了計算不同欄之間的關係，查詢可能涉及多個彙總。 例如，您可以透過下列兩種方式之一計算查詢中的平均訂單值：

* `AVG('order\_total')` 或
* `SUM('order\_total')/COUNT('order\_id')`

前者會涉及建立新度量，此度量會對 `order\_total` 欄。 不過，後者可直接在Report Builder中建立，假設您已設定量度以計算 `Total Revenue` 和 `Number of orders`.

後退一步，檢視整體查詢 `Average order value`：

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 量度 `operation` （欄） |
| `COUNT(order_id) as "Number of orders"` | 量度 `operation` （欄） |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 量度 `operation` （欄） /量度作業（欄） |
| `FROM orders` | 量度 `source` 表格 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 量度時間戳記（以及報表時間範圍） |

現在假設您已設定量度以計算 `Total Revenue` 和 `Number of orders`. 由於存在這些量度，因此您可以直接開啟 `Report Builder` 並使用以下方式建立隨選計算 `Formula` 功能：

![AOV公式](../../assets/AOV_forumula.gif)

## 正在結束

如果您是大量的SQL使用者，請考慮如何在中翻譯查詢 [!DNL Commerce Intelligence] 可讓您建立計算欄、量度和報表。

如需快速參考，請檢視下方的矩陣。 這會顯示SQL子句的對等專案 [!DNL Commerce Intelligence] 元素以及其如何對應至多個元素，端視其在查詢中的使用方式而定。

## Commerce Intelligence元素

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` （含時間元素） | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
