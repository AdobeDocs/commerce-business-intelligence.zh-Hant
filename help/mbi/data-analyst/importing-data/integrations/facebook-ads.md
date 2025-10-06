---
title: 連線Facebook廣告
description: 瞭解如何分析您的廣告支出資料，並瞭解您的錢是否花得有效率。
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 連線[!DNL Facebook Ads]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![Facebook廣告標誌](../../../assets/facebook-ads-logo.png)

您做了調查、製作廣告、在[!DNL Facebook]上啟動行銷活動。 現在，您可以分析廣告支出資料，看看您的錢是否花得有效率。 使用您的廣告支出資料，您可以將您的廣告成本與客戶期限值(CLV)配對[評估行銷活動ROI （從行銷活動取得的使用者）](../../../data-analyst/analysis/roi-ad-camp.md)。

將您的[!DNL Facebook Ad]資料連線到[!DNL Commerce Intelligence]是一個簡單的三個步驟程式：

1. [將 [!DNL Facebook] 新增為 [!DNL Commerce Intelligence]中的資料來源](#stepone)
1. [允許 [!DNL Commerce Intelligence] 存取您的 [!DNL Facebook Ads] 資料](#steptwo)
1. [選取要提取資料的 [!DNL Facebook Ads] 帳戶](#stepthree)

## 將[!DNL Facebook]新增為[!DNL Commerce Intelligence]中的資料來源 {#stepone}

1. 若要將[!DNL Facebook]整合新增至您的[!DNL Commerce Intelligence]帳戶，請瀏覽至`Connections`下的&#x200B;**[!UICONTROL Manage Data** > **Integrations]**&#x200B;頁面。
1. 按一下右側的&#x200B;**[!UICONTROL Add Integration]**。
1. 按一下[!DNL Facebook]圖示。 這會顯示[!DNL Facebook]授權頁面。
1. 按一下&#x200B;**[!UICONTROL Authorize]**。

## 允許[!DNL Commerce Intelligence]存取您的[!DNL Facebook Ads]資料 {#steptwo}

按一下&#x200B;**[!DNL Facebook Authorize]**&#x200B;之後，會顯示一個小型快顯視窗：

![Commerce Intelligence的Facebook存取許可權對話方塊](../../../assets/Facebook_Access_Popup.png)

您可以依照一系列步驟，允許[!DNL Commerce Intelligence]存取您公用設定檔、[!DNL Facebook Ads]和相關統計資料中的資料。 按一下這些步驟上的&#x200B;**[!UICONTROL OK]**&#x200B;以繼續。

## 選取要提取資料的[!DNL Facebook Ads]帳戶 {#stepthree}

1. 驗證完成後，系統會提示您選取要提取資料的[!DNL Facebook Ads]帳戶。 按一下`Connect`欄中的核取方塊，以選取所需的帳戶。

   ![Facebook廣告帳戶選擇介面](../../../assets/Facebook_Ad_Accounts.png)

1. 按一下&#x200B;**[!UICONTROL Save Connections]**。

   如果連線成功，*連線成功！*&#x200B;訊息會顯示在頁面頂端。

## 接下來呢？ {#next}

請確定您正在追蹤[!DNL Facebook]中的[!DNL Google Analytics]個行銷活動。 這可確保已針對您的`utm\_campaign`行銷活動正確填入[!DNL Google Analytics]中的[!DNL Facebook]欄位。

## 相關

* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
* [連線您的 [!DNL Google Adwords] 帳戶](../integrations/google-ecommerce.md)
* [透過 [!DNL Google eCommerce]追蹤訂單轉介來源](../integrations/google-ecommerce.md)
* [追蹤資料庫中的使用者反向連結來源](../../analysis/google-track-user-acq.md)
* [追蹤資料庫中的使用者裝置、瀏覽器和作業系統資料](../../analysis/track-usr-dev-browser.md)
* [探索您最有價值的贏取來源和管道](../../analysis/most-value-source-channel.md)
* [提高廣告行銷活動的ROI](../../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM歸因如何運作？](../../analysis/utm-attributes.md)
