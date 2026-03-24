---
title: 縮短更新週期時間
description: 瞭解如何縮短更新週期時間。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/DFlzL9E95teiWI31j7qWRU8Ab6GkbFX7iPPdaxGq48A
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 0%

---

# 縮短更新週期處理時間

[!DNL Adobe Commerce Intelligence]會一整天與您的資料庫同步以複製新資料，確保您的儀表板一律顯示最新資訊。

許多因素都會增加原本就漫長的更新時間。 某些複製方法、較高的重新檢查頻率以及儀表板和圖表的數量只是少數貢獻因素。 本主題討論減少更新時間的一些最佳實務。

## 降低重新檢查的頻率

在資料庫表格中，可以有可變更值的資料欄。 例如，在&#x200B;**訂單**&#x200B;資料表中可能有名為&#x200B;**狀態**&#x200B;的資料行。 一開始將訂單寫入資料庫時，狀態列可能包含值`pending`。 已在您的[Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md)中使用此`pending`值復寫訂單。

可變更的資料行必須在一段時間內重新檢查[更新的值](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md)。 依預設，[!DNL Commerce Intelligence]會在每次更新期間重新檢查這些欄，但如果要重新檢查並復寫大量資料，可能會對更新時間造成負面影響。 Adobe建議將重新檢查頻率設定為每日、每週或每月，而不是在每次更新時執行重新檢查。

## 使用增量複製方法

如上所述，長的更新時間與必須重新檢查及復寫多少資料直接相關。 [增量複製方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md)可以大幅減少更新週期期間處理的資料量。 Adobe建議儘可能使用這些方法，或修改資料庫以支援增量方法。

## 從儀表板移除未使用的圖表

在更新週期結束時，[!DNL Commerce Intelligence]會對所有圖表執行快取作業。 快取會儲存資料，以便未來能更快速地完成資訊請求。 在[!DNL Commerce Intelligence]中，這表示儀表板載入迅速，因為圖表不需要在每次載入時查詢資料。

由於[!DNL Commerce Intelligence]只對儀表板中找到的圖表執行快取操作，因此從儀表板中移除未使用的圖表會減少更新時間。 請記住，同一圖表可能位於多個儀表板上 — 請洽詢您的團隊，確保他們也會移除任何未使用的圖表。

>[!NOTE]
>
>從您的儀表板移除圖表並不會刪除圖表。 您可以[隨時將其重新加入](../data-user/dashboards/add-charts-dashboard.md)。

## 最佳化資料庫以進行分析

除了重新評估重新檢查頻率、複製方法和圖表有用性之外，您還可以[最佳化資料庫以進行分析](../best-practices/opt-db-analysis.md)。

## 正在結束

如果即使實作這些建議，您的更新時間仍顯緩慢，[請連絡支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
