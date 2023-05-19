---
title: 使用日期差異計算列
description: 瞭解「日期差額」計算列的用途和用途。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 日期差值計算列

本主題概述了 `Date Difference` 計算列在 **[!DNL Manage Data > Data Warehouse]** 的子菜單。 下面是它所做的說明，然後是一個示例，以及建立它的機制。

**解釋**

的 `Date Difference` 列類型根據事件時間戳計算屬於單個記錄的兩個事件之間的時間。 此列中計算的原始值以秒為單位，但會自動轉換為分鐘、小時、天等，以便在報告中顯示。 但是，當用作篩選器/分組依據時，您希望以秒為單位使用該值。

A `date difference` 可以使用計算列來建立度量，該度量計算兩個事件之間的平均時間或中值時間，例如客戶註冊和它們的第一個訂單之間的平均時間。

**示例**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


在上例中， `Date Difference` 列 `Seconds between timestamp_2 and timestamp_1` 的雙曲餘切值。 它執行計算 `timestamp_2 minus timestamp_1`。

**力學**

以下步驟說明如何建立 `Date Difference` 的雙曲餘切值。

1. 導航到 **[!DNL Manage Data > Data Warehouse]** 的子菜單。
1. 導航到要在其上建立此列的表。
1. 按一下 **[!UICONTROL Create a Column]** 並配置列，如下所示：
   * 選擇 `Column Definition Type` > `Same Table`
   * 選擇 `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * 選擇 `Ending DATETIME` 列>選擇結束日期時間欄位，該欄位通常是以後發生的事件
   * 選擇 `Starting DATETIME` column** >選擇開始日期時間欄位，該欄位通常是早期發生的事件

1. 為列提供名稱，然後按一下 **[!UICONTROL Save]**。
1. 該列可供使用 *立即*。

作為示例，以下示例配置為計算 `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
