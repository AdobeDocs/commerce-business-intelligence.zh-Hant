---
title: 連接Adobe Analytics
description: 學習將客戶的端到端行程重點集中到 [!DNL Adobe Analytics] 而你依賴的電子商務 [!DNL Commerce Intelligence]。
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 連接 [!DNL Adobe Analytics]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/adobe-analytic-slogo.png)

的 [!DNL Adobe Analytics] 整合 [!DNL Adobe Commerce Intelligence] 使您能夠將客戶的端到端行程重點 [!DNL Adobe Analytics] 而你依賴的電子商務 [!DNL Commerce Intelligence]。 這為您提供了您商店整體效能的完整圖片。

更具體地說， [!DNL Adobe Analytics] 整合 [!DNL Commerce Intelligence] 為商戶提供開始組合其功能 [!DNL Adobe Commerce] 和 [!DNL Adobe Analytics] 資料集。

- 從現有連接建立連接 [!DNL Adobe Analytics] 帳戶 [!DNL Commerce Intelligence]。

- 從一個報告套件中選擇最多25個度量和維度以複製到您的Data Warehouse中。

- 使用所有標準 [!DNL Commerce Intelligence] 轉換、連接和報告複製的功能 [!DNL Adobe Analytics] 資料。

## 連接先決條件

連接需要以下資訊：

- [!DNL Adobe Analytics] 登錄憑據

- `Name` 和/或 `ID` 共 [!DNL Adobe Analytics] 報表套件複製資料

- 要複製到的度量和維清單 [!DNL Commerce Intelligence]

## 連接 [!DNL Adobe Analytics] 整合 [!DNL Commerce Intelligence]

1. 轉到 `Integrations` 頁 **[!DNL Manage Data** > **Integrations]**。

1. 按一下 **[!UICONTROL Add an Integration]**。

1. 按一下 **[!UICONTROL Adobe Analytics]** 表徵圖以訪問允許您授權的頁面 [!DNL Adobe Analytics] 帳戶連接。

1. 按一下 **[!UICONTROL Authorize with Adobe Analytics]**。

1. 輸入 [!DNL Adobe Analytics] 憑據。 成功授權後，您將重定向回 [!DNL Commerce Intelligence]。

1. 將顯示可用報告套件的清單。 選擇要從中導入資料的報表套件，然後按一下 **[!UICONTROL Continue]**。

1. 將顯示度量和維度選擇螢幕。 至少選擇一個度量和至少一個維，最多合計25個度量和維。 按名稱搜索或滾動以查找元件，然後按一下複選框進行選擇。 按一下 **[!UICONTROL Continue]**。

1. 選定的報告套件顯示在表中。 按一下 **[!UICONTROL Save]** 確認您的選擇。

1. 通知 [!DNL Commerce Intelligence] [支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 您的整合已獲得授權，並且它們會為您運行初始連接過程。

初始連接進程運行後，您的表將在Data Warehouse頁中的 `All Tables` 頁籤。 選擇要複製的列，資料將在下次完全更新後顯示。
