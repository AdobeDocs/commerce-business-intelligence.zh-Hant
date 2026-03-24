---
title: 連線Stripe
description: 瞭解如何管理及追蹤企業的付款及發票資料。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/S6-otAlCeS8aKQ6K-xZH2ZaqEjZ-ZZ6fMWXtFFafu6c
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
source-wordcount: 151
ht-degree: 0%

---

# 連線[!DNL Stripe]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![Stripe標誌](../../../assets/stripe-logo.png)

[!DNL Stripe]可讓您管理及追蹤企業的付款與發票資料。 將您的[!DNL Stripe]帳戶連線到[!DNL Commerce Intelligence]是簡單的兩個步驟程式：

1. [將 [!DNL Stripe] 新增為 [!DNL Commerce Intelligence]中的資料來源](#stepone)
1. [允許 [!DNL Commerce Intelligence] 存取您的 [!DNL Stripe] 資料](#steptwo)

## 將[!DNL Stripe]新增為資料來源 {#stepone}

1. 移至`Connections`下的&#x200B;**[!UICONTROL Admin** > **Connections]**&#x200B;頁面。
1. 按一下&#x200B;**[!UICONTROL Add a Data Source]**&#x200B;表格上方熒幕右側的`Data Sources`。
1. 按一下[!DNL Stripe]圖示。 這會顯示`[!DNL Stripe] authorization`頁面。
1. 按一下&#x200B;**[!UICONTROL Connect with Stripe]**。

## 允許[!DNL Commerce Intelligence]存取您的[!DNL Stripe]資料 {#steptwo}

按一下&#x200B;**[!UICONTROL Connect with Stripe]**&#x200B;之後，會出現存取要求頁面。

1. 按一下&#x200B;**[!UICONTROL Sign in with Stripe to Continue]**。

1. 輸入您的認證並按一下&#x200B;**[!UICONTROL Sign in to your account]**。

1. 將會驗證您的認證，並將您導向回[!DNL Commerce Intelligence]。

1. 如果連線成功，*連線成功！*&#x200B;訊息會顯示在畫面頂端。

## 相關：

[[!DNL Stripe] API檔案](https://stripe.com/docs/api)可以成為瞭解更多有關[!DNL Stripe]如何與[!DNL Commerce Intelligence]整合的實用資源。

* [預期 [!DNL Stripe] 資料](../integrations/stripe-data.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
