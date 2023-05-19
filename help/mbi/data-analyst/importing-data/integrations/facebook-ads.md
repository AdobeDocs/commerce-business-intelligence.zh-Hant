---
title: 連接Facebook廣告
description: 瞭解如何分析您的廣告支出資料，並瞭解您的資金是否得到有效支出。
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 連接 [!DNL Facebook Ads]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/facebook-ads-logo.png)

你做了調查，做了廣告，在 [!DNL Facebook]。 現在，是時候分析一下您的廣告支出資料，看看您的資金是否得到了有效的使用。 使用廣告支出資料，您 [將廣告成本與客戶生存期價值(CLV)相結合，以衡量市場活動的投資回報率](../../../data-analyst/analysis/roi-ad-camp.md) 從您的市場活動中獲得的用戶。

連接 [!DNL Facebook Ad] 資料 [!DNL Commerce Intelligence] 是一個簡單的三步過程：

1. [添加 [!DNL Facebook] 作為 [!DNL Commerce Intelligence]](#stepone)
1. [允許 [!DNL Commerce Intelligence] 訪問 [!DNL Facebook Ads] 資料](#steptwo)
1. [選擇 [!DNL Facebook Ads] 用於提取資料的帳戶](#stepthree)

## 添加 [!DNL Facebook] 作為 [!DNL Commerce Intelligence] {#stepone}

1. 添加 [!DNL Facebook] 整合 [!DNL Commerce Intelligence]帳戶，導航到 `Connections` 頁 **[!UICONTROL Manage Data** > **Integrations]**。
1. 按一下 **[!UICONTROL Add Integration]**&#x200B;的子菜單。
1. 按一下 [!DNL Facebook] 表徵圖 這將顯示 [!DNL Facebook] 授權頁。
1. 按一下 **[!UICONTROL Authorize]**。

## 允許 [!DNL Commerce Intelligence] 訪問 [!DNL Facebook Ads] 資料 {#steptwo}

按一下後 **[!DNL Facebook Authorize]**，將顯示一個小的彈出窗口：

![](../../../assets/Facebook_Access_Popup.png)

您可以執行一系列步驟來允許 [!DNL Commerce Intelligence] 從公共配置檔案訪問資料， [!DNL Facebook Ads] 以及相關資料。 按一下 **[!UICONTROL OK]** 繼續。

## 選擇 [!DNL Facebook Ads] 用於提取資料的帳戶 {#stepthree}

1. 驗證完成後，系統將提示您選擇 [!DNL Facebook Ads] 要從中提取資料的帳戶。 通過按一下 `Connect` 的雙曲餘切值。

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. 按一下 **[!UICONTROL Save Connections]**。

   如果連接成功，則 *連接成功！* 消息顯示在頁面頂部。

## 接下來呢？ {#next}

確保您正在跟蹤 [!DNL Facebook] 活動 [!DNL Google Analytics]。 這確保 `utm\_campaign` 欄位 [!DNL Google Analytics] 正確填充 [!DNL Facebook] 活動。

## 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [連接 [!DNL Google Adwords] 帳戶](../integrations/google-ecommerce.md)
* [跟蹤訂單推薦來源 [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [跟蹤資料庫中的用戶推薦源](../../analysis/google-track-user-acq.md)
* [跟蹤資料庫中的用戶設備、瀏覽器和OS資料](../../analysis/track-usr-dev-browser.md)
* [發現您最有價值的收購來源和渠道](../../analysis/most-value-source-channel.md)
* [提高廣告活動的ROI](../../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM歸因工作？](../../analysis/utm-attributes.md)
