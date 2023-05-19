---
title: 導出原始資料
description: 學習從 [!DNL Commerce Intelligence] Data Warehouse更仔細地查看儀表板的電源。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 導出原始資料

使用原始資料導出，您可以從Data Warehouse導出記錄，以更仔細地瞭解是什麼驅動了儀表板。 此外，原始資料導出可幫助您 [精確資料差異](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html)。

原始資料導出提供對通過相關度量的去標準化和預聚合生成的附加列和維的訪問。 比如說， `User's first order date` 是可為中的每個用戶導出的維 [!DNL Commerce Intelligence]，但可能在資料庫中不可用。

本教程將介紹以下內容：

* [選擇要導出的資料](#select)
* [下載導出(](#download)
* [訪問歷史導出](#historical)

## 步驟1:選擇要導出的資料 {#select}

有兩種方法可以在 [!DNL Commerce Intelligence]:

1. 在圖表級別
1. 在表級

### 在中的表級導出 [!UICONTROL Manage Data] 頁籤

如果要從中導出表 [!UICONTROL Manage Data] 頁籤 [管理](../administrator/user-management/user-management.md) 權限。

1. 按一下 **[!UICONTROL Manage Data** > **&#x200B;導出資料&#x200B;**> **原始資料導出]**。
1. 您看到 `Export List` 導出的資料。 按一下 **[!UICONTROL Add Export]** 的子菜單。
1. 的 `New Raw Data Export` 對話框。 在此，可以通過選擇或取消選擇列和篩選器來自定義導出：

   * `Table` - `Table` 欄位選擇從中導出資料的表。 預設情況下，將顯示您導航到的表。
   * `Export Name`  — 在此欄位中，輸入導出的名稱。 例如： `Philadelphia - Daily Revenue`。
   * `Available Columns`  — 此欄位列出資料庫中可用於導出的列（維）。 要添加列，請按一下其名稱。
   * `Selected Columns`  — 此欄位列出當前包含在導出中的列（維）。 要刪除列，請按一下其名稱。
   * `Filter`  — 本節列出當前應用於導出的篩選器。 這些過濾器可以更改；還可以添加新篩選器以導出特定資料集。
   * 完成後，按一下 **[!UICONTROL Export Data]**。

### 從儀表板在圖表級別導出

1. 按一下任意圖表右上角的齒輪表徵圖。

1. 選擇 `Raw Export` 從下拉清單中顯示 `Raw Export` 對話框。

1. 通過選擇 `table`。 `columns`, `filters` 包含或排除。 有關本模組中各欄位的詳細資訊，請參閱上一節。

   >[!NOTE]
   >
   >顯示在 `Table` 預設情況下，欄位是圖表的電源表。

1. 完成後，按一下 **[!UICONTROL Export Data]**。

在圖表級別查看整個流程。

![](../assets/Chart-level_export.gif)

## 步驟2:下載導出 {#download}

導出將在完成您在 `Raw Data Export` 對話框。 由於某些出口可能大，因此限制在1000萬行，可能需要一些時間才能運行。

要檢查導出是否就緒，請按一下 **[!UICONTROL Raw Data Exports]** 在螢幕右上角。 按一下 **[!UICONTROL Download]** 下載拉鍊 `.csv` 導出檔案。

![](../assets/Downloading_export.gif)

## 第3步：訪問歷史導出 {#historical}

要查看過去的導出，請按一下 **[!UICONTROL Raw Data Export]** 在螢幕右上角。 最多可訪問7天的待處理和已完成的報告。
