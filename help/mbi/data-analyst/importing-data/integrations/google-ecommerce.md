---
title: 連線Google電子商務
description: 瞭解您最有價值的轉介管道。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iBVf-dkbm1NbELZUYjLp1TzypO7Cu55tIzd93lQ1zo0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
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
source-wordcount: 305
ht-degree: 0%

---

# 連線[!DNL Google ECommerce]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![Google電子商務標誌](../../../assets/google-ecommerce-logo.png)

您有穩定的流量和訂單流，這表示您有效地觸及和贏取客戶。 但您最有價值的轉介管道為何？ 從某個來源取得的客戶平均期限值相對於從另一個來源取得的客戶為何？ 將您的訂單轉介來源資料從[!DNL Google ECommerce]連線至[!DNL Commerce Intelligence]，即可建置分析，協助您識別[最有價值的行銷管道](../../../data-analyst/analysis/most-value-source-channel.md)。

在[!DNL Google ECommerce]中輸入您的[!DNL Commerce Intelligence]認證以開始使用：

1. 移至`Connections`下的&#x200B;**[!UICONTROL Admin** > **Connections]**&#x200B;頁面。

1. 按一下&#x200B;**[!UICONTROL Add a New Source]**&#x200B;表格上方熒幕右側的`Data Sources`。

1. 按一下[!DNL Google ECommerce]圖示。 這會開啟[!DNL Google ECommerce]認證頁面。

1. 輸入您的[!DNL Google Analytics]認證。 授權程式完成後，您將被重新導向回[!DNL Commerce Intelligence]。

1. 設定檔ID清單隨即顯示。 檢查您要連線至[!DNL Commerce Intelligence]的設定檔。

   如果您有多個設定檔且需要一些協助來識別哪一個，請參閱下面的**連線多個[!DNL Google Analytics]設定檔區段。

   ![顯示連線多個Google Analytics設定檔之選項的表單](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 變更會自動儲存，因此完成時請按一下&#x200B;**[!UICONTROL Back to Connections]**。

## 正在將多個[!DNL Google Analytics]設定檔連線到[!DNL Commerce Intelligence]

您可能有多個網站連線至單一[!DNL Google Analytics]帳戶，並以其自己的[!DNL Google Analytics]設定檔ID識別。 在此情況下，您可以選擇在[!DNL Commerce Intelligence]中包含您的所有設定檔ID。 在設定檔選取步驟中，檢查您要包含的設定檔ID。

若要識別特定網站的[!DNL Google Analytics]設定檔識別碼：

1. 登入[!DNL Google Analytics]。
1. 前往特定網站的[!DNL Google Analytics]儀表板。
1. 檢視URL — 設定檔ID對應至行尾在`p`之後的八個數字。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 正在從[!DNL Google ECommerce]中斷連線[!DNL Commerce Intelligence] {#disconnect}

1. 造訪您的[!DNL Google Analytics] [帳戶設定](https://www.google.com/account/about/?hl=en)頁面。
1. 在`Security`區段下，按一下&#x200B;**[!UICONTROL edit]**&#x200B;應用程式和網站旁的`Authorizing`。
1. 按一下&#x200B;**[!UICONTROL revoke access]**&#x200B;旁的[!DNL Commerce Intelligence]。

## 相關：

* [預期 [!DNL Google ECommerce] 資料](../integrations/google-ecommerce-data.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [正在設定 [!DNL Google ECommerce] 追蹤](https://support.google.com/analytics/answer/1009612?hl=en)
* [探索您最有價值的贏取來源和管道](../../analysis/most-value-source-channel.md)
* [提高廣告行銷活動的ROI](../../analysis/roi-ad-camp.md)
