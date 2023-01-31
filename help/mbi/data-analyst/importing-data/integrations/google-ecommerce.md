---
title: 連接Google電子商務
description: 了解您最重要的轉介管道。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Connect [!DNL Google ECommerce]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

您擁有穩定的流量和訂單流量，這表示您能有效觸及並贏取客戶。 但您最有價值的轉介管道為何？ 從一個來源獲得的客戶的平均期限值與從另一個來源獲得的客戶的平均期限值是多少？ 將訂單反向連結來源資料從 [!DNL Google ECommerce] to [!DNL MBI]，您可以建立分析以協助您識別 [最有價值的行銷管道](../../../data-analyst/analysis/most-value-source-channel.md).

讓我們從進入 [!DNL Google ECommerce] 憑證 [!DNL MBI]:

1. 前往 `Connections` 頁面底下 **[!UICONTROL Admin** > **Connections]**.
1. 按一下 **[!UICONTROL Add a New Source]**，位於畫面的右側，位於 `Data Sources` 表格。
1. 按一下 [!DNL Google ECommerce] 表徵圖。 這會開啟 [!DNL Google ECommerce] 憑據頁。
1. 輸入 [!DNL Google Analytics] 憑證。 授權程式完成後，系統會將您重新導向回 [!DNL MBI].
1. 將會顯示設定檔ID清單。 檢查您要連線的設定檔 [!DNL MBI].

   如果您有多個配置檔案，並且需要一些幫助來識別哪些是，請參閱**連接多個配置檔案 [!DNL Google Analytics] 設定檔一節。

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 變更會自動儲存，因此按一下「 」即可 **[!UICONTROL Back to Connections]** 時，才能執行此操作。

## 連接多個 [!DNL Google Analytics] 設定檔 [!DNL MBI]

您可能有多個網站連結至單一 [!DNL Google Analytics] 帳戶，以其自己的 [!DNL Google Analytics] 設定檔ID。 在此情況下，您可以選擇將所有設定檔ID納入 [!DNL MBI]. 只要檢查您要在設定檔選取步驟期間包含的設定檔ID即可。

識別特定網站的 [!DNL Google Analytics] 配置檔案ID:

1. 登入 [!DNL Google Analytics]
1. 前往特定網站的 [!DNL Google Analytics] 儀表板
1. 查看URL — 設定檔ID對應至下列8個數字 `p` 在行的結尾

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 斷開連接 [!DNL Google ECommerce] 從 [!DNL MBI] {#disconnect}

1. 造訪您的 [!DNL Google Analytics] [帳戶設定](https://www.google.com/accounts/) 頁面。
1. 在 `Security` ，按一下 **[!UICONTROL edit]** 下一頁 `Authorizing` 應用程式和網站。
1. 按一下 **[!UICONTROL revoke access]** 下一頁 [!DNL MBI].

## 相關：

* [預期 [!DNL Google ECommerce] 資料](../integrations/google-ecommerce-data.md)
* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
* [設定 [!DNL Google ECommerce] 追蹤](https://support.google.com/analytics/answer/1009612?hl=en)
* [探索您最有價值的贏取來源和管道](../../analysis/most-value-source-channel.md)
* [提高廣告宣傳的投資報酬率](../../analysis/roi-ad-camp.md)
