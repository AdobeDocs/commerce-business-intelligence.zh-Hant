---
title: 連線Stripe
description: 瞭解如何管理及追蹤企業的付款及發票資料。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Connect [!DNL Stripe]

>[!NOTE]
>
>需要 [管理員許可權](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] 可讓您管理及追蹤企業的付款與商業發票資料。 正在連線您的 [!DNL Stripe] 帳戶至 [!DNL Commerce Intelligence] 是一個簡單的兩個步驟程式：

1. [新增 [!DNL Stripe] 作為中的資料來源 [!DNL Commerce Intelligence]](#stepone)
1. [允許 [!DNL Commerce Intelligence] 存取您的 [!DNL Stripe] 資料](#steptwo)

## 新增 [!DNL Stripe] 作為資料來源 {#stepone}

1. 前往 `Connections` 頁面於 **[!UICONTROL Admin** > **Connections]**.
1. 按一下 **[!UICONTROL Add a Data Source]**，位於熒幕右側 `Data Sources` 表格。
1. 按一下 [!DNL Stripe] 圖示。 這會顯示 `[!DNL Stripe] authorization` 頁面。
1. 按一下 **[!UICONTROL Connect with Stripe]**.

## 允許 [!DNL Commerce Intelligence] 存取您的 [!DNL Stripe] 資料 {#steptwo}

按一下 **[!UICONTROL Connect with Stripe]**，就會顯示存取要求頁面。

1. 按一下 **[!UICONTROL Sign in with Stripe to Continue]**.

1. 輸入您的認證，然後按一下 **[!UICONTROL Sign in to your account]**.

1. 將會驗證您的認證，並將您導向回 [!DNL Commerce Intelligence].

1. 如果連線成功， *連線成功！* 訊息會顯示在畫面頂端。

## 相關：

此 [[!DNL Stripe] API檔案](https://stripe.com/docs/api) 可作為進一步瞭解如何操作的有用資源 [!DNL Stripe] 與整合 [!DNL Commerce Intelligence].

* [預期 [!DNL Stripe] 資料](../integrations/stripe-data.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
