---
title: 使用SQLReport Builder
description: 瞭解如何使用SQLReport Builder審核資料和度量，以便您可以將結果與本地資料庫中的資料進行比較。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

的 [!DNL SQL Report Builder] 主要用於構建新報告和迭代分析，但也可用於有效審核資料和度量。 以下資訊說明了如何使用 [!DNL SQL Report Builder] 以便將結果與本地資料庫中的資料進行比較。

## 查詢度量

要開始，請開啟 [!DNL SQL Report Builder] 通過導航 **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**。 可以使用 [!DNL SQL] 編輯器，通過懸停於度量並按一下 **[!UICONTROL Insert]**。 這會將該度量的查詢定義添加到編輯器中。 定義包括以下元件：

- 的 **度量操作** 正在執行，表示 `SUM()` 中。
- 的 **表** 度量是由 `FROM` 。
- 任意 **篩選器（和篩選器集）** 已添加到度量中，由 `WHERE` 的子句。
- 元件 **時間戳** （年、月），其上要排序的資料由 `ORDER BY` 的子句。

要更清楚地查看查詢，可以重新格式化查詢欄位中的顯示方式。 準備好後，選擇 `Run Query`。 結果以表格形式填充在查詢下方的報表面板中。

![](../../assets/run-query-results.gif)

## 限制查詢

如果您試圖查明特定差異或資料集，則應將查詢限制為特定示例，以檢查本地資料庫。 通過編輯查詢以符合所需限制，可以執行此操作。 在下例中，您將查詢限制為僅包括2013年1月1日或以後的收入。 更新查詢後，選擇 **[!UICONTROL Run Query]** 來更新結果。

![](../../assets/restricting-query.gif)

## 保存和導出

當報告滿足您的需要時，請為報告指定一個不同的名稱，按一下 **[!UICONTROL Save]**，然後選擇要保存的報告類型和儀表板。 審核度量時，Adobe建議將報告另存為 `Table` 並保存到test儀表板。

保存報表後，通過選擇 `Go to Dashboard`。 從中，可以通過查找報告並選擇 **[!UICONTROL Options gear > Full `.csv`導出]** 或 **[!UICONTROL Full Excel Export]**。

![](../../assets/export-dboard-data.gif)

## 自定義查詢

您還可以編寫自定義查詢並導出結果以與本地資料庫進行比較。 遵循 [查詢優化准則](../../best-practices/optimizing-your-sql-queries.md)，在SQL編輯器中寫入查詢。 您可以使用提要欄頂部的按鈕在表清單和可用於 [!DNL SQL Report Builder] 並添加到查詢中。 當自定義查詢符合您的需要時，您可以保存報告並從儀表板導出該資料。

>[!NOTE]
>
>如果在審核資料後發現差異，請查看 [聯繫支援：資料差異](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) 有關下一步操作的詳細資訊，請參閱支援主題。
