---
title: 連接Zendesk
description: 瞭解如何整合幫助台報告 [!DNL Commerce Intelligence]。
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 連接 [!DNL Zendesk]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/Zendesk_logo.png)

連接 [!DNL Zendesk] 資料使您能夠在 [!DNL Commerce Intelligence]。 這使您能夠優化客戶支援並監控服務台的效能以及收入。

連接 [!DNL Zendesk] 資料是一個簡單的三步過程：

1. [開啟 [!DNL Zendesk] 「憑據」頁 [!DNL Commerce Intelligence]](#stepone)
1. [檢索 [!DNL Zendesk] API令牌](#steptwo)
1. [輸入 [!DNL Zendesk] 登錄資訊和令牌 [!DNL Commerce Intelligence]](#stepthree)

要完成此過程，您需要開啟兩個瀏覽器窗口或頁籤 — 一個 [!DNL Commerce Intelligence]，另一個 [!DNL Zendesk] 帳戶。

## 開啟 [!DNL Zendesk] 「憑據」頁 [!DNL Commerce Intelligence] {#stepone}

1. 轉到 `Integrations` 頁 **[!UICONTROL Manage Data** > **&#x200B;資料源&#x200B;**> **整合]**。
1. 按一下 **[!UICONTROL Add Integration]**，位於螢幕的右側。
1. 按一下 [!DNL Zendesk] 表徵圖 開啟 [!DNL Zendesk] 「憑據」頁。

## 檢索 [!DNL Zendesk] API令牌 {#steptwo}

1. 在登錄到的窗口/頁籤中 [!DNL Zendesk] 帳戶，按一下螢幕左下角的「設定（齒輪）」表徵圖。
1. 當 `Settings` 菜單顯示，查找 `Channels` 的子菜單。 按一下 **[!UICONTROL API]** 的下界。
1. 在 `Token Access` 頁面中，按一下旁邊的複選框 `Enabled`。 顯示活動API令牌的清單。
1. 按一下 **[!UICONTROL Add New Token]**。
1. 出現提示時，請輸入令牌的標籤。 Adobe建議使用 `Commerce Intelligence`，您一眼就知道，哪個應用程式正在使用令牌。
1. 按一下 **[!UICONTROL Create]**。
1. 建立API令牌。 複製此令牌；下一步將使用。

## 輸入 [!DNL Zendesk] 登錄資訊和API令牌 [!DNL Commerce Intelligence] {#stepthree}

1. 輸入 [!DNL Zendesk] 站點前置詞和登錄電子郵件 [!DNL Zendesk] 「憑據」頁 [!DNL Commerce Intelligence]。
1. 輸入API令牌。
1. 按一下 **[!UICONTROL Save & Connect]**。 如果連接成功，則 *連接成功！* 消息顯示在螢幕頂部。

## 相關：

* [預期 [!DNL Zendesk] 資料](../integrations/exp-zendesk-data.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
