---
title: 資料和更新資訊
description: 了解如何檢查更新週期的狀態。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '417'
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

圖表值可能會隨著新資料同步至您的Data Warehouse而變更。 此外，現有資料欄的值可能會因 [重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md). 重新檢查是在資料欄中尋找已變更值的程式，例如從 `open` to `shipped`.

有幾種不同的方法 [檢查更新週期的狀態](../../best-practices/check-update-cycle.md)，視您擁有的使用者權限類型而定。

## 定期更新和強制更新之間有何差異？ {#regularforcedupdates}

定期更新為 **排程** 強制更新時的處理 **您啟動的手動流程**. 如果您有封鎖時間，或者 [!DNL MBI] 不應更新資料 — 強制更新會啟動一個不遵守封鎖期限限制的週期。

## 更新週期為何需要很長時間？ {#updatecycletime}

許多因素可能會增加本已耗時的更新時間。 特定 [複製方法](../data-warehouse-mgr/cfg-replication-methods.md), [更高的重檢頻率](../data-warehouse-mgr/cfg-data-rechecks.md)，而控制面板和圖表的數量只是少數貢獻者。 Adobe建議 [重新配置某些設定](../../best-practices/reduce-update-cycle-time.md) 和 [優化資料庫以進行分析](../../best-practices/opt-db-analysis.md) 以縮短更新時間。

## 更新週期完成時，是否可收到通知？ {#notifyupdate}

如果正在進行更新，則上會有連結 `Connections` 頁面，您可以在週期完成後用來要求電子郵件通知。

## 為什麼[!DNL Google ECommerce]資料與我的資料庫不同？ {#ecommdatabase}

之間的差異 [!DNL Google Analytics] 而您的資料庫可能因各種原因而出現。 追蹤未正確啟用、使用者無痕造訪，以及點按事件未正確運作，只是幾個範例。 如果您的收入和訂單看起來不正確， [使用本文](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) 診斷問題。

## 如何疑難排解資料不一致？ {#datadiscrepancy}

Adobe知道看到不一致的資料可能是令人沮喪的體驗。 請嘗試使用 [資料差異檢查清單](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=en) 或 [資料匯出教學課程](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en) 診斷問題。 如果你還被難住， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
