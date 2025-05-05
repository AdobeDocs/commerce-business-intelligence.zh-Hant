---
title: 連線Mixpanel
description: 瞭解如何分析使用者如何導覽及使用您的網站和應用程式。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 連線[!DNL Mixpanel]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![](../../../assets/Mixpanel_logo.png)

透過[!DNL Mixpanel]，您可以分析使用者如何導覽及使用您的網站和應用程式。 仔細檢視使用者行為資料可導致更聰明的設計和開發決策，也就是說總體上可獲得更好的產品。 將[!DNL Mixpanel]連線至[!DNL Commerce Intelligence]可讓您分析使用者的行為以及該行為轉化為收入的方式。

將您的[!DNL Mixpanel]資料連線到[!DNL Commerce Intelligence]一個簡單的三個步驟程式：

1. [在 [!DNL Commerce Intelligence]中開啟 [!DNL Mixpanel] 認證頁面](#stepone)
1. [擷取您的 [!DNL Mixpanel] API認證](#steptwo)
1. [在 [!DNL Commerce Intelligence]中輸入您的 [!DNL Mixpanel] API認證](#stepthree)

若要完成此程式，您必須開啟兩個瀏覽器視窗或索引標籤，一個用於[!DNL Commerce Intelligence]，另一個用於您的[!DNL Mixpanel]帳戶。

## 正在開啟[!DNL Mixpanel]認證頁面 {#stepone}

開始使用：

1. 移至&#x200B;**[!DNL Manage Data** > **Connections]**&#x200B;下的`Connections`頁面。

1. 按一下`Data Sources`表格上方熒幕右側的&#x200B;**[!UICONTROL Add a New Source]**。

1. 按一下[!DNL Mixpanel]圖示並開啟認證頁面。

暫時保持此頁面開啟，並使用您的[!DNL Mixpanel]帳戶切換至瀏覽器視窗。

## 正在擷取您的[!DNL Mixpanel] API認證 {#steptwo}

如果您尚未登入您的[!DNL Mixpanel]帳戶，請先登入，然後再執行下列動作：

1. 按一下右上角的&#x200B;**[!UICONTROL Account]**。

1. 在顯示的對話方塊中，按一下&#x200B;**[!UICONTROL Projects]**。

1. 您的API認證顯示：

![正在擷取Mixpanel API認證](../../../assets/Mixpanel_API_creds.png)

請保持此開啟，您需要它來結束此工作。

## 在[!DNL Commerce Intelligence]中輸入您的[!DNL Mixpanel] API認證 {#stepthree}

1. 將`API Key`和`Secret`複製到[!DNL Commerce Intelligence]中的[!DNL Mixpanel]認證頁面。
1. 按一下&#x200B;**[!UICONTROL Connect to Mixpanel]**&#x200B;以完成設定。

如果連線成功，則為&#x200B;_成功！_&#x200B;訊息會顯示在頁面頂端。

### 相關

* [預期 [!DNL Mixpanel] 資料](../integrations/mixpanel-data.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
