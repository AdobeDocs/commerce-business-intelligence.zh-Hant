---
title: 連線Adobe Analytics
description: 瞭解如何將 [!DNL Adobe Analytics] 的端對端客戶歷程重點與您從 [!DNL Commerce Intelligence]所仰賴的電子商務重點結合在一起。
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 連線[!DNL Adobe Analytics]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![](../../../assets/adobe-analytic-slogo.png)

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
