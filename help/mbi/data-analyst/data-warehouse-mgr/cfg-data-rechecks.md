---
title: 配置資料檢查
description: 瞭解如何配置具有可更改值的資料列。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 配置資料檢查

在資料庫表中，可以有具有可更改值的資料列。 例如，在 `orders` 表中可能有一個名為 `status`。 在最初將訂單寫入資料庫時，狀態列可能包含該值 _掛起_。 訂單已複製到 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 這 `pending` 值。

訂單狀態可能會更改，儘管它們並不總是在 `pending` 狀態。 最終，它可能 `complete` 或 `cancelled`。 為確保Data Warehouse同步此更改，必須重新檢查列以獲取新值。

這與 [複製方法](../data-warehouse-mgr/cfg-replication-methods.md) 討論過嗎？ 重新檢查的處理因所選複製方法而異。 的 `Modified\_At` 複製方法是處理更改值的最佳選擇，因為無需配置重新檢查。 的 `Auto-Incrementing Primary Key` 和 `Primary Key Batch Monitoring` 方法需要重新檢查配置。

使用其中任何一種方法時，必須標籤可更改的列以進行重新檢查。 有三種方法可以做到這一點：

1. 作為要重新檢查的更新標誌列的一部分運行的審核進程。

   >[!NOTE]
   >
   >審計員依賴抽樣過程，所更改的列可能不會立即捕獲。

1. 您可以自行設定它們，方法是選中Data Warehouse管理器中列旁邊的複選框，然後按一下 **[!UICONTROL Set Recheck Frequency]**，並為應檢查更改的時間選擇適當的時間間隔。

1. 成員 [!DNL Adobe Commerce Intelligence] Data Warehouse團隊可以手動標籤要重新簽入的列，以便重新簽入Data Warehouse。 如果您知道可更改的列，請與團隊聯繫以請求設定重新檢查。 包括列清單以及頻率，並附帶您的請求。

## 重新檢查頻率 {#frequency}

**你知道嗎？**
設定重新檢查 `primary key` 列不檢查列中是否有更改的值。 該表將檢查已刪除的行，並從Data Warehouse中清除任何刪除。

當列被標籤為要重新檢查時，您還可以設定重新檢查的頻率。 如果特定列不經常更改，則選擇較不頻繁的重新檢查可以 [優化更新週期](../../best-practices/reduce-update-cycle-time.md)。

頻率選項包括：

* `always`  — 每次更新時都會重新檢查
* `daily`  — 對聲明的時區進行午夜後首次更新時重新檢查
* `weekly`  — 每週晚9點後對所聲明的時區進行重新檢查
* `monthly`  — 每四周對所聲明的時區進行一次週五9點後更新
* `once`  — 僅在下次更新（一次性刷新）中發生

由於更新時間與需要同步的資料量相關，Adobe建議選擇 `daily`。 `weekly`或 `monthly` 重新檢查而不是每次更新。

## 管理重新檢查頻率 {#manage}

通過按一下表名，然後檢查各個列，可以在Data Warehouse中管理重新檢查頻率。 同步狀態和重新檢查頻率( **變化？** 列)顯示表中每列。

要更改重新檢查頻率，請按一下要更改的列旁邊的複選框。 然後按一下 **[!UICONTROL Set Recheck Frequency]** 下拉並設定所需頻率。

![](../../assets/dwm-recheck.png)

你有時可能會看到 `Paused` 的 `Changes?` 的雙曲餘切值。 此值顯示在 [複製方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 設定為 `Paused`。

[!DNL Adobe] 建議複查這些列，以優化更新並確保重新檢查可更改的列。 如果列的重新檢查頻率很高，則Adobe建議減少該頻率以優化更新。

與我們聯繫，詢問有關當前複製方法或重新檢查的問題。

**相關：**

* [減少更新時間](../../best-practices/reduce-update-cycle-time.md)
* [優化資料庫以進行分析](../../best-practices/opt-db-analysis.md)
