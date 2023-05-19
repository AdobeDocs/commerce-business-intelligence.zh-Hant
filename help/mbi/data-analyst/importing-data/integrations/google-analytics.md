---
title: 連接Google Analytics
description: 學習將Google Analytics與 [!DNL Commerce Intelligence]。
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 連接 [!DNL Google Analytics]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是網際網路上使用最廣泛的Web分析服務。 實施 [!DNL Google Analytics] 在您的網站上，您可以跟蹤訪問者如何使用您的網站、哪些內容很吸引人、訪問者離開的地方等。 在 [!DNL Commerce Intelligence]除了其他資料外，還可改善您站點的整體健康和可用性。

通過輸入 [!DNL Google Analytics] 憑據 [!DNL Commerce Intelligence]:

1. 轉到 **[!UICONTROL Manage Data** > **Integrations]**。

1. 按一下 **[!UICONTROL Add Integration]**，位於螢幕的右側。

1. 按一下 [!DNL Google Analytics] 表徵圖 開啟 [!DNL Google Analytics] 「憑據」頁。

1. 輸入 [!DNL Google Analytics] 憑據。 在完成授權過程後，您將被重定向回 [!DNL Commerce Intelligence]。

1. 顯示配置檔案ID的清單。 檢查要連接到的配置檔案 [!DNL Commerce Intelligence]。 如果您有多個配置式，並且需要一些幫助來確定哪個是，請參閱「連接多個」 [!DNL Google Analytics] 配置檔案部分。

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 更改將自動保存，因此按一下 **返回連接** 等你做完。

## 連接多個 [!DNL Google Analytics] 配置檔案

您可能有多個網站連接到一個 [!DNL Google Analytics] 帳戶，由自己確定 [!DNL Google Analytics] 配置檔案ID。 在這種情況下，您可以選擇將所有配置檔案ID包含在 [!DNL Commerce Intelligence]。 檢查要在配置檔案選擇步驟中包括的配置檔案ID。

確定特定網站的 [!DNL Google Analytics] 配置檔案ID:

1. 登錄 [!DNL Google Analytics]
1. 轉到特定網站 [!DNL Google Analytics] 儀表板
1. 查看URL — 配置檔案ID對應於以下八個數字 `p` 在行末：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 斷開 [!DNL Google Analytics] 從 [!DNL Commerce Intelligence] {#disconnect}

1. 訪問 [!DNL Google Analytics] [帳戶設定](https://accounts.google.com/) 的子菜單。
1. 在 `Security` ，然後按一下 **[!UICONTROL edit]** 下 `Authorizing` 應用程式和站點。
1. 按一下 **[!UICONTROL revoke access]** 下 [!DNL Commerce Intelligence]。

## 相關：

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [連接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析網站活動和客戶轉換率](../../analysis/web-act-cust-conversion.md)
* [使用跟蹤用戶獲取資料 [!DNL Google Analytics] 餅](../../analysis/google-track-user-acq.md)
