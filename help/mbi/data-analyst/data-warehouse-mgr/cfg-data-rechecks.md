---
title: 設定資料檢查
description: 瞭解如何使用可變更的值來設定資料欄。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 設定資料檢查

在資料庫表格中，可以有可變更值的資料欄。 例如，在 `orders` 表格中可能有一欄稱為 `status`. 最初將訂單寫入資料庫時，狀態列可能包含值 _擱置中_. 此順序會複製到您的 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 與此 `pending` 值。

訂單狀態可以變更，但它們並不一定都在 `pending` 狀態。 最終，它可能會變成 `complete` 或 `cancelled`. 為確保您的Data Warehouse同步此變更，必須重新檢查欄以取得新值。

這與 [復寫方法](../data-warehouse-mgr/cfg-replication-methods.md) 已經討論過了？ 重新檢查的處理方式會因所選的複製方法而異。 此 `Modified\_At` 復寫方法是處理變更值的最佳選擇，因為不需要設定重新檢查。 此 `Auto-Incrementing Primary Key` 和 `Primary Key Batch Monitoring` 方法需要重新檢查設定。

使用其中一種方法時，必須標籤可變更的欄以重新檢查。 有三種方法可以達成此目的：

1. 作為要重新檢查的更新旗標欄的一部分執行的稽核程式。

   >[!NOTE]
   >
   >Auditor仰賴取樣程式，因此可能不會立即擷取變更的欄。

1. 您可以自行設定，方法是在Data Warehouse管理員中選取欄旁的核取方塊，然後按一下 **[!UICONTROL Set Recheck Frequency]**，並選擇適當的時間間隔，以檢查變更。

1. 成員 [!DNL Adobe Commerce Intelligence] Data Warehouse團隊可以手動標籤欄，以便在您的Data Warehouse中重新檢查。 如果您知道可變更欄，請聯絡團隊以請求設定重新檢查。 在您的要求中包含欄清單，以及頻率。

## 重新檢查頻率 {#frequency}

**您知道嗎？**
在上設定重新檢查 `primary key` 欄不會檢查欄中是否有變更的值。 系統會檢查表格中是否有已刪除的列，且會從Data Warehouse中清除任何刪除。

當欄被標籤為要重新檢查時，您也可以設定重新檢查發生的頻率。 如果特定欄不經常變更，則選擇不太頻繁的重新檢查可以 [最佳化您的更新週期](../../best-practices/reduce-update-cycle-time.md).

頻率選項包括：

* `always`  — 在每次更新期間進行重新檢查
* `daily`  — 對於您宣告的時區，會在午夜後第一次更新時重新檢查
* `weekly`  — 對於您宣告的時區，每週於下午9點後進行星期五更新，以重新檢查
* `monthly`  — 對於您宣告的時區，每四周在星期五晚上9點後進行重新檢查
* `once`  — 只會在下次更新時發生（一次性的重新整理）

由於更新時間與需要同步多少資料相關，Adobe建議選擇 `daily`， `weekly`，或 `monthly` 重新檢查而不是每次更新。

## 管理重新檢查頻率 {#manage}

按一下表格名稱，然後檢查個別欄，即可在Data Warehouse中管理重新檢查頻率。 同步狀態與重新檢查頻率( **變更？** 欄)。

若要變更重新檢查頻率，請按一下您要變更之欄旁的核取方塊。 然後按一下 **[!UICONTROL Set Recheck Frequency]** 下拉式清單，並設定所需的頻率。

![](../../assets/dwm-recheck.png)

您有時可能會看到 `Paused` 在 `Changes?` 欄。 當表格的 [複製方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 設為 `Paused`.

[!DNL Adobe] 建議您檢閱這些欄，以最佳化更新並確保重新檢查可變更的欄。 如果根據資料變更的頻率，欄的重新檢查頻率很高，Adobe建議將其降低，以最佳化更新。

如有疑問，請聯絡我們，或查詢目前的復寫方法或重新檢查。

**相關：**

* [縮短更新時間](../../best-practices/reduce-update-cycle-time.md)
* [最佳化資料庫以進行分析](../../best-practices/opt-db-analysis.md)
