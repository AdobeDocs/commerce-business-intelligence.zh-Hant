---
title: 使用SQL Report Builder
description: 瞭解如何使用SQL Report Builder稽核資料和測量結果，以便將結果與本機資料庫的資料進行比較。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

[!DNL SQL Report Builder]主要用於建立新報告並反複分析，但也可以用來有效稽核資料和量度。 下列資訊說明如何使用[!DNL SQL Report Builder]稽核資料與度量，以便您可以將結果與本機資料庫的資料進行比較。

## 查詢量度

若要開始，請瀏覽至[!DNL SQL Report Builder]以開啟&#x200B;**[!UICONTROL Report Builder > SQL Report Builder > Create Report]**。 您可以使用[!DNL SQL]編輯器中的側邊欄，將滑鼠游標移至量度上並按一下&#x200B;**[!UICONTROL Insert]**，直接將量度插入查詢。 這會將該量度的查詢定義新增到編輯器中。 定義包括下列元件：

- 正在執行&#x200B;**量度作業**，以下範例中的`SUM()`表示。
- 在&#x200B;**上建立量度的**&#x200B;資料表，由`FROM`子句表示。
- 已新增至量度的任何&#x200B;**篩選器（和篩選器集）**，由以下範例中的`WHERE`子句表示。
- 要排序資料之&#x200B;**timestamp** （年、月）的元件，由下列範例中的`ORDER BY`子句表示。

若要更清楚的檢視查詢，您可以重新格式化查詢欄位中的顯示方式。 準備就緒後，選取`Run Query`。 結果會在查詢下方的報表面板中填入為表格。

![](../../assets/run-query-results.gif)

## 限制查詢

如果您嘗試查明特定差異或資料集，您應該將查詢限製為特定範例，以對照您的本機資料庫進行檢查。 您可以編輯查詢以符合所需的限制來完成此操作。 在下列範例中，您將查詢限製為僅包含自2013年1月1日或之後開始的收入。 更新查詢之後，再次選取&#x200B;**[!UICONTROL Run Query]**&#x200B;以更新結果。

![](../../assets/restricting-query.gif)

## 儲存和匯出

當報告符合您的需求時，請為報告指定不同的名稱，按一下「**[!UICONTROL Save]**」，然後選取您要儲存的報告型別和儀表板。 在稽核量度時，Adobe建議將報表儲存為`Table`並儲存至測試儀表板。

在儲存報告後，選取`Go to Dashboard`以導覽至該儀表板。 從那裡，您可以尋找報告並選取&#x200B;**[!UICONTROL Options gear > Full `.csv`匯出]**&#x200B;或&#x200B;**[!UICONTROL Full Excel Export]**&#x200B;以匯出資料。

![](../../assets/export-dboard-data.gif)

## 自訂查詢

您也可以撰寫自訂查詢並匯出結果，以便與本機資料庫進行比較。 依照查詢最佳化[的](../../best-practices/optimizing-your-sql-queries.md)准則，在SQL編輯器中寫入查詢。 您可以使用側邊欄頂端的按鈕，在[!DNL SQL Report Builder]中可用的表格和量度清單之間切換，並將它們新增至您的查詢。 當自訂查詢符合您的需求時，您可以儲存報告並從儀表板匯出該資料。

>[!NOTE]
>
>如果您在稽核資料後發現不一致，請參閱[連絡支援：資料差異](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html)支援主題，以取得後續操作的詳細資訊。
