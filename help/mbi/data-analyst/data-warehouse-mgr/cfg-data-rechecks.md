---
title: 設定資料檢查
description: 了解如何使用可變的值來設定資料欄。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# 設定資料檢查

在資料庫表中，可以有可更改值的資料列。 例如，在 `orders`)表格中可能有 `status`. 最初將訂單寫入資料庫時，狀態列可能包含值 _擱置_. 順序會複製到 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 這個 `pending` 值。

不過，訂單狀態可能會變更 — 它們不一定會在 `pending` 狀態。 最終，它可能變成 `complete` 或 `cancelled`. 為確保您的Data Warehouse同步此變更，必須重新檢查欄以取得新值。

這與 [複製方法](../data-warehouse-mgr/cfg-replication-methods.md) 討論過嗎？ 重新檢查的處理會因所選復寫方法而異。 此 `Modified\_At` 復寫方法是處理變更值的最佳選擇，因為不需要設定重新檢查。 此 `Auto-Incrementing Primary Key` 和 `Primary Key Batch Monitoring` 方法需要重新檢查配置。

使用其中一種方法時，必須標籤可變更的欄以進行重新檢查。 有三種方法可執行此作業：

* 作為要重新檢查的更新標誌列的一部分運行的審核進程。

   >[!NOTE]
   >
   >Auditor仰賴取樣程式，且不會立即擷取變更的欄。

* 您可以選取「Data Warehouse管理員」中欄旁的核取方塊，按一下「 **[!UICONTROL Set Recheck Frequency]**，並選擇適當的時間間隔，以檢查變更的時間。
* 成員 [!DNL MBI] Data Warehouse團隊可以手動標籤要在Data Warehouse中重新勾選的欄。 如果您知道可變的欄，請聯絡團隊以請求設定重新檢查。 請在請求中加入欄清單及頻率。

## 重新檢查頻率 {#frequency}

**你知道嗎？**
在 `primary key` 欄不會檢查欄中是否有變更的值。 系統會檢查表中是否有已刪除的行，並從Data Warehouse中清除所有刪除。

將欄標籤為要重新檢查時，您也可以設定重新檢查的發生頻率。 如果特定列不經常更改，則選擇較不頻繁的重新檢查可以 [優化更新週期](../../best-practices/reduce-update-cycle-time.md).

頻率選項包括：

* `always`  — 每次更新時都會重新檢查
* `daily`  — 在午夜後第一次為您宣告的時區更新時重新檢查
* `weekly`  — 每週晚9點後，您宣告的時區都會重新檢查
* `monthly`  — 針對您宣告的時區，每四周在星期五晚9點後重新檢查一次
* `once`  — 僅在下次更新中發生（一次性重新整理）

由於更新時間與需要同步的資料量相關，因此Adobe建議您選擇 `daily`, `weekly`，或 `monthly` 重新檢查，而非每次更新。

## 管理重新檢查頻率 {#manage}

通過按一下表名，然後檢查單個列，可以在Data Warehouse中管理重新檢查頻率。 同步狀態和重新檢查頻率( **變更？** 欄)顯示。

若要變更重新核取頻率，請按一下您要變更之欄旁的核取方塊。 然後按一下 **[!UICONTROL Set Recheck Frequency]** 下拉式清單，然後設定所需的頻率。

![](../../assets/dwm-recheck.png)

你有時可能會看到 `Paused` 在 `Changes?` 欄。 此值會在表格的 [複製方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 設為 `Paused`.

Adobe建議您檢閱這些欄，以最佳化更新並確保正在重新勾選可變更的欄。 如果欄的重新檢查頻率很高，且資料變更的頻率很高，Adobe建議您降低頻率，以最佳化更新。

如有疑問，請聯絡我們以查詢目前的復寫方法或重新檢查。

**相關：**

* [縮短更新時間](../../best-practices/reduce-update-cycle-time.md)
* [優化資料庫以進行分析](../../best-practices/opt-db-analysis.md)
