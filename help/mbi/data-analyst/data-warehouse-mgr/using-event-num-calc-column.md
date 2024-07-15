---
title: 事件編號計算欄
description: 瞭解「事件編號」計算欄的用途和用途。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 事件編號計算欄

此主題概述&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;頁面中可用`Event Number`計算欄的用途和用途。 以下是其功能的說明，隨後是一個範例，以及建立它的機制。

**說明**

`Event Number`資料行型別識別特定&#x200B;**事件擁有者** （如`customer`或`user`）發生事件的順序。 如果您熟悉SQL，則此資料行型別與`RANK`函式相同。 它可用來觀察資料中首次事件、重複事件或第n個事件之間的行為差異。

在並列的情況下，此欄包含與並列事件相同的&#x200B;**排名**，並略過後續的數字。 例如，如果對數字進行排名5,8，10,10,12，則排名將是1,2，3,3，5。

此欄最常見的使用案例是分析首次購買者和重複購買者。 第一次透過在`Customer's order number` = 1上新增篩選器（至量度或報告）來識別購買者。 `Customer's order number`是型別`Event Number`的資料行。

**範例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

在上述範例中，資料行`Owner's event number`是`Event Number`資料行。 它會根據事件的發生順序（根據`timestamp`欄）對擁有者的事件進行排名。

例如，考慮`owner_id = A`的所有資料列。 表格中的第一列是此擁有者最早的時間戳記，後面是表格中的第三列，後面是表格中的第四列。

**機械**

以下是建立`Event Number`欄的一些指示：

1. 導覽至&#x200B;**[!UICONTROL Manage Data > Data Warehouse]**&#x200B;頁面。

1. 導覽至您要建立此欄的表格。

1. 按一下&#x200B;**[!UICONTROL Create a Column]**&#x200B;並選擇`Same Table`區段下的`EVENT_NUMBER (…)`欄型別： 。

1. 第一個下拉式清單`Event Owner`指定要決定排名的實體。 在`Customer's order number`的情況下，`customer_id`或`customer_email`等客戶識別碼將是`Event Owner`。

1. 第二個下拉式清單`Event Rank`指定強制執行決定資料列排名的順序的資料行。 在`Customer's order number`的情況下，`created_at`時間戳記將是`Event Rank`。

1. 在`Options`下拉式清單下，您可以新增篩選器以排除不予以考慮的列。 排除的資料列有此資料行的`NULL`值。

1. 提供資料行的名稱，然後按一下&#x200B;**[!UICONTROL Save]**。

1. 資料行可以立即使用&#x200B;_。_
