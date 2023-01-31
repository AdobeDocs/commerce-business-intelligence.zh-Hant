---
title: 連接Google Analytics倉庫
description: 了解如何追蹤訪客使用您網站的方式、哪些內容吸引人、哪些是訪客的退出位置等。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---

# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是網際網路上最廣泛使用的網頁分析服務。 實作 [!DNL Google Analytics] 可讓您追蹤訪客使用您網站的方式、哪些內容吸引人、哪些是訪客的退出位置等。 [!DNL Google Analytics Warehoused] 是與現有 [!DNL Google Analytics] 整合。 因為有 [!DNL Google Analytics] Data Warehouse中的資料，此變數與現有即時摘要的不同 [!DNL Google Analytics] 整合。 在 [!DNL MBI]與其他資料片段一起，可改善網站的整體健康狀況和可用性。

## GA Warehoused和Live Integration之間的差異

主要優點在於儲存了一個整合([!DNL Google Analytics Warehoused])，而另一個不是([!DNL Google Analytics Live])。 若 [!DNL Google Analytics Warehoused]，這可讓您 [!DNL Google Analytics] 資料，讓您能夠 [!DNL Google Analytics] 及其他資料來源，以建立有洞察力的報表。

讓我們看看 [!DNL Google Analytics] 廣告促銷活動，以說明從操作觀點可以執行的作業。 假設第4季有多個不同名稱的廣告促銷活動。 行銷活動是特定行銷計畫的結果。 有了倉庫資料，我們可以建立新的欄，找出相關的促銷活動名稱並傳回的第4季計畫名稱 `Operation Dumbo`.

組合方面允許 [!DNL Google Analytics] 要連結到其他資料以進行分析的資料。 例如，取 `Total Time On Site By Ad Campaign` 資料來源 [!DNL Google Analytics] 加入 `Total Spent Per Campaign` 資料來源 [!DNL Facebook Ads] 來全面了解您的投入成本。

使用 [!DNL Google Analytics Live] 另一方面， [!DNL Google Analytics] 圖表就像沒有儲存在您的 [!DNL MBI] 資料倉庫。

## 連接 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] 是 `Premium` 整合。 [聯絡支援](../../../guide-overview.md) 如果您有興趣將此整合新增至您的訂閱。

1. 前往 `Connections` 頁面底下 **[!UICONTROL Admin** > **Integrations]**.
1. 按一下 **[!UICONTROL Add a Add Integration]**，位於畫面的右側。
1. 按一下 [!DNL Google Analytics Warehoused] 表徵圖。 這會開啟 [!DNL Google Analytics] 憑據頁。
1. 輸入 [!DNL Google Analytics] 憑證。 授權程式完成後，系統會將您重新導向回 [!DNL MBI].
1. 將會顯示設定檔ID清單。 檢查您要連線的設定檔 [!DNL MBI]. 如果您有多個配置檔案，並且需要一些幫助來識別哪些是，請參閱連接多個配置檔案 [!DNL Google Analytics] 設定檔一節。

## 連接多個 [!DNL Google Analytics] 設定檔

您可能有多個網站連結至單一 [!DNL Google Analytics] 帳戶，以其自己的 [!DNL Google Analytics] 設定檔ID。 在此情況下，您可以選擇將所有設定檔ID納入 [!DNL MBI]. 只要檢查您要在設定檔選取步驟期間包含的設定檔ID即可。

識別特定網站的 [!DNL Google Analytics] 配置檔案ID:

1. 登入 [!DNL Google Analytics]
1. 前往特定網站的 [!DNL Google Analytics] 儀表板
1. 查看URL — 設定檔ID對應至下列8個數字 `p` 在行的結尾

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 斷開連接 [!DNL Google Analytics Warehoused] 從 [!DNL MBI] {#disconnect}

1. 造訪您的 [!DNL Google Analytics] [帳戶設定](https://www.google.com/accounts/) 頁面。
1. 在 `Security` ，然後按一下 **[!UICONTROL edit]** 下一頁 `Authorizing` 應用程式和網站。
1. 按一下 **[!UICONTROL revoke access]** 下一頁 [!DNL MBI].

## 相關檔案

* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
* [連接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析網站活動和客戶轉換率](../../analysis/web-act-cust-conversion.md)
* [使用追蹤使用者贏取資料 [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
* [使用追蹤使用者裝置和瀏覽器資料 [!DNL Google Analytics] cookie](https://support.magento.com/hc/en-us/articles/360016732911)
