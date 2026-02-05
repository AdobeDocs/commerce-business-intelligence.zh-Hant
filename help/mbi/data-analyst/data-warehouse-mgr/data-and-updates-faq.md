---
title: 資料和更新資訊
description: 瞭解如何檢查更新週期的狀態。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: db93e5284950fa9336d0833af24589754c94a8b3
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# 資料和更新資訊

* [我的資料為何變更？](#datachange)
* [定期和強制更新之間有何差異？](#regularforcedupdates)
* [更新週期為何要花很長的時間？](#updatecycletime)
* [更新週期完成時是否可以通知我？](#notifyupdate)
* [為什麼 [!DNL Google ECommerce] 資料與我的資料庫不同？](#ecommdatabase)
* [如何疑難排解資料差異？](#datadiscrepancy)

## 我的資料為何變更？ {#datachange}

圖表值可能會因新資料同步至您的Data Warehouse而在一天中發生變更。 此外，由於[重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md)，現有資料欄的值可能會變更。 重新檢查是尋找資料欄中變更值的程式，例如從`open`移至`shipped`的訂單狀態。

根據使用者的許可權設定，有幾種不同的方式[可檢查更新週期](../../best-practices/check-update-cycle.md)的狀態：

* **[!UICONTROL Read-Only]和[!UICONTROL Standard]使用者** — 您可以將滑鼠移至頁面右上角的圖示上，檢視上次提取資料點的時間。
* **[!UICONTROL Admin]使用者** — 可以檢視最後一個資料點和帳戶整合狀態圖示。 如需詳細資訊，請瀏覽至&#x200B;**[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**，以檢視目前的更新狀態和上次完成更新的時間。
* **API方法** — 可以使用更新週期狀態API擷取最近完成的更新週期。

如需檢查更新週期狀態的完整詳細資訊，請參閱[檢查更新週期狀態](../../best-practices/check-update-cycle.md)。

## 定期和強制更新之間有何差異？ {#regularforcedupdates}

定期更新是&#x200B;**已排程**&#x200B;程式，而強制更新是由您啟動的&#x200B;**手動程式**。 如果您有中斷時數（或[!DNL Commerce Intelligence]不應更新資料的時間段），強制更新會啟動一個不遵守中斷期間限制的週期。

## 更新週期為何要花很長的時間？ {#updatecycletime}

許多因素都會增加原本就漫長的更新時間。 某些[復寫方法](../data-warehouse-mgr/cfg-replication-methods.md)、[較高的重新檢查頻率](../data-warehouse-mgr/cfg-data-rechecks.md)以及儀表板和圖表的數量只是少數貢獻者。 Adobe建議[重新設定部分設定](../../best-practices/reduce-update-cycle-time.md)和[最佳化資料庫以利分析](../../best-practices/opt-db-analysis.md)，以減少更新時間。

## 更新週期完成時是否可以通知我？ {#notifyupdate}

如果更新進行中，**[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**&#x200B;頁面上有一個連結，您可以在週期完成時用來要求電子郵件通知。 如果更新不在進行中，您會看到強制更新開始的連結。

## 為什麼[!DNL Google ECommerce]資料與我的資料庫不同？ {#ecommdatabase}

[!DNL Google Analytics]和您的資料庫之間的差異可能因各種原因而產生。 追蹤功能未正確啟用、使用者造訪無痕內容，以及點選事件無法正常運作只是幾個例子。 如果您的收入和訂單看起來不正確，[請參閱此主題](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=zh-Hant)以診斷問題。

## 如何疑難排解資料差異？ {#datadiscrepancy}

Adobe知道看到不一致的資料可能會讓人感到挫折。 嘗試使用[資料差異檢查清單](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=zh-Hant)或[資料匯出教學課程](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=zh-Hant)來診斷問題。 如果您仍然被截斷，[請連絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)。
