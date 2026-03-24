---
title: 連線Zendesk
description: 瞭解如何在 [!DNL Commerce Intelligence]中合併服務檯報告。
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KBUuqTDD9s3qXDktcV3RzLx4zxtAFwAkKPbsQE2YGtI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 261
ht-degree: 0%

---

# 連線[!DNL Zendesk]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![Zendesk標誌](../../../assets/Zendesk_logo.png)

連線您的[!DNL Zendesk]資料可讓您在[!DNL Commerce Intelligence]中合併服務檯報告。 這可讓您最佳化客戶支援，並監控服務檯績效與您的收入。

連線您的[!DNL Zendesk]資料是一個簡單的三個步驟程式：

1. [在 [!DNL Zendesk] 中開啟 [!DNL Commerce Intelligence]認證頁面](#stepone)
1. [擷取您的 [!DNL Zendesk] API Token](#steptwo)
1. [在 [!DNL Zendesk] 中輸入您的 [!DNL Commerce Intelligence]登入資訊和權杖](#stepthree)

若要完成此程式，您必須開啟兩個瀏覽器視窗或索引標籤，一個用於[!DNL Commerce Intelligence]，另一個用於您的[!DNL Zendesk]帳戶。

## 在[!DNL Zendesk]中開啟[!DNL Commerce Intelligence]認證頁面 {#stepone}

1. 移至`Integrations`資料來源&#x200B;**[!UICONTROL Manage Data** > **&#x200B; > &#x200B;** 整合&#x200B;**下的]**&#x200B;頁面。
1. 按一下畫面右側的&#x200B;**[!UICONTROL Add Integration]**。
1. 按一下[!DNL Zendesk]圖示。 這會開啟[!DNL Zendesk]認證頁面。

## 擷取您的[!DNL Zendesk] API Token {#steptwo}

1. 在您登入[!DNL Zendesk]帳戶的視窗/標籤中，按一下畫面左下角的「設定」（齒輪）圖示。
1. 顯示`Settings`功能表時，找出`Channels`區段。 按一下此區段中的&#x200B;**[!UICONTROL API]**。
1. 在此頁面的`Token Access`區段中，按一下`Enabled`旁的核取方塊。 顯示作用中API Token清單。
1. 按一下&#x200B;**[!UICONTROL Add New Token]**。
1. 出現提示時，輸入權杖的標籤。 Adobe建議使用`Commerce Intelligence`，以便於您一眼就能知道使用權杖的應用程式。
1. 按一下&#x200B;**[!UICONTROL Create]**。
1. API權杖已建立。 複製此Token；它將在下一個步驟中使用。

## 在[!DNL Zendesk]中輸入[!DNL Commerce Intelligence]登入資訊和API權杖 {#stepthree}

1. 在[!DNL Zendesk]的[!DNL Zendesk]認證頁面中輸入您的[!DNL Commerce Intelligence]網站首碼和登入電子郵件。
1. 輸入您的API Token。
1. 按一下&#x200B;**[!UICONTROL Save & Connect]**。 如果連線成功，*連線成功！*&#x200B;訊息會顯示在畫面頂端。

## 相關：

* [預期 [!DNL Zendesk] 資料](../integrations/exp-zendesk-data.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
