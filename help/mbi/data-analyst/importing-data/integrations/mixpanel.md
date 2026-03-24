---
title: 連線Mixpanel
description: 瞭解如何分析使用者如何導覽及使用您的網站和應用程式。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/ap-nWiPVnPSpvUT4uiimZ7iC4fiuKvKH0ZMVkOTDcK8
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 246
ht-degree: 0%

---

# 連線[!DNL Mixpanel]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![Mixpanel標誌](../../../assets/Mixpanel_logo.png)

透過[!DNL Mixpanel]，您可以分析使用者如何導覽及使用您的網站和應用程式。 仔細檢視使用者行為資料可導致更聰明的設計和開發決策，也就是說總體上可獲得更好的產品。 將[!DNL Mixpanel]連線至[!DNL Commerce Intelligence]可讓您分析使用者的行為以及該行為轉化為收入的方式。

將您的[!DNL Mixpanel]資料連線到[!DNL Commerce Intelligence]一個簡單的三個步驟程式：

1. [在 [!DNL Mixpanel] 中開啟 [!DNL Commerce Intelligence]認證頁面](#stepone)
1. [擷取您的 [!DNL Mixpanel] API認證](#steptwo)
1. [在 [!DNL Mixpanel] 中輸入您的 [!DNL Commerce Intelligence]API認證](#stepthree)

若要完成此程式，您必須開啟兩個瀏覽器視窗或索引標籤，一個用於[!DNL Commerce Intelligence]，另一個用於您的[!DNL Mixpanel]帳戶。

## 正在開啟[!DNL Mixpanel]認證頁面 {#stepone}

開始使用：

1. 移至`Connections`下的&#x200B;**[!DNL Manage Data** > **Connections]**&#x200B;頁面。

1. 按一下&#x200B;**[!UICONTROL Add a New Source]**&#x200B;表格上方熒幕右側的`Data Sources`。

1. 按一下[!DNL Mixpanel]圖示並開啟認證頁面。

暫時保持此頁面開啟，並使用您的[!DNL Mixpanel]帳戶切換至瀏覽器視窗。

## 正在擷取您的[!DNL Mixpanel] API認證 {#steptwo}

如果您尚未登入您的[!DNL Mixpanel]帳戶，請先登入，然後再執行下列動作：

1. 按一下右上角的&#x200B;**[!UICONTROL Account]**。

1. 在顯示的對話方塊中，按一下&#x200B;**[!UICONTROL Projects]**。

1. 您的API認證顯示：

![正在擷取Mixpanel API認證](../../../assets/Mixpanel_API_creds.png)

請保持此開啟，您需要它來結束此工作。

## 在[!DNL Mixpanel]中輸入您的[!DNL Commerce Intelligence] API認證 {#stepthree}

1. 將`API Key`和`Secret`複製到[!DNL Mixpanel]中的[!DNL Commerce Intelligence]認證頁面。
1. 按一下&#x200B;**[!UICONTROL Connect to Mixpanel]**&#x200B;以完成設定。

如果連線成功，則為&#x200B;_成功！_&#x200B;訊息會顯示在頁面頂端。

### 相關

* [預期 [!DNL Mixpanel] 資料](../integrations/mixpanel-data.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
