---
title: 使用日期差異計算欄
description: 瞭解日期差異計算欄的用途和用途。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/5SElfBoU6vqCNthFdj96eCNH26dC54ucjqknnhQXQy8
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 272
ht-degree: 0%

---

# 日期差異計算欄

此主題概述`Date Difference`頁面中可用&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;計算欄的用途和用途。 以下是其功能的說明，隨後是一個範例，以及建立它的機制。

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

![日期差異計算組態顯示日期時間資料行選取專案](../../assets/date_diff.png)
