---
title: 循序比較計算欄
description: 瞭解「循序比較」計算欄的用途和用途。
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 循序比較計算欄

此主題概述&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;頁面中可用`Sequential Comparison`計算欄的用途和用途。 以下是其功能的說明，然後是一個範例和建立它的機制。

**說明**

`Sequential Comparison`欄型別：尋找連續事件之間的差異。 最常見的`Sequential Comparison`資料行型別是`Seconds since previous order`資料行。 此欄需要三個輸入：

1. `Event Owner`：此輸入決定要將列分組的實體。 例如，在`Seconds since previous order`欄中，事件擁有者是客戶，因為您想要尋找自相同客戶的上次訂購以來的秒數。
1. `Event Date`：此輸入會強制事件順序。 在`Seconds since previous order`的情況下，包含訂單時間戳記的資料行應為`Event Date`。 此輸入一律為時間戳記。
1. `Value to Compare`：此輸入是要比較的實際值。 它會從目前列的值減去前一列的值。 因此，尋找客戶連續訂單之間時間差異的欄稱為`Seconds since previous order`。 此輸入不一定要是時間戳記。 非時間戳記範例是找出客戶連續訂單之間的訂單值差異。

**範例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | 空 |
| **`2`** | B | 2015-01-01 00:30:00 | 空 |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

在上述範例中，`Seconds since owner's previous event`是`Sequential Comparison`計算資料行。 對於`owner_id = A`，它會先根據`timestamp`資料行識別順序，然後從目前事件的時間戳記中減去先前事件的`timestamp`。 在表格的第三列 — `owner_id A`的第二列 — `Seconds since owner's previous event`的值是&#39;2015-01-01 02:00&#39;和&#39;2015-01-01 00:00:00&#39;之間的秒數。 此差異等於兩個小時= 7200秒。

對於此計算欄型別，對應至擁有者第一個事件的資料列有`NULL`值。

**機械**

若要建立&#x200B;**事件編號**&#x200B;資料行：

1. 導覽至&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;頁面。

1. 導覽至您要建立此欄的表格。

1. 按一下右上角的&#x200B;**[!UICONTROL Create New Column]**。

1. 選取`Same Table`作為`Definition Type` （如果您要比較的資料行不在相同的資料表中，您可能需要重新設定它們的位置）。

1. 選取`SEQUENTIAL_COMPARISON`做為`Column Definition Equation`。

1. 選擇輸入，如上所述：
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. 您也可以新增篩選器，以排除不考慮的列。 排除的資料列有此資料行的`NULL`值。

1. 提供頁面頂端欄的名稱，然後按一下&#x200B;**[!UICONTROL Save]**。

1. 資料行可以立即使用&#x200B;**。

![秒](../../assets/SEC_new.png)
