---
title: 預期 [!DNL Adobe Analytics] 資料
description: 了解連接RDS實例的步驟。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# 預期 [!DNL Adobe Analytics] 資料

此 [!DNL Adobe Analytics] 整合 [!DNL MBI] 使用 [Analytics 2.0報表API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>若要確保您取得預期的資料，您可以先在 [!DNL Adobe Analytics] 工作區及您所需的量度和維度。 這可讓您檢查資料的相容性和可用性。

每個已連線報表套裝一個表格(稱為 `report-suite-<ID>`，其中 `<ID>` 是 [!DNL MBI]  — 會在您的Data Warehouse中建立。

此表的架構由您在整合設定程式中選取的度量和維度組成。 也會產生數個其他欄 [!DNL MBI]，以供識別之用。

例如，如果您在設定期間選取了下列量度和維度：
- `Metric`: `Page views`
- `Dimension`: `Page`

表格會包含下列欄：

| 欄名稱 | 說明 |
| --- | --- |
| `_id` | 此欄是主要索引鍵。 |
| `_item_hash` | [!DNL MBI] 唯一識別碼。 此列由建立 [!DNL MBI]. |
| `_updated_at` | 此欄包含上次更新資料列的時間。 建立者 [!DNL MBI]. |
| `start_date` | 列包含資料的開始日期。 `start_date` 一列內一律為當天00:00。 |
| `end_date` | 列包含資料的結束日期。 `end_date` 一列內一律為當天23:59。 |
| `page_views` | 所選量度：已識別時段的頁面檢視總數。 |
| `page` | 所選維：具有追蹤檢視的個別頁面名稱。 |

控制哪些選取的量度和維度在您的 [!DNL MBI] 表格，使用 *同步* 或 *取消同步* 選項 `Data Warehouse` 頁面。 目前未同步的欄會以灰色顯示。 如果您停止同步欄，可以稍後再開始同步。

## 目前限制

本節概述 [!DNL Adobe Analytics] 整合 [!DNL MBI].

| 限制 | 說明 |
| --- | --- |
| `Historical data period` | 如同其他協力廠商整合， [!DNL Adobe Analytics] 整合會提取有限的歷史資料，然後繼續保持資料更新。 歷史期間設為2週。 |
| `Empty component combinations` | 某些量度和維度的組合不含任何資料。 如果為複製選擇了這種組合， [!DNL MBI] 從複製表中排除該列。 若要避免選取此類組合，您可以先在 [[!DNL Adobe Analytics] 工作區](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) 來驗證您獲得的資料。 |
| `Re-authorization cadence` | 重新授權 [!DNL Adobe Analytics] 每兩週需要整合一次。 若要重新授權，請前往整合的編輯頁面，然後按一下 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] 一次提供一個維度的量度資料。 如果您在設定期間選取多個維度， [!DNL MBI] 表包含每個其他維的單個維值和空值。 |
