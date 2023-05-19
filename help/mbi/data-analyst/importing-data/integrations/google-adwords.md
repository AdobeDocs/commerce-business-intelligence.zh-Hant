---
title: 連接Google廣告詞
description: 通過將廣告成本與從您的市場活動中獲得的用戶的客戶生命週期價值(CLV)相結合，學習衡量市場活動ROI。
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 連接 [!DNL Google Adwords]

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/Google_Adwords_logo.png)

你做了調查，做了廣告，發佈了 [!DNL Google] 競選。 現在，是時候分析一下您的廣告支出資料，看看您的資金是否得到了有效的使用。 使用廣告支出資料，您 [將廣告成本與客戶生存期價值(CLV)相結合，以衡量市場活動的投資回報率](../../analysis/roi-ad-camp.md) 從您的市場活動中獲得的用戶。

通過輸入 [!DNL Google Adwords] 憑據 [!DNL Commerce Intelligence]。

1. 轉到 `Connections` 頁 **管理資料>整合**。
1. 按一下 **添加整合**，位於螢幕的右上側。
1. 按一下 **[!DNL Google Adwords]** 表徵圖 開啟 [!DNL Google Adwords] 「憑據」頁。
1. 輸入 [!DNL Google Analytics] 憑據。 在完成授權過程後，您將被重定向回 [!DNL Commerce Intelligence]。
1. 顯示配置檔案ID的清單。 檢查要連接到的配置檔案 [!DNL Commerce Intelligence]。

   ![](../../../assets/cnnct-profile.png)

1. 更改將自動保存，因此按一下 **[!UICONTROL Back to Connections]** 等你做完。

如果您有多個配置式，並且需要一些幫助來確定哪個是，請參閱 `Connecting Multiple Google Analytics profiles` 的下界。

## 連接多個 [!DNL Google Analytics] 配置檔案

您可能有多個網站連接到一個 [!DNL Google Analytics] 帳戶，由自己確定 [!DNL Google Analytics] 配置檔案ID。 在這種情況下，您可以選擇將所有配置檔案ID包括在 [!DNL Commerce Intelligence]。 檢查要在配置檔案選擇步驟中包括的配置檔案ID。

**要標識特定網站的Google Analytics配置檔案ID:**

1. 登錄 [!DNL Google Analytics]
1. 轉到特定網站 [!DNL Google Analytics] 儀表板
1. 查看URL — 配置檔案ID對應於以下八個數字 `p` 在行末：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 斷開 [!DNL Google Adwords]

1. 訪問 [!DNL Google] [帳戶設定](https://www.google.com/account/about/?hl=en) 的子菜單。
1. 在 `Security` ，按一下 **[!UICONTROL edit]** 下 `Authorizing` 應用程式和站點。
1. 按一下 **[!UICONTROL revoke access]**。

## 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [跟蹤訂單推薦來源 [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [跟蹤資料庫中的用戶推薦源](../../analysis/google-track-user-acq.md)
* [發現您最有價值的收購來源和渠道](../../analysis/most-value-source-channel.md)
* [提高廣告活動的ROI](../../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM歸因工作？](../../analysis/utm-attributes.md)
