---
title: 連線Stripe
description: 瞭解如何管理及追蹤企業的付款及發票資料。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '151'
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
