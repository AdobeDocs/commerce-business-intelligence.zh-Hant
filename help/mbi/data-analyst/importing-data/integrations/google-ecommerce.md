---
title: 連線Google電子商務
description: 瞭解您最有價值的轉介管道。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 連線[!DNL Google ECommerce]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![](../../../assets/google-ecommerce-logo.png)

您有穩定的流量和訂單流，這表示您有效地觸及和贏取客戶。 但您最有價值的轉介管道為何？ 從某個來源取得的客戶平均期限值相對於從另一個來源取得的客戶為何？ 將您的訂單轉介來源資料從[!DNL Google ECommerce]連線至[!DNL Commerce Intelligence]，即可建置分析，協助您識別[最有價值的行銷管道](../../../data-analyst/analysis/most-value-source-channel.md)。

在[!DNL Commerce Intelligence]中輸入您的[!DNL Google ECommerce]認證以開始使用：

1. 移至&#x200B;**[!UICONTROL Admin** > **Connections]**&#x200B;下的`Connections`頁面。

1. 按一下`Data Sources`表格上方熒幕右側的&#x200B;**[!UICONTROL Add a New Source]**。

1. 按一下[!DNL Google ECommerce]圖示。 這會開啟[!DNL Google ECommerce]認證頁面。

1. 輸入您的[!DNL Google Analytics]認證。 授權程式完成後，您將被重新導向回[!DNL Commerce Intelligence]。

1. 設定檔ID清單隨即顯示。 檢查您要連線至[!DNL Commerce Intelligence]的設定檔。

   如果您有多個設定檔且需要一些協助來識別哪一個，請參閱下面的**連線多個[!DNL Google Analytics]設定檔區段。

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 變更會自動儲存，因此完成時請按一下&#x200B;**[!UICONTROL Back to Connections]**。

## 正在將多個[!DNL Google Analytics]設定檔連線到[!DNL Commerce Intelligence]

您可能有多個網站連線至單一[!DNL Google Analytics]帳戶，並以其自己的[!DNL Google Analytics]設定檔ID識別。 在此情況下，您可以選擇在[!DNL Commerce Intelligence]中包含您的所有設定檔ID。 在設定檔選取步驟中，檢查您要包含的設定檔ID。

若要識別特定網站的[!DNL Google Analytics]設定檔識別碼：

1. 登入[!DNL Google Analytics]。
1. 前往特定網站的[!DNL Google Analytics]儀表板。
1. 檢視URL — 設定檔ID對應至行尾在`p`之後的八個數字。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 正在從[!DNL Commerce Intelligence]中斷連線[!DNL Google ECommerce] {#disconnect}

1. 造訪您的[!DNL Google Analytics] [帳戶設定](https://www.google.com/account/about/?hl=en)頁面。
1. 在`Security`區段下，按一下`Authorizing`應用程式和網站旁的&#x200B;**[!UICONTROL edit]**。
1. 按一下[!DNL Commerce Intelligence]旁的&#x200B;**[!UICONTROL revoke access]**。

## 相關：

* [預期 [!DNL Google ECommerce] 資料](../integrations/google-ecommerce-data.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [正在設定 [!DNL Google ECommerce] 追蹤](https://support.google.com/analytics/answer/1009612?hl=en)
* [探索您最有價值的贏取來源和管道](../../analysis/most-value-source-channel.md)
* [提高廣告行銷活動的ROI](../../analysis/roi-ad-camp.md)
