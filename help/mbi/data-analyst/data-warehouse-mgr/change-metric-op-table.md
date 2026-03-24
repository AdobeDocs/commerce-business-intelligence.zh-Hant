---
title: 變更量度的作業表格
description: 瞭解如何變更量度用來執行其操作的資料表。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 0%

---

# 變更量度的作業表格

在某些情況下，您可以決定變更量度用來執行操作的資料表格。 例如，如果您有新的使用者表格，您想要從`Users\_Old`表格移轉與使用者相關的量度，以改用`Users\_New`表格。

1. 前往&#x200B;**[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. 按一下您要切換&#x200B;**[!UICONTROL Edit]**&#x200B;資料表的量度旁的`operational`。
1. 在編輯器中，按一下&#x200B;**[!UICONTROL Change]**。

   ![顯示作業資料表設定的量度定義頁面](../../assets/change-metrics-1.png)
1. 選取您要以此量度為基礎的新表格。
1. 比對現有資料維度與新表格中對應的資料維度。 例如，如果您有一個名為`User's registration date`的資料行，只要選取新資料表中記錄相同日期資料的資料行即可。 （如果新表格中沒有相符的欄，請參閱下一步）

   ![顯示可用資料表的資料表選取下拉式清單](../../assets/change-metrics-2.png)

1. 如果您在新資料表中沒有相符的資料行，您可以&#x200B;**在資料表中建立它**，或者[聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant) （如果它是由[!DNL Commerce Intelligence]建立的計算資料行或維度）。 您也可以&#x200B;**從量度**&#x200B;中刪除維度。 若要刪除您不再需要的維度，只要返回量度的編輯器，並在「`Dimensions`」下選取要刪除的維度即可。

   ![操作資料行選取下拉式功能表](../../assets/change-metrics-3.png)
