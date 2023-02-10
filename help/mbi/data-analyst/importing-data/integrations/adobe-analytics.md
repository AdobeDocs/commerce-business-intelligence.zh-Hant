---
title: Connect Adobe Analytics
description: 了解如何將 [!DNL Adobe Analytics] 以及您所依賴的電子商務 [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

此 [!DNL Adobe Analytics] 整合 [!DNL MBI] 讓您將端對端客戶歷程的重點整合在 [!DNL Adobe Analytics] 以及您所依賴的電子商務 [!DNL MBI]，以更完整地了解您商店的整體效能。

更具體而言， [!DNL Adobe Analytics] 整合 [!DNL MBI] 為商戶提供開始結合其「商務」和「分析」資料集的功能。
- 從您現有的 [!DNL Adobe Analytics] 帳戶 [!DNL MBI].
- 從一個報表套裝中選取最多25個量度和維度，以複製至您的 [!DNL MBI] 資料倉庫。
- 使用所有標準 [!DNL MBI] 轉換、連接和報告已複製內容的功能 [!DNL Adobe Analytics] 資料。

## 連線必要條件

連線需要下列資訊：
- [!DNL Adobe Analytics] 登入憑證
- `Name` 和/或 `ID` of [!DNL Adobe Analytics] 報表套裝，以從
- 要複製到的量度和維度清單 [!DNL MBI]

## 連接 [!DNL Adobe Analytics] MBI整合

1. 前往 `Integrations` 頁面底下 **[!DNL Manage Data** > **Integrations]**.
1. 按一下 **[!UICONTROL Add an Integration]**，位於畫面的右側。
1. 按一下 **[!UICONTROL Adobe Analytics]** 圖示來存取可讓您授權您 [!DNL Adobe Analytics] 帳戶連線。
1. 按一下 **[!UICONTROL Authorize with Adobe Analytics]**.
1. 輸入 [!DNL Adobe Analytics] 憑證。 成功授權後，系統會將您重新導向回 [!DNL MBI].
1. 可用的報表套裝清單隨即顯示。 選取您要匯入資料的報表套裝，然後按一下 **[!UICONTROL Continue]**.
1. 量度和維度選取畫面隨即顯示。 選取至少一個量度和至少一個維度，最多總共25個量度和維度。 依名稱搜尋或捲動以尋找您的元件，然後按一下要選取的核取方塊。 按一下 **[!UICONTROL Continue]**.
1. 選取的報表套裝會顯示在表格中。 按一下 **[!UICONTROL Save]** 以確認您的選取。
1. 通知 [!DNL MBI] 支援團隊授權您的整合，他們會為您執行初始連線程式。

初始連線程式執行後，您的表格將可在「Data Warehouse」頁面中的 `All Tables` 標籤。 選取您要復寫的欄，下次完整更新後就會顯示資料。
