---
title: 匯出原始資料
description: 了解如何從 [!DNL MBI] Data Warehouse，進一步了解是什麼在推動您的控制面板。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 匯出原始資料

使用原始資料匯出功能，您可以從 [!DNL MBI] Data Warehouse，進一步了解是什麼在推動您的控制面板。 此外，原始資料匯出可協助您 [找出資料差異](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en).

原始資料匯出功能可存取其他欄和維度，這些是透過相關量度的去標準化和預先匯總所產生。 例如， `User's first order date` 是可針對 [!DNL MBI]，但資料庫中可能無法使用。

本教學課程涵蓋下列內容：

* [選擇要導出的資料](#select)
* [下載匯出(](#download)
* [存取歷史匯出](#historical)

## 步驟1:選擇要導出的資料 {#select}

有兩種方式可在 [!DNL MBI]:在圖表層級或表格層級。

### 在 `Manage Data` 標籤

如果要從中導出表 `Manage Data` 標籤，您需要 [管理](../administrator/user-management/user-management.md) 權限。

1. 按一下 **[!UICONTROL Manage Data** > **&#x200B;匯出資料&#x200B;**> **原始資料匯出]** 開始使用。
1. 您會看到 `Export List` （如果有的話）。 按一下 **[!UICONTROL Add Export]** 來建立匯出。
1. 此 `New Raw Data Export` 對話框。 您可以在此選取或取消選取欄和篩選器，以自訂匯出：

   * `Table` - `Table` 欄位會選取要匯出資料的表格。 依預設，這會顯示您導覽至的表格。
   * `Export Name`  — 在此欄位中，輸入匯出的名稱。 例如： `Philadelphia - Daily Revenue`.
   * `Available Columns`  — 此欄位列出資料庫中可用於匯出的欄（維度）。 若要新增欄，請按一下其名稱。
   * `Selected Columns`  — 此欄位列出匯出中目前包含的欄（維度）。 要刪除列，請按一下其名稱。
   * `Filter`  — 本節列出目前套用至匯出的篩選器。 這些篩選器可以變更；您也可以新增篩選器，以匯出特定資料集。
   * 完成後，按一下 **[!UICONTROL Export Data]**.

### 從控制面板在圖表層級匯出

1. 按一下任何圖表右上角的齒輪圖示。
1. 選擇 `Raw Export` 顯示 `Raw Export` 對話框。
1. 自訂匯出，方法是選擇 `table`, `columns`，和 `filters` 包含或排除。 如需本模組中欄位的詳細資訊，請參閱上一節。
   >[!NOTE]
   >
   >顯示於 `Table` 欄位預設為提供圖表的表格。

1. 完成後，按一下 **[!UICONTROL Export Data]**.

從圖表層級查看整個流程。

![](../assets/Chart-level_export.gif)

## 步驟2:下載匯出 {#download}

完成在 `Raw Data Export` 對話框。 由於某些匯出項目可能很大，因此限制為1,000萬列，而且可能需要一些時間才能執行。

要檢查導出是否就緒，請按一下 **[!UICONTROL Raw Data Exports]** 在畫面的右上角。 按一下 **[!UICONTROL Download]** 下載壓縮的 `.csv` 檔案。

![](../assets/Downloading_export.gif)

## 步驟3:存取歷史匯出 {#historical}

若要檢視過去的匯出項目，請按一下 **[!UICONTROL Raw Data Export]** 在畫面的右上角。 最多可存取7天的待定和已完成報表。

恭喜！ 你完成了。
