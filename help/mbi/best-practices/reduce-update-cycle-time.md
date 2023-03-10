---
title: 縮短更新週期時間
description: 了解如何縮短更新週期時間。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# 縮短更新週期處理時間

[!DNL MBI] 會一整天與資料庫同步，以複製新資料，確保控制面板一律顯示最新資訊。

許多因素可能會導致更新時間過長。 某些復寫方法、較高的重新檢查頻率，以及控制面板和圖表的數量，只是少數貢獻者。 本主題探討一些最佳實務，以縮短更新時間。

## 降低重新檢查頻率

在資料庫表中，可以有可更改值的資料列。 例如，在 **訂購** 表中可能有一列稱為 **狀態**. 最初將訂單寫入資料庫時，狀態列可能包含值 `pending`. 順序會複製到 [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) 這個 `pending` 值。

可更改的列必須是 [重新檢查更新的值](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 隨著時間推移。 依預設， [!DNL MBI] 在每次更新時都會重新檢查這些欄，但如果有大量資料要重新檢查和複製，可能會對您的更新時間造成負面影響。 Adobe建議將重新檢查頻率設為每日、每週或每月，而非在每次更新期間執行重新檢查。

## 使用增量複製方法

如上所述，長時間的更新時間會直接與必須重新檢查和複製的資料數量相關。 [增量複製方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) 可大幅減少更新週期中處理的資料量。 如果可能，Adobe建議使用這些方法或修改資料庫以支援增量方法。

## 從控制面板中移除未使用的圖表

在更新週期結束時， [!DNL MBI] 對所有圖表執行快取操作。 快取會儲存資料，以便更快完成未來的資訊要求。 在 [!DNL MBI]，這表示控制面板會快速載入，因為圖表不需要在每次載入時查詢資料。

自 [!DNL MBI] 僅對控制面板中找到的圖表執行快取操作，從控制面板中移除未使用的圖表會減少更新時間。 請記住，同一個圖表可能位於多個控制面板上 — 請洽詢您的團隊，確定它們也移除了任何未使用的圖表。

>[!NOTE]
>
>從控制面板移除圖表並不會刪除圖表。 您可以 [隨時重新添加](../data-user/dashboards/add-charts-dashboard.md).

## 優化資料庫以進行分析

除了重新評估重新檢查頻率、複製方法和圖表的實用性之外，您還可以 [優化資料庫以進行分析](../best-practices/opt-db-analysis.md).

## 包裝

如果即使在實作這些建議後，更新時間仍緩慢， [聯絡支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
