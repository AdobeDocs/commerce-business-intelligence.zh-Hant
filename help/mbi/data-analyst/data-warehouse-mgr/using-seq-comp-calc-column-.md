---
title: 順序比較計算列
description: 瞭解「順序比較」計算列的用途和用途。
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# 順序比較計算列

本主題概述了 `Sequential Comparison` 計算列在 **[!DNL Manage Data > Data Warehouse]** 的子菜單。 下面是它所做的說明，然後是一個示例和建立它的機制。

**解釋**

的 `Sequential Comparison` 列類型：查找連續事件之間的差異。 最常見的類型 `Sequential Comparison` 列 `Seconds since previous order` 的雙曲餘切值。 此欄需要三個輸入：

1. `Event Owner`:此輸入確定要為其分組的行的實體。 例如，在 `Seconds since previous order` 列中，事件所有者是客戶，因為您要查找自同一客戶的上一訂單以來的秒數。
1. `Event Date`:此輸入強制執行事件序列。 在 `Seconds since previous order`，包含訂單時間戳的列應為 `Event Date`。 此輸入始終是時間戳。
1. `Value to Compare`:此輸入是要比較的實際值。 它從當前行的值中減去上一行的值。 因此，調用查找客戶連續訂單之間時間差的列 `Seconds since previous order`。 此輸入不必是時間戳。 非時間戳示例是查找客戶連續訂單之間順序值的差。

**示例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | 空 |
| **`2`** | B | 2015-01-01 00:30:00 | 空 |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

在上例中， `Seconds since owner's previous event` 是 `Sequential Comparison` 計算列。 對於 `owner_id = A`它首先根據 `timestamp` 列，然後減去上一個事件 `timestamp` 從當前事件的時間戳。 在表的第三行中 — 第二行 `owner_id A`  — 資產價值 `Seconds since owner's previous event` 是「2015-01-01 02:00」和「2015-01-01 00」之間的秒數:00:00&#39; 這個差等於2小時= 7200秒。

對於此計算列類型，與所有者的第一個事件對應的行具有 `NULL` 值。

**力學**

建立 **事件編號** 列：

1. 導航到 **[!DNL Manage Data > Data Warehouse]** 的子菜單。

1. 導航到要在其上建立此列的表。

1. 按一下 **[!UICONTROL Create New Column]** 在右上角。

1. 選擇 `Same Table` 的 `Definition Type` （如果要比較的列不在同一個表中，則可能需要重新定位它們）。

1. 選擇 `SEQUENTIAL_COMPARISON` 的 `Column Definition Equation`。

1. 選擇輸入，如上所述：
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. 還可以添加篩選器以排除不考慮的行。 排除的行具有 `NULL` 值。

1. 提供頁面頂部列的名稱，然後按一下 **[!UICONTROL Save]**。

1. 該列可供使用 *立即*。

![秒](../../assets/SEC_new.png)
