---
title: Connect Zendesk
description: 了解如何在 [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Connect [!DNL Zendesk]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

連接 [!DNL Zendesk] 資料可讓您整合 [!DNL MBI]. 這可讓您最佳化客戶支援，並監控服務台效能與收入。

連接 [!DNL Zendesk] 資料是簡單的三步驟程式：

1. [開啟 [!DNL Zendesk] 憑據頁 [!DNL MBI]](#stepone)
1. [擷取 [!DNL Zendesk] API Token](#steptwo)
1. [輸入 [!DNL Zendesk] 登入資訊和Token，於 [!DNL MBI]](#stepthree)

若要完成此程式，您需要開啟兩個瀏覽器視窗或標籤，其中一個用於 [!DNL MBI]，另一個 [!DNL Zendesk] 帳戶。

## 開啟 [!DNL Zendesk] 憑據頁 [!DNL MBI] {#stepone}

1. 前往 `Integrations` 頁面底下 **[!UICONTROL Manage Data** > **&#x200B;資料來源&#x200B;**> **整合]**.
1. 按一下 **[!UICONTROL Add Integration]**，位於畫面的右側。
1. 按一下 [!DNL Zendesk] 表徵圖。 這會開啟 [!DNL Zendesk] 憑據頁。

## 擷取 [!DNL Zendesk] API代號 {#steptwo}

1. 在您登入 [!DNL Zendesk] 帳戶，按一下畫面左下角的「設定」（齒輪）圖示。
1. 當 `Settings` 功能表，找出 `Channels` 區段。 按一下 **[!UICONTROL API]** 在本節中。
1. 在 `Token Access` ，按一下旁邊的複選框 `Enabled`. 將顯示「作用中API代號」清單。
1. 按一下 **[!UICONTROL Add New Token]**.
1. 出現提示時，請為代號輸入標籤。 建議您使用 `MBI`，您一看就知道使用代號的應用程式。
1. 按一下 **[!UICONTROL Create]**.
1. 將建立API代號。 複製此代號；它將用於下一步。

## 輸入 [!DNL Zendesk] 登入資訊和API代號 [!DNL MBI] {#stepthree}

1. 輸入 [!DNL Zendesk] 網站首碼和登入電子郵件 [!DNL Zendesk] 憑據頁 [!DNL MBI].
1. 輸入您的API代號。
1. 按一下 **[!UICONTROL Save & Connect]**. 如果連線成功，則 *連接成功！* 訊息會顯示在畫面頂端。

## 相關：

* [預期 [!DNL Zendesk] 資料](../integrations/exp-zendesk-data.md)
* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
