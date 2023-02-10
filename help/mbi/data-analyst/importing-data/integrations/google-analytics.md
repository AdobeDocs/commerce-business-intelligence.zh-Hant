---
title: 連接Google Analytics
description: 了解如何連結Google Analytics [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Connect [!DNL Google Analytics]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是網際網路上最廣泛使用的網頁分析服務。 實作 [!DNL Google Analytics] 可讓您追蹤訪客使用您網站的方式、哪些內容吸引人、哪些是訪客的退出位置等。 在 [!DNL MBI]與其他資料片段一起，可改善網站的整體健康狀況和可用性。

讓我們從進入 [!DNL Google Analytics] 憑證 [!DNL MBI]:

1. 前往 **[!UICONTROL Manage Data** > **Integrations]** 頁面。
1. 按一下 **[!UICONTROL Add Integration]**，位於畫面的右側。
1. 按一下 [!DNL Google Analytics] 表徵圖。 這會開啟 [!DNL Google Analytics] 憑據頁。
1. 輸入 [!DNL Google Analytics] 憑證。 授權程式完成後，系統會將您重新導向回 [!DNL MBI].
1. 將會顯示設定檔ID清單。 檢查您要連線的設定檔 [!DNL MBI]. 如果您有多個配置檔案，並且需要一些幫助來識別哪些是，請參閱連接多個配置檔案 [!DNL Google Analytics] 設定檔一節。

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 變更會自動儲存，因此按一下 **返回連接** 等你完成。

## 連接多個 [!DNL Google Analytics] 設定檔

您可能有多個網站連結至單一 [!DNL Google Analytics] 帳戶，以其自己的 [!DNL Google Analytics] 設定檔ID。 在此情況下，您可以選擇將所有設定檔ID納入 [!DNL MBI]. 只要檢查您要在設定檔選取步驟期間包含的設定檔ID即可。

識別特定網站的 [!DNL Google Analytics] 配置檔案ID:

1. 登入 [!DNL Google Analytics]
1. 前往特定網站的 [!DNL Google Analytics] 儀表板
1. 查看URL — 設定檔ID對應至下列8個數字 `p` 在行尾：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 斷開連接 [!DNL Google Analytics] 從 [!DNL MBI] {#disconnect}

1. 造訪您的 [!DNL Google Analytics] [帳戶設定](https://www.google.com/accounts/) 頁面。
1. 在 `Security` ，然後按一下 **[!UICONTROL edit]** 下一頁 `Authorizing` 應用程式和網站。
1. 按一下 **[!UICONTROL revoke access]** 下一頁 [!DNL MBI].

## 相關：

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [連接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析網站活動和客戶轉換率](../../analysis/web-act-cust-conversion.md)
* [使用追蹤使用者贏取資料 [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
