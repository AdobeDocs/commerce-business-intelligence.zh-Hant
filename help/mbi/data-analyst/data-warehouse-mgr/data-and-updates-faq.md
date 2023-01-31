---
title: 資料和更新資訊
description: 了解如何檢查更新週期的狀態。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# 資料和更新資訊

* [為什麼我的資料會變更？](#datachange)
* [定期更新和強制更新之間有何差異？](#regularforcedupdates)
* [更新週期為何需要很長時間？](#updatecycletime)
* [更新週期完成時，是否可收到通知？](#notifyupdate)
* [為什麼 [!DNL Google ECommerce] 資料與我的資料庫不同？](#ecommdatabase)
* [如何疑難排解資料不一致？](#datadiscrepancy)

## 為什麼我的資料會變更？ {#datachange}

由於同步至資料倉庫的新資料，圖表值可能會在一整天內變更。 此外，現有資料欄的值可能會因 [重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md). 重新檢查是在資料欄中尋找已變更值的程式，例如從 `open` to `shipped`.

有幾種不同的方法 [檢查更新週期的狀態](../../best-practices/check-update-cycle.md)，視您擁有的使用者權限類型而定。

## 定期更新和強制更新之間有何差異？ {#regularforcedupdates}

定期更新為 **排程** 強制更新時的處理 **您啟動的手動流程**. 如果您有封鎖時間，或者 [!DNL MBI] 不應更新資料 — 強制更新將啟動一個不遵守封鎖期限限制的週期。

## 更新週期為何需要很長時間？ {#updatecycletime}

許多因素可能會增加本已耗時的更新時間。 特定 [複製方法](../data-warehouse-mgr/cfg-replication-methods.md), [更高的重檢頻率](../data-warehouse-mgr/cfg-data-rechecks.md)，而控制面板和圖表的數量只是少數貢獻者。 建議 [重新配置某些設定](../../best-practices/reduce-update-cycle-time.md) 和 [優化資料庫以進行分析](../../best-practices/opt-db-analysis.md) 以縮短更新時間。

## 更新週期完成時，是否可收到通知？ {#notifyupdate}

當然！ 如果目前正在進行更新，則上會有 `Connections` 頁面，您可以在週期完成後用來要求電子郵件通知。

## 為什麼[!DNL Google ECommerce]資料與我的資料庫不同？ {#ecommdatabase}

之間的差異 [!DNL Google Analytics] 而您的資料庫可能因多種原因出現。 追蹤未正確啟用、使用者無痕造訪，以及點按事件未正確運作，只是幾個範例。 如果您的收入和訂單看起來不太正確， [使用本文](https://support.magento.com/hc/en-us/articles/360016505232) 診斷問題。

## 如何疑難排解資料不一致？ {#datadiscrepancy}

我們知道看到不一致的資料可能是令人沮喪的體驗。 嘗試使用 [資料差異檢查清單](https://support.magento.com/hc/en-us/articles/360016731271) 或 [資料匯出教學課程](https://support.magento.com/hc/en-us/articles/360016730631) 診斷問題。 如果你還被難住， [聯絡支援](../../guide-overview.md).
