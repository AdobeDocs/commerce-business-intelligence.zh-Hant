---
title: 連線Zendesk
description: 瞭解如何在中整合您的服務檯報告 [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# 連線 [!DNL Zendesk]

>[!NOTE]
>
>需要 [管理員許可權](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

正在連線您的 [!DNL Zendesk] 資料可讓您將服務檯報告整合到 [!DNL Commerce Intelligence]. 這可讓您最佳化客戶支援，並監控服務檯績效與您的收入。

正在連線您的 [!DNL Zendesk] 資料是一個簡單的三個步驟流程：

1. [開啟 [!DNL Zendesk] 認證頁面，位於 [!DNL Commerce Intelligence]](#stepone)
1. [擷取您的 [!DNL Zendesk] API Token](#steptwo)
1. [輸入您的 [!DNL Zendesk] 中的登入資訊和權杖 [!DNL Commerce Intelligence]](#stepthree)

若要完成此程式，您必須開啟兩個瀏覽器視窗或標籤 — 一個用於 [!DNL Commerce Intelligence]，您的另一個 [!DNL Zendesk] 帳戶。

## 開啟 [!DNL Zendesk] 認證頁面，位於 [!DNL Commerce Intelligence] {#stepone}

1. 前往 `Integrations` 頁面於 **[!UICONTROL Manage Data** > **&#x200B;資料來源&#x200B;**> **整合]**.
1. 按一下 **[!UICONTROL Add Integration]**，位於畫面右側。
1. 按一下 [!DNL Zendesk] 圖示。 如此將可開啟 [!DNL Zendesk] 證明資料頁面。

## 擷取您的 [!DNL Zendesk] API權杖 {#steptwo}

1. 在您登入的視窗/標籤中 [!DNL Zendesk] 帳戶，請按一下畫面左下角的「設定」 （齒輪）圖示。
1. 當 `Settings` 功能表顯示，找到 `Channels` 區段。 按一下 **[!UICONTROL API]** 在本節中。
1. 在 `Token Access` 區段，按一下旁邊的核取方塊 `Enabled`. 顯示作用中API Token清單。
1. 按一下 **[!UICONTROL Add New Token]**.
1. 出現提示時，輸入權杖的標籤。 Adobe建議使用 `Commerce Intelligence`，所以您一眼就能知道使用代號的應用程式。
1. 按一下 **[!UICONTROL Create]**.
1. API權杖已建立。 複製此Token；它將在下一個步驟中使用。

## 輸入 [!DNL Zendesk] 登入資訊和API權杖登入 [!DNL Commerce Intelligence] {#stepthree}

1. 輸入您的 [!DNL Zendesk] 中的網站首碼和登入電子郵件 [!DNL Zendesk] 認證頁面，位於 [!DNL Commerce Intelligence].
1. 輸入您的API Token。
1. 按一下 **[!UICONTROL Save & Connect]**. 如果連線成功， *連線成功！* 訊息會顯示在畫面頂端。

## 相關：

* [預期 [!DNL Zendesk] 資料](../integrations/exp-zendesk-data.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
