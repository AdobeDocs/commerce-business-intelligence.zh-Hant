---
title: 預期 [!DNL Adobe Analytics] 資料
description: 瞭解連線RDS執行個體的步驟。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 預期[!DNL Adobe Analytics]資料

[!DNL Adobe Analytics]的[!DNL Adobe Commerce Intelligence]整合使用[Analytics 2.0報告API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md)。

>[!INFO]
>
>為確保您取得預期的資料，您可以先在[!DNL Adobe Analytics] Workspace中使用您想要的量度和維度建立報表。 這可讓您檢查資料的相容性和可用性。

在您的Data Warehouse中為每個連線的報表套裝建立一個名為`report-suite-<ID>`的資料表（其中`<ID>`是由[!DNL Commerce Intelligence]產生的唯一ID）。

此表格的結構描述是由您在整合設定程式中選取的量度和維度所組成。 [!DNL Commerce Intelligence]也會產生數個額外的資料行，以供識別。

例如，如果您在設定期間選取下列量度和維度：
- `Metric`： `Page views`
- `Dimension`： `Page`

此表格將包含下列欄：

| 欄名稱 | 說明 |
| --- | --- |
| `_id` | 此欄是主索引鍵。 |
| `_item_hash` | [!DNL Commerce Intelligence]唯一識別碼。 此資料行由[!DNL Commerce Intelligence]建立。 |
| `_updated_at` | 此欄包含上次更新資料列的時間。 由[!DNL Commerce Intelligence]建立。 |
| `start_date` | 資料列所含資料的開始日期。 `start_date`一律為一列中的同日00:00。 |
| `end_date` | 列所包含資料的結束日期。 `end_date`在一列中永遠是同一天23:59。 |
| `page_views` | 選取的量度：所識別時段內的頁面檢視總數。 |
| `page` | 選取的維度：具有追蹤檢視的個別頁面名稱。 |

使用[!DNL Commerce Intelligence]頁面中的&#x200B;*sync*&#x200B;或&#x200B;*unsync*&#x200B;選項，控制`Data Warehouse`表格中哪些選取的量度和維度有可用資料。 目前未同步的欄會以灰色顯示。 如果您停止同步欄，可以稍後再次開始同步。

## 目前限制

本節概述[!DNL Adobe Analytics]之[!DNL Commerce Intelligence]整合的限制。

| 限制 | 說明 |
| --- | --- |
| `Historical data period` | 如同其他協力廠商整合，[!DNL Adobe Analytics]整合會提取有限的歷史資料量，然後繼續更新資料。 歷史期間設定為2週。 |
| `Empty component combinations` | 有些量度和維度組合沒有包含資料。 如果選取這種組合進行復寫，[!DNL Commerce Intelligence]會從復寫資料表中排除資料行。 若要避免選取這類組合，您可以先在[[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=zh-Hant)中建立報告，以確認您取得預期的資料。 |
| `Re-authorization cadence` | 每兩週需要重新授權[!DNL Adobe Analytics]整合。 若要重新授權，請移至整合的[編輯]頁面，然後按一下&#x200B;**[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**。 |
| `One dimension per row` | [!DNL Adobe Analytics]一次提供一個維度的量度資料。 如果您在設定期間選取多個維度，則[!DNL Commerce Intelligence]表格中的每一列會包含單一維度值，且其他維度的每一列為Null。 |
