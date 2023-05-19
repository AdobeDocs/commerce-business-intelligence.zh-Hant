---
title: 高級計算列類型
description: 瞭解大多數使用列案例的基本知識 — 但您可能希望計算的列比Data Warehouse管理器可以建立的列複雜得多。
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# 高級計算列類型

您可能要建立的許多分析都涉及使用 **新列** 你想 `group by` 或 `filter by`。 的 [建立計算列](../data-warehouse-mgr/creating-calculated-columns.md) 本教程介紹了大多數使用案例的基本知識，但您可能希望計算的列比Data Warehouse管理器可以建立的列複雜得多。
{:#top}

這些類型的列可由Adobe分析師Data Warehouse小組建立。 要定義新的計算列，請提供以下資訊：

1. 的 **`definition`** 列（包括輸入、公式或格式）
1. 的 **`table`** 要在上建立列
1. 任意 **`example data points`** 描述列應包含的內容

下面是一些用戶經常認為有用的高級計算列的常見示例：

* [按順序排列（或排名）事件](#compareevents)
* [查找兩個事件之間的時間](#twoevents)
* [比較順序事件值](#sequence)
* [轉換貨幣](#currency)
* [轉換時區](#timezone)
* [別的東西](#else)

## 我嘗試按順序排序事件 {#compareevents}

這稱為 **事件編號** 計算列。 這意味著您正在嘗試查找特定事件所有者（如客戶或用戶）發生事件的順序。

下面是一個示例：

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style="table-layout:auto"}

事件編號計算列可用於觀察資料中首次事件、重複事件或第n個事件之間的行為差異。

是否要查看「客戶的訂單編號」列的操作？ 按一下該影像，以查看它用作報表中的「按組」維。

![使用事件編號計算列按客戶的訂單編號分組。](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

要建立此類型的計算列，您需要知道：

* 要在其上建立此列的表
* 標識事件所有者的欄位(`owner\_id` 在本示例中)
* 要用於訂購事件的欄位(`timestamp` 在本示例中)

[返回頂部](#top)

## 我在努力尋找兩個事件之間的時間。 {#twoevents}

這叫做 `date difference` 計算列。 這意味著您正試圖根據事件時間戳查找屬於單個記錄的兩個事件之間的時間。

下面是一個示例：

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}

日期差計算列可用於建立度量，該度量計算兩個事件之間的平均時間或中值時間。 按一下下面的影像，檢查 `Average time to first order` 度量用於報告。

![使用日期差計算列計算「平均到一階」時間。](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

要建立此類型的計算列，您需要知道：

* 要在其上建立此列的表
* 你想知道的兩個時間戳

[返回頂部](#top)

## 我正在嘗試比較順序事件值。 {#sequence}

這叫做 **順序事件比較**。 這意味著您正試圖查找值（貨幣、數字、時間戳）與所有者上一事件的相應值之間的差值。

下面是一個示例：

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 空 |
| 2 | `B` | 2015-01-01 00:30:00 | 空 |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style="table-layout:auto"}

順序事件比較可用於查找每個順序事件之間的平均時間或中值時間。 按一下下面的影像查看 **訂單間的平均時間和中值時間** 指標。

=![使用順序事件比較計算列計算訂單之間的平均時間和中值時間。](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

要建立此類型的計算列，您需要知道：

* 要在其上建立此列的表
* 標識事件所有者的欄位(`owner\_id` )
* 要查看每個連續事件之間差異的值欄位(`timestamp` 在本示例中)

[返回頂部](#top)

## 我在嘗試兌換貨幣。 {#currency}

A **貨幣兌換** 計算列根據事件時的匯率將事務處理金額從記錄幣種轉換為報告幣種。

下面是一個示例：

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30 | 33.57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55.93 |

{style="table-layout:auto"}

要建立此類型的計算列，您需要知道：

* 要在其上建立此列的表
* 要轉換的交易記錄金額列
* 指示資料記錄的幣種的列（通常為ISO代碼）
* 首選報告幣種

[返回頂部](#top)

## 我正在嘗試轉換時區。 {#timezone}

A **時區轉換** calculated列將特定資料源的時間戳從其記錄的時區轉換為報告時區。

下面是一個示例：

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style="table-layout:auto"}

要建立此類型的計算列，您需要知道：

* 要在其上建立此列的表
* 要轉換的時間戳列
* 記錄資料的時區
* 首選報告時區

[返回頂部](#top)

## 我正在嘗試做一件沒有列在這裡的事情。 {#else}

別擔心。 不是因為這裡沒有列出，就不意味著不可能。 Adobe分析師團隊可以提供幫助。

要定義新的計算列， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 詳細說明您想要構建什麼。

## 相關文檔

* [建立計算列](../data-warehouse-mgr/creating-calculated-columns.md)
* [計算的列類型](../data-warehouse-mgr/calc-column-types.md)
* [大樓 [!DNL Google ECommerce] 包含訂單和客戶資料的維](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
