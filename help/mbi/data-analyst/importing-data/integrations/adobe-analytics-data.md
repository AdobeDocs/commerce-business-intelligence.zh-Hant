---
title: 預期 [!DNL Adobe Analytics] 資料
description: 瞭解連接RDS實例的步驟。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 預期 [!DNL Adobe Analytics] 資料

的 [!DNL Adobe Analytics] 整合 [!DNL Adobe Commerce Intelligence] 使用 [分析2.0報告API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md)。

>[!INFO]
>
>為確保獲得您期望的資料，您可以先在 [!DNL Adobe Analytics] 具有所需度量和尺寸的工作區。 這允許您檢查資料的相容性和可用性。

每個連接的報告套件都調用一個表 `report-suite-<ID>` ( `<ID>` 是由 [!DNL Commerce Intelligence])。

此表的架構由您在整合設定過程中選擇的度量和維組成。 還由 [!DNL Commerce Intelligence]，用於標識目的。

例如，如果在設定期間選擇了以下度量和維：
- `Metric`: `Page views`
- `Dimension`: `Page`

該表將包含以下列：

| 列名 | 說明 |
| --- | --- |
| `_id` | 此列是主鍵。 |
| `_item_hash` | [!DNL Commerce Intelligence] 唯一標識符。 此列由 [!DNL Commerce Intelligence]。 |
| `_updated_at` | 此列包含上次更新資料行的時間。 建立者 [!DNL Commerce Intelligence]。 |
| `start_date` | 行的包含資料的開始日期。 `start_date` 是同一天的00:00。 |
| `end_date` | 行的包含資料的結束日期。 `end_date` 是同一天的23:59。 |
| `page_views` | 所選度量：標識的時段的頁面視圖總數。 |
| `page` | 所選維：具有跟蹤視圖的單個頁名。 |

控制所選度量和維中哪些資料可用 [!DNL Commerce Intelligence] 表 *同步* 或 *未同步* 的 `Data Warehouse` 的子菜單。 當前未同步的列以灰色顯示。 如果停止同步列，可以稍後再開始同步它。

## 當前限制

本節概述了 [!DNL Adobe Analytics] 整合 [!DNL Commerce Intelligence]。

| 限制 | 說明 |
| --- | --- |
| `Historical data period` | 與其他第三方整合一樣， [!DNL Adobe Analytics] 整合可獲取有限的歷史資料，然後繼續更新資料。 歷史時段配置為2週。 |
| `Empty component combinations` | 度量和維的某些組合不包含任何資料。 如果選擇了這種組合進行複製， [!DNL Commerce Intelligence] 從複製的表中排除該列。 為避免選擇此組合，可先在 [[!DNL Adobe Analytics] 工作區](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) 來驗證您是否獲得了預期的資料。 |
| `Re-authorization cadence` | 重新授權 [!DNL Adobe Analytics] 每兩週需要一次整合。 要重新授權，請轉至整合的「編輯」頁，然後按一下 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**。 |
| `One dimension per row` | [!DNL Adobe Analytics] 一次提供一個維的度量資料。 如果在設定期間選擇多個維，則 [!DNL Commerce Intelligence] 表包含每個其他維的單個維值和空值。 |
