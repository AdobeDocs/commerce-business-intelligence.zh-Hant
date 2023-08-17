---
title: 連線Google Analytics
description: 瞭解如何連結Google Analytics [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 連線 [!DNL Google Analytics]

>[!NOTE]
>
>需要 [管理員許可權](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是網際網路上使用最廣泛的網頁分析服務。 實作 [!DNL Google Analytics] 可讓您在網站上追蹤訪客如何使用您的網站、哪些內容吸引人、訪客的退出位置等。 在中分析這些量度 [!DNL Commerce Intelligence]，連同其他資料片段，可改善您網站的整體健康狀況和可用性。

輸入您的網站以開始 [!DNL Google Analytics] 憑證進入 [!DNL Commerce Intelligence]：

1. 前往 **[!UICONTROL Manage Data** > **Integrations]**.

1. 按一下 **[!UICONTROL Add Integration]**，位於畫面右側。

1. 按一下 [!DNL Google Analytics] 圖示。 如此將可開啟 [!DNL Google Analytics] 證明資料頁面。

1. 輸入您的 [!DNL Google Analytics] 認證。 授權程式完成後，您會被重新導向回 [!DNL Commerce Intelligence].

1. 設定檔ID清單隨即顯示。 檢查您要連線的設定檔 [!DNL Commerce Intelligence]. 如果您有多個設定檔，並且需要一些幫助來識別哪一個，請參閱連線多個 [!DNL Google Analytics] 設定檔區段底下。

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 變更會自動儲存，因此請按一下 **返回連線** 完成時。

## 正在連線多個 [!DNL Google Analytics] 設定檔

您可能有多個網站連線至單一 [!DNL Google Analytics] 帳戶，由其自身識別 [!DNL Google Analytics] 設定檔ID。 在此情況下，您可以選擇將您的所有設定檔ID包含在 [!DNL Commerce Intelligence]. 在設定檔選取步驟中，檢查您要包含的設定檔ID。

識別特定網站的 [!DNL Google Analytics] 設定檔ID：

1. 登入 [!DNL Google Analytics]
1. 前往特定網站的 [!DNL Google Analytics] 儀表板
1. 檢視URL — 設定檔ID對應至下列八個數字 `p` 行尾：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 正在中斷連線 [!DNL Google Analytics] 從 [!DNL Commerce Intelligence] {#disconnect}

1. 造訪您的 [!DNL Google Analytics] [帳戶設定](https://accounts.google.com/) 頁面。
1. 在 `Security` 部分，然後按一下 **[!UICONTROL edit]** 旁邊 `Authorizing` 應用程式和網站。
1. 按一下 **[!UICONTROL revoke access]** 旁邊 [!DNL Commerce Intelligence].

## 相關：

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [正在連線 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析網站活動和客戶轉換率](../../analysis/web-act-cust-conversion.md)
* [使用追蹤使用者贏取資料 [!DNL Google Analytics] Cookie](../../analysis/google-track-user-acq.md)
