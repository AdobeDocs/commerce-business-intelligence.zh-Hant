---
title: 連線Adobe Analytics
description: 瞭解如何將 [!DNL Adobe Analytics] 的端對端客戶歷程重點與您從 [!DNL Commerce Intelligence]所仰賴的電子商務重點結合在一起。
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KkiKySM2q8ewqhQ1kdUjLuTM4iOpzrZb5Ok-UvBBpJE
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
source-wordcount: 312
ht-degree: 0%

---

# 連線[!DNL Adobe Analytics]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![Adobe Analytics標誌](../../../assets/adobe-analytic-slogo.png)

[!DNL Adobe Analytics]的[!DNL Adobe Commerce Intelligence]整合可讓您將[!DNL Adobe Analytics]的端對端客戶歷程重點與您從[!DNL Commerce Intelligence]所仰賴的電子商務重點結合在一起。 這可讓您全面瞭解商店的整體效能。

更具體來說，[!DNL Adobe Analytics]的[!DNL Commerce Intelligence]整合提供商戶開始合併其[!DNL Adobe Commerce]和[!DNL Adobe Analytics]資料集的功能。

- 從您現有的[!DNL Adobe Analytics]帳戶建立與[!DNL Commerce Intelligence]的連線。

- 從單一報表套裝中選取最多25個量度和維度，以複製至您的Data Warehouse。

- 使用所有標準[!DNL Commerce Intelligence]功能來轉換、加入及報告復寫的[!DNL Adobe Analytics]資料。

## 連線先決條件

連線需要下列資訊：

- [!DNL Adobe Analytics]登入認證

- 要復寫資料的`Name`和/或`ID` （共[!DNL Adobe Analytics]個報告套裝）

- 要復寫至[!DNL Commerce Intelligence]的量度和維度清單

## 正在連線[!DNL Adobe Analytics]的[!DNL Commerce Intelligence]整合

1. 移至`Integrations`下的&#x200B;**[!DNL Manage Data** > **Integrations]**&#x200B;頁面。

1. 按一下&#x200B;**[!UICONTROL Add an Integration]**。

1. 按一下「**[!UICONTROL Adobe Analytics]**」圖示可存取允許您授權您的[!DNL Adobe Analytics]帳戶連線的頁面。

1. 按一下&#x200B;**[!UICONTROL Authorize with Adobe Analytics]**。

1. 輸入您的[!DNL Adobe Analytics]認證。 成功授權後，您會被重新導向回[!DNL Commerce Intelligence]。

1. 接著會顯示可用報表套裝的清單。 選取您要匯入資料的報表套裝，然後按一下&#x200B;**[!UICONTROL Continue]**。

1. 度量和維度選擇畫面隨即顯示。 請選取至少一個量度和至少一個維度，最多合共25個量度和維度。 依名稱搜尋或捲動以尋找您的元件，然後按一下核取方塊以選取。 按一下&#x200B;**[!UICONTROL Continue]**。

1. 選取的報表套裝會顯示在表格中。 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以確認您的選擇。

1. 通知[!DNL Commerce Intelligence] [支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)您的整合已獲得授權，他們將為您執行初始連線程式。

初始連線程式執行後，您的表格將可在Data Warehouse頁面的`All Tables`標籤下使用。 選取您要復寫的欄，資料將在下次完整更新後顯示。
