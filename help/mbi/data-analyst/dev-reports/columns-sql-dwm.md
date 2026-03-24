---
title: SQL與Data Warehouse Manager之間的差異
description: 瞭解SQL和Data Warehouse Manager之間的差異。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
TQID: https://experienceleague.adobe.com/aWLLAi9e-A6Di7AGujRNd79W7GqSRo5yIgmQRZAHOEQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 0%

---

# [!DNL SQL]與[!DNL Data Warehouse Manager]之間的差異

在[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)中建立的資料行與使用[[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md)建立的資料行之間有兩項主要差異。 一個是與更新週期的相依性，另一個是欄如何儲存在您的帳戶中。

## [!DNL SQL Report Builder]中的資料行

欄不依賴更新週期，因此您不必再等待一個欄完成即可對欄進行反複運算。 如果發生錯誤，只需要按幾下按鍵即可進行修正，不必再等待兩次更新完成後才能重新開始工作。

>[!IMPORTANT]
>
>您使用[!DNL SQL]編輯器建立的欄未儲存至您的Data Warehouse。 您一律可以存取包含欄的查詢，但如果您想要在多個報表中使用欄，則必須在每個報表的查詢中重新建立該欄。 這表示使用[!DNL SQL]編輯器建立的資料行無法用於傳統[!DNL Report Builder]。

## Data Warehouse Manager中的欄

欄取決於更新週期，因此必須先完成一個完整的週期，然後才能對其進行編輯。 這些資料行會儲存至Data Warehouse Manager，並可用於傳統[!DNL Report Builder]或[!DNL SQL Report Builder]。
