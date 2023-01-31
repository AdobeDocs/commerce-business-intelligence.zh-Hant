---
title: 使用SQLReport Builder
description: 了解如何使用SQLReport Builder審核資料和度量，以便您可以將結果與本地資料庫的資料進行比較。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `SQL Report Builder`

此 `SQL Report Builder` 主要用於建立新報表和反覆分析，但也可用於有效稽核資料和量度。 以下資訊說明如何使用 `SQL Report Builder` 以便將結果與本地資料庫中的資料進行比較。

## 查詢量度

若要開始，請開啟 `SQL Report Builder` 瀏覽至 **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. 您可以使用SQL編輯器中的側欄，將游標移至量度上並按一下，將量度直接插入查詢中 **[!UICONTROL Insert]**. 這會將該量度的查詢定義新增至編輯器。 定義將包含下列元件：

- 此 **量度操作** 正在執行，由以下範例中的SUM()指示。
- 此 **表格** 由FROM子句指示的量度。
- 任何 **篩選器（和篩選器集）** 已新增至量度的值，如下列範例中的WHERE子句所指示。
- 元件 **timestamp** （年、月），以下範例中的ORDER BY子句指示。

如果您想要更清楚地查看查詢，可以重新格式化查詢欄位中查詢的顯示方式。 準備就緒時，請選取 `Run Query`. 結果會以表格形式填入查詢下方的報表面板。

![](../../assets/run-query-results.gif)

## 限制查詢

如果您嘗試找出特定的差異或一組資料，應將查詢限制在特定範例，以檢查您的本機資料庫。 您可以編輯查詢以符合所需的限制，以執行此操作。 在下列範例中，我們將查詢限制為僅包含2013年1月1日或之後的收入。 更新查詢後，請選取 **[!UICONTROL Run Query]** 再次更新結果。

![](../../assets/restricting-query.gif)

## 儲存和匯出

當報表符合您的需求時，請為報表指定不同的名稱，按一下「 」，將其儲存至控制面板 **[!UICONTROL Save]**，並選取您要儲存的報表類型和控制面板。 稽核量度時，建議將報表儲存為 `Table` 並儲存至測試控制面板。

儲存報表後，選取「 `Go to Dashboard`. 您可從該處尋找報表並選取「 」，以匯出資料 **[!UICONTROL Options gear > Full `.csv`匯出]** 或 **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## 自訂查詢

您也可以撰寫自訂查詢並匯出結果，以與本機資料庫進行比較。 遵循 [查詢優化指南](../../best-practices/optimizing-your-sql-queries.md)，在SQL編輯器中寫入查詢。 您可以使用側邊欄頂端的按鈕，在可供 `SQL Report Builder` 並將其添加到查詢中。 當您的自訂查詢符合您的需求時，您可以儲存報表，並從控制面板匯出該資料。

### 還難過？

如果您在稽核資料後發現不一致，請查看 [聯絡支援：資料差異](https://support.magento.com/hc/en-us/articles/360016505312) 支援文章，以取得後續操作的詳細資訊。
