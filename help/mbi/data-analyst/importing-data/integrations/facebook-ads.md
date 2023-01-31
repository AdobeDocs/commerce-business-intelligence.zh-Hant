---
title: Connect Facebook Ads
description: 了解如何分析您的廣告支出資料，並查看您的資金是否得到有效支援。
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Connect [!DNL Facebook Ads]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/Facebook_Logo.png)

你做了調查，製作了廣告，在 [!DNL Facebook]. 現在，您可以分析廣告支出資料，並查看您的資金是否得到有效支援。 使用您的廣告支出資料，您可以 [將廣告成本和客戶期限值(CLV)結合在一起，以評估行銷活動的投資報酬率](../../../data-analyst/analysis/roi-ad-camp.md) 從您的行銷活動獲得的使用者。

將您的Facebook廣告資料連結至 [!DNL MBI] 是簡單的三步驟程式：

1. [新增 [!DNL Facebook] 作為 [!DNL MBI]](#stepone)
1. [允許 [!DNL MBI] 存取 [!DNL Facebook Ads] 資料](#steptwo)
1. [選擇 [!DNL Facebook Ads] 提取資料的帳戶](#stepthree)

## 新增 [!DNL Facebook] 作為 [!DNL MBI] {#stepone}

1. 若要新增 [!DNL Facebook] 與帳戶的整合，導覽至 `Connections` 頁面底下 **[!UICONTROL Manage Data** > **Integrations]**.
1. 按一下 **[!UICONTROL Add Integration]**，位於資料上方畫面的右側 `Sources` 表格。
1. 按一下 [!DNL Facebook] 表徵圖。 這會顯示 [!DNL Facebook] 授權頁面。
1. 按一下 **[!UICONTROL Authorize]**.

## 允許 [!DNL MBI] 存取 [!DNL Facebook Ads] 資料 {#steptwo}

按一下 **[!DNL Facebook Authorize]**，會顯示一個小型快顯視窗：

![](../../../assets/Facebook_Access_Popup.png)

您將依照一系列步驟來允許 [!DNL MBI] 要從公共配置檔案訪問資料， [!DNL Facebook Ads] 和相關統計資料。 按一下 **[!UICONTROL OK]** 繼續。

## 選擇 [!DNL Facebook Ads] 提取資料的帳戶 {#stepthree}

1. 驗證完成後，系統會提示您選取 [!DNL Facebook Ads] 要提取資料的帳戶。 按一下 `Connect` 欄。

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. 按一下 **[!UICONTROL Save Connections]**.

   如果連線成功，則 *連接成功！* 訊息會顯示在頁面頂端。

## 接下來呢？ {#next}

請確定您正在追蹤 [!DNL Facebook] 行銷活動 [!DNL Google Analytics] 按照 [教學課程](https://www.facebook.com/business/google-analytics). 這將確保 `utm\_campaign` 欄位 [!DNL Google Analytics] 正確填入 [!DNL Facebook] 行銷活動。

## 相關

* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
* [連接您的 [!DNL Google Adwords] 帳戶](../integrations/google-ecommerce.md)
* [透過追蹤訂單轉介來源 [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [在您的資料庫中追蹤使用者反向連結來源](../../analysis/google-track-user-acq.md)
* [在資料庫中追蹤使用者裝置、瀏覽器和作業系統資料](../../analysis/track-usr-dev-browser.md)
* [探索您最有價值的贏取來源和管道](../../analysis/most-value-source-channel.md)
* [提高廣告宣傳的投資報酬率](../../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM歸因功能是否正常？](../../analysis/utm-attributes.md)
