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

在資料庫表格中，可以有可變更值的資料欄。 例如，在`orders`資料表中可能會有名為`status`的資料行。 一開始將訂單寫入資料庫時，狀態資料行可能包含值&#x200B;_pending_。 已在您的[Data Warehouse](../data-warehouse-mgr/tour-dwm.md)中使用此`pending`值復寫訂單。

訂單狀態可以變更，但它們並不一定處於`pending`狀態。 最終可能會變成`complete`或`cancelled`。 為確保您的Data Warehouse同步此變更，必須重新檢查欄以取得新值。

這如何與討論的[復寫方法](../data-warehouse-mgr/cfg-replication-methods.md)相容？ 重新檢查的處理方式會因所選的複製方法而異。 `Modified\_At`復寫方法是處理變更值的最佳選擇，因為不需要設定重新檢查。 `Auto-Incrementing Primary Key`和`Primary Key Batch Monitoring`方法需要重新檢查組態。

使用其中一種方法時，必須標籤可變更的欄以重新檢查。 有三種方法可以達成此目的：

1. 作為要重新檢查的更新旗標欄的一部分執行的稽核程式。

   >[!NOTE]
   >
   >Auditor仰賴取樣程式，因此可能不會立即擷取變更的欄。

1. 您可以自行設定，方法是在Data Warehouse管理員中選取欄旁的核取方塊，按一下「**[!UICONTROL Set Recheck Frequency]**」，然後選取您應檢查變更的適當時間間隔。

1. [!DNL Adobe Commerce Intelligence] Data Warehouse團隊的成員可以在Data Warehouse中手動標示要重新檢查的欄。 如果您知道可變更欄，請聯絡團隊以請求設定重新檢查。 在您的要求中包含欄清單，以及頻率。

## 重新檢查頻率 {#frequency}

**您知道嗎？**
在`primary key`資料行上設定重新檢查並不會檢查資料行是否有變更值。 系統會檢查表格中是否有已刪除的列，且任何刪除都會從Data Warehouse中清除。

當欄被標籤為要重新檢查時，您也可以設定重新檢查發生的頻率。 如果特定資料行不經常變更，則選擇較不頻繁的重新檢查可以[最佳化您的更新週期](../../best-practices/reduce-update-cycle-time.md)。

頻率選項包括：

* `always` — 在每次更新期間進行重新檢查
* `daily` — 重新檢查會在您宣告的時區的第一次午夜後更新時進行
* `weekly` — 對於您宣告的時區，每週會在下午9點後重新檢查一次
* `monthly` — 對於您宣告的時區，每四周於星期五晚上9點後進行重新檢查
* `once` — 只在下次更新中發生（一次性的重新整理）

由於更新時間與需要同步多少資料相關，Adobe建議選擇`daily`、`weekly`或`monthly`重新檢查，而不是每次更新。

## 管理重新檢查頻率 {#manage}

按一下表格名稱，然後檢查個別欄，即可在Data Warehouse中管理重新檢查頻率。 同步處理狀態與重新檢查頻率(**變更嗎？**&#x200B;欄)會針對表格中的每個欄顯示。

若要變更重新檢查頻率，請按一下您要變更之欄旁的核取方塊。 然後按一下&#x200B;**[!UICONTROL Set Recheck Frequency]**&#x200B;下拉式清單，並設定所要的頻率。

![](../../assets/dwm-recheck.png)

您有時可能會在`Paused`欄中看到`Changes?`。 當表格的[復寫方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md)設定為`Paused`時，會顯示這個值。

[!DNL Adobe]建議檢閱這些欄，以最佳化您的更新並確保重新檢查可變更的欄。 如果根據資料變更的頻率，欄的重新檢查頻率很高，Adobe建議將其降低，以最佳化您的更新。

如有疑問，請聯絡我們，或查詢目前的復寫方法或重新檢查。

**相關：**

* [縮短更新時間](../../best-practices/reduce-update-cycle-time.md)
* [最佳化資料庫以進行分析](../../best-practices/opt-db-analysis.md)
