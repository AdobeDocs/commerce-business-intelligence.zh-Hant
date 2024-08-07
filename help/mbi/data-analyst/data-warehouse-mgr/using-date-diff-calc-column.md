---
title: 使用日期差異計算欄
description: 瞭解日期差異計算欄的用途和用途。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 日期差異計算欄

此主題概述&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;頁面中可用`Date Difference`計算欄的用途和用途。 以下是其功能的說明，隨後是一個範例，以及建立它的機制。

**說明**

`Date Difference`欄型別會根據事件時間戳記，計算屬於單一記錄的兩個事件之間的時間。 此欄中計算的原始值以秒為單位，但會自動轉換為分鐘、小時、天等等，以便顯示在報表上。 但是，當您作為篩選/群組使用時，您想要以秒為單位使用值。

`date difference`計算欄可用來建立量度，以計算兩個事件之間的平均或中間時間，例如客戶註冊與其第一筆訂單之間的平均時間。

**範例**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


在上述範例中，`Date Difference`欄是`Seconds between timestamp_2 and timestamp_1`欄。 它執行計算`timestamp_2 minus timestamp_1`。

**機械**

下列步驟說明如何建立`Date Difference`欄。

1. 導覽至&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;頁面。
1. 導覽至您要建立此欄的表格。
1. 按一下&#x200B;**[!UICONTROL Create a Column]**&#x200B;並依照以下方式設定您的欄：
   * 選取`Column Definition Type` > `Same Table`
   * 選取`Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * 選取`Ending DATETIME`欄>選擇結束日期時間欄位，這通常是稍後發生的事件
   * 選取`Starting DATETIME`欄** >選擇開始日期時間欄位，這通常是較早發生的事件

1. 提供資料行的名稱，然後按一下&#x200B;**[!UICONTROL Save]**。
1. 資料行可以立即使用&#x200B;**。

例如，下列範例設定為計算`Seconds between order date and customer's creation date`：

![](../../assets/date_diff.png)
