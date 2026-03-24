---
title: 連線Google Adwords
description: 瞭解如何將您的廣告成本與從您的行銷活動取得的使用者客戶期限值(CLV)結合，以評估行銷活動ROI。
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/mZ8R2vPyFy8pGpYi4KhqocVnP-OlgMPGU3KJ4C9vsTo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 322
ht-degree: 0%

---

# 連線[!DNL Google Adwords]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![Google AdWords標誌](../../../assets/Google_Adwords_logo.png)

您做了調查、製作了自己的廣告、啟動了[!DNL Google]行銷活動。 現在，您可以分析廣告支出資料，看看您的錢是否花得有效率。 使用您的廣告支出資料，您可以將您的廣告成本與客戶期限值(CLV)配對[評估行銷活動ROI （從行銷活動取得的使用者）](../../analysis/roi-ad-camp.md)。

在[!DNL Google Adwords]中輸入您的[!DNL Commerce Intelligence]認證以開始。

1. 移至`Connections`管理資料>整合&#x200B;**底下的**&#x200B;頁面。
1. 按一下熒幕右上角的&#x200B;**新增整合**。
1. 按一下&#x200B;**[!DNL Google Adwords]**&#x200B;圖示。 這會開啟[!DNL Google Adwords]認證頁面。
1. 輸入您的[!DNL Google Analytics]認證。 完成授權程式後，系統會將您重新導向回[!DNL Commerce Intelligence]。
1. 設定檔ID清單隨即顯示。 檢查您要連線至[!DNL Commerce Intelligence]的設定檔。

   ![Google AdWords連線對話方塊顯示設定檔選取專案](../../../assets/cnnct-profile.png)

1. 變更會自動儲存，因此完成時請按一下&#x200B;**[!UICONTROL Back to Connections]**。

如果您有多個設定檔，且需要一些協助來識別哪一個，請參閱下列`Connecting Multiple Google Analytics profiles`區段。

## 正在連線多個[!DNL Google Analytics]設定檔

您可能有多個網站連線至單一[!DNL Google Analytics]帳戶，並以其自己的[!DNL Google Analytics]設定檔ID識別。 在此情況下，您可以選擇在[!DNL Commerce Intelligence]中包含您的所有設定檔ID。 在設定檔選取步驟中，核取您要包含的設定檔ID。

**識別特定網站的Google Analytics設定檔識別碼：**

1. 登入[!DNL Google Analytics]
1. 前往特定網站的[!DNL Google Analytics]儀表板
1. 檢視URL — 設定檔ID對應至行尾在`p`之後的八個數字：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 正在中斷連線[!DNL Google Adwords]

1. 造訪您的[!DNL Google] [帳戶設定](https://www.google.com/account/about/?hl=en)頁面。
1. 在`Security`區段下，按一下&#x200B;**[!UICONTROL edit]**&#x200B;應用程式和網站旁的`Authorizing`。
1. 按一下&#x200B;**[!UICONTROL revoke access]**。

## 相關

* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
* [透過 [!DNL Google ECommerce]追蹤訂單轉介來源](../integrations/google-ecommerce.md)
* [追蹤資料庫中的使用者反向連結來源](../../analysis/google-track-user-acq.md)
* [探索您最有價值的贏取來源和管道](../../analysis/most-value-source-channel.md)
* [提高廣告行銷活動的ROI](../../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM歸因如何運作？](../../analysis/utm-attributes.md)
