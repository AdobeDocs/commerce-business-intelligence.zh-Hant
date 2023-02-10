---
title: 事件編號計算列
description: 了解「事件編號」計算欄的用途和用途。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---

# 事件編號計算列

本主題概述 `Event Number` 可用的計算欄 **[!DNL Manage Data > Data Warehouse]** 頁面。 以下是其功能的說明，其後是範例，以及建立範例的機制。

**說明**

此 `Event Number` 欄類型：識別特定事件發生的順序 **事件擁有者**，如 `customer` 或 `user`. 如果您熟悉SQL，則此列類型與 `RANK` 函式。 它可用來觀察資料中首次事件、重複事件或第n個事件之間的行為差異。

若是系結，此欄包含相同 **排名** ，並略過後續的數字。 例如，如果排名為5,8,10,10,12，則排名為1,2,3,3,5。

此欄最常見的使用案例是分析首次購買者和重複購買者。 首次購買者的識別方式，是將篩選器（新增至量度或報表） `Customer's order number` = 1。 `Customer's order number` 是類型的列 `Event Number`.

**範例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

在上例中，欄 `Owner's event number` 是 `Event Number` 欄。 它會依發生的順序來排列擁有者事件(根據 `timestamp` 欄)。

例如，請考慮 `owner_id = A`. 表格中的第一行是此所有者的最早時間戳，後跟表格中的第三行，後跟表格中的第四行。

**力學**

以下是建立 `Event Number` 欄：

1. 導覽至 **[!UICONTROL Manage Data > Data Warehouse]** 頁面。
1. 導覽至您要建立此欄的表格。
1. 按一下 **[!UICONTROL Create a Column]** 並選擇 `EVENT_NUMBER (…)` 欄類型：在 `Same Table` 區段。
1. 第一個下拉式清單 `Event Owner` 指定要為其確定排名的實體。 若 `Customer's order number`，客戶識別碼，例如 `customer_id` 或 `customer_email` 會是 `Event Owner`.
1. 第二個下拉式清單 `Event Rank` 指定執行決定行排名的序列的列。 若 `Customer's order number`, `created_at` 時間戳記會是 `Event Rank`.
1. 在 `Options` 下拉式清單中，您可以新增篩選器以排除不會考慮列。 排除的列會具有 `NULL` 值。
1. 為欄提供名稱，然後按一下 **[!UICONTROL Save]**.
1. 欄將可供使用 _立即。_
