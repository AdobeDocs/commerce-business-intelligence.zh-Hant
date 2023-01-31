---
title: 連接Mixpanel
description: 了解如何分析使用者如何導覽及運用您的網站和應用程式。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Connect [!DNL Mixpanel]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

使用 [!DNL Mixpanel]，您可以分析使用者如何導覽及運用您的網站和應用程式。 深入了解使用者行為資料，便能做出更明智的設計和開發決策，整體上更佳的產品。 連接 [!DNL Mixpanel] to [!DNL MBI] 可讓您分析使用者的行為，以及該行為轉化為收入的方式。

連接 [!DNL Mixpanel] 資料 [!DNL MBI] 簡單的三步法：

1. [開啟 [!DNL Mixpanel] 憑據頁 [!DNL MBI]](#stepone)
1. [擷取 [!DNL Mixpanel] API憑證](#steptwo)
1. [輸入 [!DNL Mixpanel] MBI中的API憑據](#stepthree)

若要完成此程式，您需要開啟兩個瀏覽器視窗或標籤，其中一個用於 [!DNL MBI]，另一個 [!DNL Mixpanel] 帳戶。

## 開啟 [!DNL Mixpanel] 認證頁面 {#stepone}

讓我們開始吧：

1. 前往 `Connections` 頁面底下 **[!DNL Manage Data** > **Connections]**.
1. 按一下 **[!UICONTROL Add a New Source]**，位於畫面的右側，位於 `Data Sources` 表格。
1. 按一下 [!DNL Mixpanel] 表徵圖和憑據頁將開啟。

暫時保持此頁面開啟，並切換至瀏覽器視窗，並使用 [!DNL Mixpanel] 帳戶。

## 擷取 [!DNL Mixpanel] API憑證 {#steptwo}

如果您尚未登入 [!DNL Mixpanel] 帳戶時，請執行此操作，然後執行下列操作：

1. 按一下 **[!UICONTROL Account]** 在右上角。
1. 在顯示的對話方塊中，按一下 **[!UICONTROL Projects]**.
1. 您的API憑證將會顯示：

![擷取Mixpanel API憑證](../../../assets/Mixpanel_API_creds.png)

保持開啟 — 我們需要它來把它包起來。

## 輸入 [!DNL Mixpanel] 中的API憑證 [!DNL MBI] {#stepthree}

1. 複製 `API Key` 和 `Secret` 進入 [!DNL Mixpanel] 憑據頁 [!DNL MBI].
1. 按一下 **[!UICONTROL Connect to Mixpanel]** 以完成設定。

就這樣！ 如果連線成功，則 _成功！_ 訊息會顯示在頁面頂端。

### 相關

* [預期 [!DNL Mixpanel] 資料](../integrations/mixpanel-data.md)
* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
