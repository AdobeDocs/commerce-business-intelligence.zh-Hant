---
title: 格式化和導入財務資料
description: 了解如何格式化和匯入財務資料。
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 格式和導入財務資料

本主題探討匯入財務資料以進行分析的最佳方式，位於 [!DNL MBI].

二維、跨索引標籤資料表通常是用於財務資料的格式。 由於欄和列中都有按標籤分類的值，這種類型的版面可能很容易用人的眼睛和電子錶格工具來查看，但對資料庫來說不太友好。

![](../../mbi/assets/crosstab.png)

若要在 [!DNL MBI]，表格必須平面化為一維清單。 平面化時，每個資料值會依多個標籤分類，這些標籤全部在單一列中，其中每一列都是唯一的，或會有唯一識別碼，例如主索引鍵欄。

![](../../mbi/assets/flattened.png)

## 格式化要導入的Excel檔案

要使用Excel透視表平面化二維表：

1. 開啟包含二維資料表的檔案。
1. 開啟資料透視表嚮導。 在Windows中，快捷方式是 `Alt-D`. 在Mac OSX中，輸入 `Command-Option-P`.
1. 選擇 **[!UICONTROL Multiple consolidated ranges]** 按一下 **[!UICONTROL Next]**.
1. 選擇 **[!UICONTROL I will create the page fields]** 按一下 **[!UICONTROL Next]**.
1. 選取二維表格中的整個資料集，包括標籤。 確保 `0` 已針對所需頁面欄位數選取，然後按一下 **[!UICONTROL Next]**.
1. 在新工作表中建立透視表，然後按一下 **[!UICONTROL Finish]**.
1. 從欄位清單中取消選取欄位和列欄位。
1. 按兩下生成的數值，在新頁面中顯示平面化源資料。
   ![](../../mbi/assets/pivot-table-double-click.png)
1. 另存為 `CSV` 檔案。

就這樣！ 資料表已轉換為清單格式，保留了其所有原始資訊，現在可以 [匯入 [!DNL MBI]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) 供分析之用。
