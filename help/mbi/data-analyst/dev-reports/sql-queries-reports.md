---
title: 將SQL查詢轉換為Commerce Intelligence報表
description: 瞭解SQL查詢如何轉換為計算列（在Commerce Intelligence中使用的度量）。
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 在Commerce Intelligence中轉換SQL查詢

曾想知道SQL查詢如何轉換為 [計算列](../data-warehouse-mgr/creating-calculated-columns.md)。 [度量](../../data-user/reports/ess-manage-data-metrics.md), [報告](../../tutorials/using-visual-report-builder.md) 您使用 [!DNL Commerce Intelligence]？如果您是SQL用戶，請瞭解SQL的轉換方式 [!DNL Commerce Intelligence] 使您能夠在 [Data Warehouse管理器](../data-warehouse-mgr/tour-dwm.md) 最充分地利用 [!DNL Commerce Intelligence] 平台。

在本主題的末尾，您會發現 **平移矩陣** 用於SQL查詢子句和 [!DNL Commerce Intelligence] 元素。

首先查看一般查詢：

|  |  |
|--- |--- |
| `SELECT` |  |
| `a,` | 報告 `group by` |
| `SUM(b)` | `Aggregate function` （列） |
| `FROM c` | `Source` 表 |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 報告 `time frame` |
| `GROUP BY a` | 報告 `group by` |

此示例涵蓋大多數翻譯案例，但有一些例外。 潛入，從 `aggregate` 函式。

## 集合函式

集合函式(例如， `count`。 `sum`。 `average`。 `max`。 `min`)中的 **度量聚合** 或 **列聚合** 在 [!DNL Commerce Intelligence]。 區分因素是是否需要連接來執行聚合。

請看上面每個示例。

## 度量聚合 {#aggregate}

聚合時需要度量 `within a single table`。 比如， `SUM(b)` 上述查詢中的集合函式很可能由對列求和的度量表示 `B`。 

請看一個具體示例 `Total Revenue` 度量可能在中定義 [!DNL Commerce Intelligence]。 查看下面嘗試翻譯的查詢：

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` （列） |
| `FROM orders` | `Metric source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 度量 `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 度量 `timestamp` （和報告） `time range`) |

通過按一下導航到度量生成器 **[!UICONTROL Manage Data** > **&#x200B;度量&#x200B;**> **建立新度量]**，必須首先選擇 `source` 表，在本例中 `orders` 的子菜單。 然後，將按如下所示設定度量：

![度量聚合](../../assets/Metric_aggregation.png)

## 列聚合

聚合從另一個表聯接的列時需要計算列。 例如，您可能在您的 `customer` 表調用 `Customer LTV`，該值將與該客戶關聯的所有訂單的總值 `orders` 的子菜單。

此聚合的查詢可能如下所示：

|  |  |
|--- |--- |
| `Select` |  |
| `c.customer_id` | 聚合所有者 |
| `SUM(o.order_total) as "Customer LTV"` | 聚合操作（列） |
| `FROM customers c` | 聚合所有者表 |
| `JOIN orders o` | 聚合源表 |
| `ON c.customer_id = o.customer_id` | 路徑 |
| `WHERE o.status = 'success'` | 聚合篩選器 |

設定 [!DNL Commerce Intelligence] 需要使用Data Warehouse管理器，在其中在 `orders` 和 `customers` 然後建立名為 `Customer LTV` 在客戶的桌子上。

查看如何在 `customers` 和 `orders`。 最終目標是在 `customers` 表，因此首先導航到 `customers` 表格，然後按一下 **[!UICONTROL Create a Column** > **&#x200B;選擇定義&#x200B;**> **求和]**。

接下來，需要選擇源表。 如果路徑存在於 `orders` ，只需從下拉清單中選擇它即可。 但是，如果要生成新路徑，請按一下 **[!UICONTROL Create new path]** 螢幕顯示如下：

![建立新路徑](../../assets/Create_new_path.png)

在此，您需要仔細考慮您嘗試加入的兩個表之間的關係。 在這個例子中， `Many` 關聯的訂單 `One` 客戶，因此 `orders` 表列在 `Many` 側，而 `customers` 表 `One` 邊。

>[!NOTE]
>
>在 [!DNL Commerce Intelligence]的 `path` 等於 `Join` 中。

保存路徑後，可以建立 `Customer LTV` 欄！ 請參見以下內容：

![](../../assets/Customer_LTV.gif)

既然你已經建好了 `Customer LTV` 列 `customers` 表，您已準備好建立 [度量聚集](#aggregate) 使用此列（例如，查找每個客戶的平均LTV）。 您也可以 `group by` 或 `filter` 使用基於 `customers` 的子菜單。

>[!NOTE]
>
>對於後者，無論何時生成新的計算列，都必須 [將維添加到現有度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 在它作為 `filter` 或 `group by`。

請參閱 [建立計算列](../data-warehouse-mgr/creating-calculated-columns.md) 你的Data Warehouse經理。

## `Group By` 條款

`Group By` 查詢中的函式通常表示在 [!DNL Commerce Intelligence] 列，用於段或篩選可視報表。 例如，讓我們重訪 `Total Revenue` 查詢，但此時按收入分段 `coupon\_code` 更好地瞭解哪些優惠券能產生最多收入。

從以下查詢開始：

|  |  |
|--- |--- |
| `SELECT coupon_code,` | 報告 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`（列） |
| `FROM orders` | `Metric source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 度量 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 度量 `timestamp` （和報告） `time range`) |
| `GROUP BY coupon_code` | 報告 `group by` |

>[!NOTE]
>
>與之前啟動的查詢唯一的區別是添加「優惠券\_code」作為分組依據。_

使用相同 `Total Revenue` 您以前建立的指標，現在您已準備好建立按優惠券代碼劃分的收入報告！ 請查看下面的gif，其中顯示如何設定查看9月至11月資料的此可視報告：

![按優惠券代碼列出的收入](../../assets/Revenue_by_coupon_code.gif)

## 公式

有時，查詢可能涉及多個聚合以計算不同列之間的關係。 例如，可以通過以下兩種方法之一計算查詢中的平均順序值：

* `AVG('order\_total')` 或
* `SUM('order\_total')/COUNT('order\_id')`

前一種方法將涉及建立新度量，該度量在 `order\_total` 的雙曲餘切值。 但是，後一種方法可以直接在報表生成器中建立，前提是您已設定了用於計算 `Total Revenue` 和 `Number of orders`。

退一步，查看整個查詢 `Average order value`:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 度量 `operation` （列） |
| `COUNT(order_id) as "Number of orders"` | 度量 `operation` （列） |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 度量 `operation` （列）/度量操作（列） |
| `FROM orders` | 度量 `source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 度量 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 度量時間戳（和報告時間範圍） |

現在假設您已設定度量以計算 `Total Revenue` 和 `Number of orders`。 由於存在這些度量，因此您只需開啟 `Report Builder` 並使用 `Formula` 功能：

![AOV公式](../../assets/AOV_forumula.gif)

## 包裝

如果您是SQL用戶，請考慮查詢如何轉換 [!DNL Commerce Intelligence] 使您能夠生成計算列、度量和報表。

要快速參考，請查看下面的矩陣。 這顯示SQL子句的等效項 [!DNL Commerce Intelligence] 元素，以及它如何映射到多個元素，具體取決於它在查詢中的使用方式。

## 商業智慧元素

|**`SQL Clause`**|**`Metric`**|**`Filter`**|**`Report group by`**|**`Report time frame`**|**`Path`**|**`Calculated column inputs`**|**`Source table`**| |—|—|—||—| |`SELECT`|X|-|X|-|-|X|-| |`FROM`|-|-|-|-|-|-|-|-|X| |`WHERE`|-|X|-|-|-|-|-| |`WHERE` （含時間元素）|-|-|-|X|-|-|-| |`JOIN...ON`|-|X|-|-|X|X|-| |`GROUP BY`|-|-|X|-|-|-|-|
