---
title: 縮短更新週期時間
description: 瞭解如何縮短更新週期。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 減少更新週期處理時間

[!DNL Adobe Commerce Intelligence] 在一天中與資料庫同步以複製新資料，確保儀表板始終顯示最新資訊。

許多因素可能會增加已經很長的更新時間。 某些複製方法、更高的重新檢查頻率以及儀表板和圖表的數量只是少數貢獻者。 本主題討論一些減少更新時間的最佳做法。

## 減少重新檢查頻率

在資料庫表中，可以有具有可更改值的資料列。 例如，在 **訂單** 表中可能有一個名為 **狀態**。 在最初將訂單寫入資料庫時，狀態列可能包含該值 `pending`。 訂單已複製到 [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) 這 `pending` 值。

可更改的列必須是 [重新檢查更新的值](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 時間過長。 預設情況下， [!DNL Commerce Intelligence] 在每次更新期間都會重新檢查這些列，但是，如果有大量資料要重新檢查和複製，則可能會對更新時間產生負面影響。 Adobe建議將重新檢查頻率設定為每日、每週或每月，而不是在每次更新期間運行重新檢查。

## 使用增量複製方法

如上所述，長時間的更新時間直接與需要重新檢查和複製的資料量相關。 [增量複製方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) 可以大大減少更新週期中處理的資料量。 如果可能，Adobe建議使用這些方法或修改資料庫以支援增量方法。

## 從儀表板中刪除未使用的圖表

在更新週期結束時， [!DNL Commerce Intelligence] 對所有圖表執行快取操作。 快取儲存資料，以便以後可以更快地完成對資訊的請求。 在 [!DNL Commerce Intelligence]，這意味著儀表板可以快速載入，因為圖表在每次載入資料時不需要查詢資料。

自 [!DNL Commerce Intelligence] 只對儀表板中找到的圖表執行快取操作，從儀表板中刪除未使用的圖表會縮短更新時間。 請記住，同一圖表可能位於多個儀表板上 — 請與您的團隊聯繫，確保它們還刪除了任何未使用的圖表。

>[!NOTE]
>
>從儀表板中刪除圖表不會刪除圖表。 你可以 [隨時添加](../data-user/dashboards/add-charts-dashboard.md)。

## 優化資料庫以進行分析

除了重新評估重新檢查頻率、複製方法和圖表用途外，還可以 [優化資料庫以進行分析](../best-practices/opt-db-analysis.md)。

## 包裝

如果您的更新時間即使在實施這些建議後仍然緩慢， [與支援團隊聯繫](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
