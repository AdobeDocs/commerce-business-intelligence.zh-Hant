---
title: 連接混合面板
description: 瞭解如何分析用戶如何導航和使用您的網站和應用。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 連接 [!DNL Mixpanel]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/Mixpanel_logo.png)

與 [!DNL Mixpanel]，您可以分析用戶如何導航和使用您的網站和應用。 仔細查看用戶行為資料會帶來更明智的設計和開發決策，這意味著整體產品更好。 連接 [!DNL Mixpanel] 至 [!DNL Commerce Intelligence] 用於分析用戶的行為以及該行為如何轉化為收入。

連接 [!DNL Mixpanel] 資料 [!DNL Commerce Intelligence] 一個簡單的三步過程：

1. [開啟 [!DNL Mixpanel] 「憑據」頁 [!DNL Commerce Intelligence]](#stepone)
1. [檢索 [!DNL Mixpanel] API憑據](#steptwo)
1. [輸入 [!DNL Mixpanel] API憑據 [!DNL Commerce Intelligence]](#stepthree)

要完成此過程，您需要開啟兩個瀏覽器窗口或頁籤，一個用於 [!DNL Commerce Intelligence] 另一個是 [!DNL Mixpanel] 帳戶。

## 開啟 [!DNL Mixpanel] 「憑據」頁 {#stepone}

開始：

1. 轉到 `Connections` 頁 **[!DNL Manage Data** > **Connections]**。

1. 按一下 **[!UICONTROL Add a New Source]**，位於螢幕右側，位於 `Data Sources` 的子菜單。

1. 按一下 [!DNL Mixpanel] 表徵圖並開啟「憑據」頁。

使此頁面暫時開啟，並切換到瀏覽器窗口 [!DNL Mixpanel] 帳戶。

## 正在檢索 [!DNL Mixpanel] API憑據 {#steptwo}

如果您尚未登錄 [!DNL Mixpanel] )，然後執行以下操作：

1. 按一下 **[!UICONTROL Account]** 在右上角。

1. 在顯示的對話框中，按一下 **[!UICONTROL Projects]**。

1. API憑據顯示：

![正在檢索Mixpanel API憑據](../../../assets/Mixpanel_API_creds.png)

保持開啟狀態，你需要它來收尾。

## 輸入 [!DNL Mixpanel] API憑據 [!DNL Commerce Intelligence] {#stepthree}

1. 複製 `API Key` 和 `Secret` 到 [!DNL Mixpanel] 「憑據」頁 [!DNL Commerce Intelligence]。
1. 按一下 **[!UICONTROL Connect to Mixpanel]** 完成設定。

如果連接成功，則 _成功！_ 消息顯示在頁面頂部。

### 相關

* [預期 [!DNL Mixpanel] 資料](../integrations/mixpanel-data.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
