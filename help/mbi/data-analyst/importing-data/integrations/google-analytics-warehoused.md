---
title: 連接倉庫Google Analytics
description: 瞭解訪問者如何使用您的網站、哪些內容有吸引力、訪問者離開的地方等。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 連接 [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是網際網路上使用最廣泛的Web分析服務。 實施 [!DNL Google Analytics] 在您的網站上，您可以跟蹤訪問者如何使用您的網站、哪些內容很吸引人、訪問者離開的地方等。 [!DNL Google Analytics Warehoused] 是與現有的 [!DNL Google Analytics] 整合。 它允許更好的分析，因為 [!DNL Google Analytics] Data Warehouse中的資料，這與現有源的即時源不同 [!DNL Google Analytics] 整合。 在 [!DNL Commerce Intelligence]除了其他資料外，還可改善您站點的整體健康和可用性。

## GA倉庫與即時整合的區別

主要區別在於儲存了一個整合([!DNL Google Analytics Warehoused])，另一個不是([!DNL Google Analytics Live])。 在 [!DNL Google Analytics Warehoused]，這允許操縱 [!DNL Google Analytics] 資料，讓你能夠 [!DNL Google Analytics] 以及其他資料來源，以建立有洞察力的報告。

看 [!DNL Google Analytics] 以操縱為例，說明可以做什麼。 假設您在第四季度有多個不同名稱的廣告活動。 這些活動是特定營銷計畫的結果。 使用倉庫資料，您可以建立一個列，該列查找有關的市場活動名稱並返回第四季度方案名稱 `Operation Dumbo`。

組合方面允許 [!DNL Google Analytics] 要與其他資料聯接以便進行分析的資料。 例如， `Total Time On Site By Ad Campaign` 資料 [!DNL Google Analytics] 加入它 `Total Spent Per Campaign` 資料 [!DNL Facebook Ads] 全面瞭解你投入的成本。

使用 [!DNL Google Analytics Live] 另一方面， [!DNL Google Analytics] 圖表就像一個小思洛儲存器，它不儲存在您的Data Warehouse中。

## 連接 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] 是 `Premium` 整合。 [聯繫支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果您有興趣將此整合添加到您的訂閱中。

1. 轉到 `Connections` 頁 **[!UICONTROL Admin** > **Integrations]**。
1. 按一下 **[!UICONTROL Add an Integration]**，位於右側。
1. 按一下 [!DNL Google Analytics Warehoused] 表徵圖 開啟 [!DNL Google Analytics] 「憑據」頁。
1. 輸入 [!DNL Google Analytics] 憑據。 在完成授權過程後，您將被重定向回 [!DNL Commerce Intelligence]。
1. 顯示配置檔案ID的清單。 檢查要連接到的配置檔案 [!DNL Commerce Intelligence]。 如果您有多個配置式，並且需要一些幫助來確定哪個是，請參閱「連接多個」 [!DNL Google Analytics] 配置檔案部分。

## 連接多個 [!DNL Google Analytics] 配置檔案

您可能有多個網站連接到一個 [!DNL Google Analytics] 帳戶，由自己確定 [!DNL Google Analytics] 配置檔案ID。 在這種情況下，您可以選擇將所有配置檔案ID包含在 [!DNL Commerce Intelligence]。 檢查要在配置檔案選擇步驟中包括的配置檔案ID。

確定特定網站的 [!DNL Google Analytics] 配置檔案ID:

1. 登錄 [!DNL Google Analytics]
1. 轉到特定網站 [!DNL Google Analytics] 儀表板
1. 查看URL — 配置檔案ID對應於以下八個數字 `p` 在行的末尾

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 斷開 [!DNL Google Analytics Warehoused] 從 [!DNL Commerce Intelligence] {#disconnect}

1. 訪問 [!DNL Google Analytics] [帳戶設定](https://myaccount.google.com/intro) 的子菜單。
1. 在 `Security` ，然後按一下 **[!UICONTROL edit]** 下 `Authorizing` 應用程式和站點。
1. 按一下 **[!UICONTROL revoke access]** 下 [!DNL Commerce Intelligence]。

## 相關文檔

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [連接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析網站活動和客戶轉換率](../../analysis/web-act-cust-conversion.md)
* [使用跟蹤用戶獲取資料 [!DNL Google Analytics] 餅](../../analysis/google-track-user-acq.md)
