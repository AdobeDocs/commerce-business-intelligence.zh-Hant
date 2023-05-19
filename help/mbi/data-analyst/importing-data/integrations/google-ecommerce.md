---
title: 連接Google電子商務
description: 瞭解您最重要的推薦渠道。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 連接 [!DNL Google ECommerce]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/google-ecommerce-logo.png)

您擁有穩定的流量和訂單流，這意味著您能夠有效地接觸和獲取客戶。 但您最有價值的推薦渠道是什麼？ 從一個來源獲得的客戶與從另一個來源獲得的客戶的平均生命週期價值是多少？ 通過連接訂單推薦源資料 [!DNL Google ECommerce] 至 [!DNL Commerce Intelligence]，可以生成分析以幫助您識別 [最有價值的營銷渠道](../../../data-analyst/analysis/most-value-source-channel.md)。

通過輸入 [!DNL Google ECommerce] 憑據 [!DNL Commerce Intelligence]:

1. 轉到 `Connections` 頁 **[!UICONTROL Admin** > **Connections]**。

1. 按一下 **[!UICONTROL Add a New Source]**，位於螢幕右側，位於 `Data Sources` 的子菜單。

1. 按一下 [!DNL Google ECommerce] 表徵圖 開啟 [!DNL Google ECommerce] 「憑據」頁。

1. 輸入 [!DNL Google Analytics] 憑據。 在完成授權過程後，您將被重定向回 [!DNL Commerce Intelligence]。

1. 顯示配置檔案ID的清單。 檢查要連接到的配置檔案 [!DNL Commerce Intelligence]。

   如果您有多個配置式，並且需要一些幫助來確定哪個是，請參閱**連接多個配置式 [!DNL Google Analytics] 配置檔案部分。

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 更改將自動保存，因此按一下 **[!UICONTROL Back to Connections]** 的雙曲餘切值。

## 連接多個 [!DNL Google Analytics] 配置檔案 [!DNL Commerce Intelligence]

您可能有多個網站連接到一個 [!DNL Google Analytics] 帳戶，由自己確定 [!DNL Google Analytics] 配置檔案ID。 在這種情況下，您可以選擇將所有配置檔案ID包含在 [!DNL Commerce Intelligence]。 檢查要在配置檔案選擇步驟中包括的配置檔案ID。

確定特定網站的 [!DNL Google Analytics] 配置檔案ID:

1. 登錄 [!DNL Google Analytics]。
1. 轉到特定網站 [!DNL Google Analytics] 控制項欄。
1. 查看URL — 配置檔案ID對應於以下八個數字 `p` 最後一段。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 斷開 [!DNL Google ECommerce] 從 [!DNL Commerce Intelligence] {#disconnect}

1. 訪問 [!DNL Google Analytics] [帳戶設定](https://www.google.com/account/about/?hl=en) 的子菜單。
1. 在 `Security` ，按一下 **[!UICONTROL edit]** 下 `Authorizing` 應用程式和站點。
1. 按一下 **[!UICONTROL revoke access]** 下 [!DNL Commerce Intelligence]。

## 相關：

* [預期 [!DNL Google ECommerce] 資料](../integrations/google-ecommerce-data.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [設定 [!DNL Google ECommerce] 跟蹤](https://support.google.com/analytics/answer/1009612?hl=en)
* [發現您最有價值的收購來源和渠道](../../analysis/most-value-source-channel.md)
* [提高廣告活動的ROI](../../analysis/roi-ad-camp.md)
