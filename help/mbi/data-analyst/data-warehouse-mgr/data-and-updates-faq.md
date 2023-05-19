---
title: 資料和更新資訊
description: 瞭解如何檢查更新週期的狀態。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 資料和更新資訊

* [為什麼我的資料會改變？](#datachange)
* [常規更新和強制更新之間有何區別？](#regularforcedupdates)
* [為什麼更新週期需要很長時間？](#updatecycletime)
* [更新週期完成後，是否可以通知我？](#notifyupdate)
* [為什麼 [!DNL Google ECommerce] 資料與我的資料庫不同嗎？](#ecommdatabase)
* [如何排除資料差異？](#datadiscrepancy)

## 為什麼我的資料會改變？ {#datachange}

由於新資料正同步到您的Data Warehouse，圖表值可以全天更改。 此外，現有資料列的值可能因 [重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md)。 重新檢查是查找資料列中更改的值（如從中移動的訂單狀態）的過程 `open` 至 `shipped`。

有幾種不同的方法 [檢查更新週期的狀態](../../best-practices/check-update-cycle.md)，具體取決於用戶的權限設定。

## 常規更新和強制更新之間有何區別？ {#regularforcedupdates}

定期更新 **計畫** 強制更新時的進程 **您啟動的手動流程**。 如果您有封鎖時間(或一個 [!DNL Commerce Intelligence] 不應更新資料)，強制更新將啟動一個不遵守封鎖期限限制的週期。

## 為什麼更新週期需要很長時間？ {#updatecycletime}

許多因素可能會增加本已很長的更新時間。 確定 [複製方法](../data-warehouse-mgr/cfg-replication-methods.md)。 [較高的重檢頻率](../data-warehouse-mgr/cfg-data-rechecks.md)，而儀表板和圖表的數量只是少數貢獻者。 Adobe建議 [重新配置某些設定](../../best-practices/reduce-update-cycle-time.md) 和 [優化資料庫以進行分析](../../best-practices/opt-db-analysis.md) 縮短更新時間。

## 更新週期完成後，是否可以通知我？ {#notifyupdate}

如果正在進行更新，則 `Connections` 頁面，您可以在週期完成後使用該頁面請求電子郵件通知。

## 為什麼[!DNL Google ECommerce]資料與我的資料庫不同嗎？ {#ecommdatabase}

之間的差異 [!DNL Google Analytics] 而您的資料庫可能因各種原因而出現。 未正確啟用跟蹤、訪問Incognito的用戶以及按一下事件無法正常工作只是幾個示例。 如果你的收入和訂單看起來不對， [查看主題](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 診斷問題。

## 如何排除資料差異？ {#datadiscrepancy}

Adobe知道，看到不一致的資料可能是令人沮喪的經歷。 嘗試使用 [資料差異核對表](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) 或 [資料導出教程](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) 診斷問題。 如果你還是被難倒了， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
