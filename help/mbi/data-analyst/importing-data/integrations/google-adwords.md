---
title: 連線Google Adwords
description: 了解如何結合廣告成本和從行銷活動中獲得的使用者客戶終身價值(CLV)，以評估行銷活動的投資報酬率。
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Connect [!DNL Google Adwords]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

你做了調查，製作了廣告，發起了宣傳。 現在，您可以分析廣告支出資料，並查看您的資金是否得到有效支援。 使用您的廣告支出資料，您可以 [將廣告成本和客戶期限值(CLV)結合在一起，以評估行銷活動的投資報酬率](../../analysis/roi-ad-camp.md) 從您的行銷活動獲得的使用者。

輸入 [!DNL Google Adwords] 憑證 [!DNL MBI]:

1. 前往下方的「連線」頁面 **管理資料>整合**.
1. 按一下 **新增整合**，位於畫面的右上方。
1. 按一下 **[!DNL Google Adwords]** 表徵圖。 這會開啟 [!DNL Google Adwords] 憑據頁。
1. 輸入 [!DNL Google Analytics] 憑證。 授權程式完成後，系統會將您重新導向回 [!DNL MBI].
1. 隨即顯示設定檔ID清單。 檢查您要連線的設定檔 [!DNL MBI].

   ![](../../../assets/cnnct-profile.png)

1. 變更會自動儲存，因此按一下 **[!UICONTROL Back to Connections]** 等你完成。

如果您有多個設定檔，且需要一些說明來識別哪個是，請參閱 `Connecting Multiple Google Analytics profiles` 一節。

## `Connecting multiple Google Analytics profiles`

您可能有多個網站連結至單一 [!DNL Google Analytics] 帳戶，以其自己的 [!DNL Google Analytics] 設定檔ID。 在此情況下，您可以選擇將所有設定檔ID納入 [!DNL MBI]. 檢查在設定檔選取步驟期間您要包含的設定檔ID。

**識別特定網站的Google Analytics設定檔ID:**

1. 登入 [!DNL Google Analytics]
1. 前往特定網站的 [!DNL Google Analytics] 儀表板
1. 查看URL — 設定檔ID對應至下列八個數字 `p` 在行尾：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 斷開連接 [!DNL Google Adwords]

1. 造訪您的 [!DNL Google] [帳戶設定](https://www.google.com/account/about/?hl=en) 頁面。
1. 在 `Security` ，然後按一下 **[!UICONTROL edit]** 下一頁 `Authorizing` 應用程式和網站。
1. 按一下 **[!UICONTROL revoke access]** 下一頁 [!DNL MBI].

## 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [透過追蹤訂單轉介來源 [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [在您的資料庫中追蹤使用者反向連結來源](../../analysis/google-track-user-acq.md)
* [探索您最有價值的贏取來源和管道](../../analysis/most-value-source-channel.md)
* [提高廣告宣傳的投資報酬率](../../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM歸因功能是否正常？](../../analysis/utm-attributes.md)
