---
title: 事件編號計算列
description: 瞭解事件編號計算列的用途和用途。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---

# 事件編號計算列

本主題概述了 `Event Number` 計算列在 **[!DNL Manage Data > Data Warehouse]** 的子菜單。 下面是它所做的說明，然後是一個示例，以及建立它的機制。

**解釋**

的 `Event Number` 列類型標識特定事件發生的順序 **事件所有者**，例如 `customer` 或 `user`。 如果您熟悉SQL ，則此列類型與 `RANK` 的子菜單。 它可用於觀察資料中首次事件、重複事件或第n個事件之間的行為差異。

在打領帶時，此列包含相同 **秩** 跳過後續的數字。 例如，如果排名為5,8,10,10,12，則排名為1,2,3,3,5。

此欄最常見的使用案例是分析首次購買者和重複購買者。 通過將篩選器（添加到度量或報告）添加到 `Customer's order number` = 1。 `Customer's order number` 是類型的列 `Event Number`。

**示例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

在上例中，列 `Owner's event number` 是 `Event Number` 的雙曲餘切值。 它按事件發生的順序(根據 `timestamp` 列)。

例如，考慮所有行 `owner_id = A`。 表中的第一行是此所有者的最早時間戳，後跟表中的第三行，後跟表中的第四行。

**力學**

以下是有關建立 `Event Number` 列：

1. 導航到 **[!UICONTROL Manage Data > Data Warehouse]** 的子菜單。

1. 導航到要在其上建立此列的表。

1. 按一下 **[!UICONTROL Create a Column]** 選擇 `EVENT_NUMBER (…)` 列類型：下 `Same Table` 的子菜單。

1. 第一個下拉清單 `Event Owner` 指定要確定其等級的實體。 如果 `Customer's order number`，客戶標識符，如 `customer_id` 或 `customer_email` 會是 `Event Owner`。

1. 第二個下拉清單 `Event Rank` 指定強制執行確定行等級的序列的列。 如果 `Customer's order number`，也請參見Wiki頁。 `created_at` 時間戳是 `Event Rank`。

1. 在 `Options` 下拉清單中，您可以添加篩選器以排除考慮的行。 排除的行具有 `NULL` 值。

1. 為列提供名稱，然後按一下 **[!UICONTROL Save]**。

1. 該列可供使用 _立即。_
