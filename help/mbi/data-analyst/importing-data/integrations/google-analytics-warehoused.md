---
title: 連線Google Analytics倉儲
description: 瞭解如何追蹤訪客如何使用您的網站、哪些內容吸引人、訪客的退出位置等。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 連線[!DNL Google Analytics Warehoused]

>[!NOTE]
>
>需要[管理員許可權](../../../administrator/user-management/user-management.md)。

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics]是網際網路上使用最廣泛的網頁分析服務。 在您的網站上實作[!DNL Google Analytics]可讓您追蹤訪客如何使用您的網站、哪些內容吸引人、訪客的退出地點等等。 [!DNL Google Analytics Warehoused]與您現有的[!DNL Google Analytics]整合是獨立的整合。 由於您的Data Warehouse中有[!DNL Google Analytics]資料，不同於現有[!DNL Google Analytics]整合的即時摘要，因此可允許更佳的分析。 在[!DNL Commerce Intelligence]中分析這些量度，連同其他資料片段，可改善您網站的整體健康狀況和可用性。

## GA倉儲與Live整合的差異

主要區別在於一個整合已儲存([!DNL Google Analytics Warehoused])，而另一個則未儲存([!DNL Google Analytics Live])。 以[!DNL Google Analytics Warehoused]為例，這可讓您操控您的[!DNL Google Analytics]資料，並讓您結合[!DNL Google Analytics]和其他資料來源以建立深入分析的報告。

檢視[!DNL Google Analytics]個廣告行銷活動，以取得從操作觀點可以做些什麼的範例。 假設您在第四季有多個名稱不同的廣告行銷活動。 行銷活動是特定行銷活動的結果。 使用倉儲資料，您可以建立欄，找出有問題的行銷活動名稱，並傳回第四季方案名稱`Operation Dumbo`。

組合方面可讓[!DNL Google Analytics]資料與其他資料結合，以進行分析。 例如，從[!DNL Google Analytics]取得`Total Time On Site By Ad Campaign`個資料，並與[!DNL Facebook Ads]的`Total Spent Per Campaign`個資料結合，以完整瞭解有多少參與導致您成本。

另一方面，透過[!DNL Google Analytics Live]整合，每個[!DNL Google Analytics]圖表都像是未儲存在您Data Warehouse中的小型定址接收器。

## 正在連線[!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused]是`Premium`整合。 如果您有興趣將此整合新增至您的訂閱，請[連絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

1. 移至&#x200B;**[!UICONTROL Admin** > **Integrations]**&#x200B;下的`Connections`頁面。
1. 按一下位於右側的&#x200B;**[!UICONTROL Add an Integration]**。
1. 按一下[!DNL Google Analytics Warehoused]圖示。 這會開啟[!DNL Google Analytics]認證頁面。
1. 輸入您的[!DNL Google Analytics]認證。 完成授權程式後，系統會將您重新導向回[!DNL Commerce Intelligence]。
1. 設定檔ID清單隨即顯示。 檢查您要連線至[!DNL Commerce Intelligence]的設定檔。 如果您有多個設定檔，並且需要一些協助來識別哪一個，請參閱下面的「連線多個[!DNL Google Analytics]設定檔」一節。

## 正在連線多個[!DNL Google Analytics]設定檔

您可能有多個網站連線至單一[!DNL Google Analytics]帳戶，並以其自己的[!DNL Google Analytics]設定檔ID識別。 在此情況下，您可以選擇在[!DNL Commerce Intelligence]中包含您的所有設定檔ID。 在設定檔選取步驟中，檢查您要包含的設定檔ID。

若要識別特定網站的[!DNL Google Analytics]設定檔識別碼：

1. 登入[!DNL Google Analytics]
1. 前往特定網站的[!DNL Google Analytics]儀表板
1. 檢視URL — 設定檔ID對應至行尾在`p`之後的八個數字

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 正在從[!DNL Commerce Intelligence]中斷連線[!DNL Google Analytics Warehoused] {#disconnect}

1. 造訪您的[!DNL Google Analytics] [帳戶設定](https://myaccount.google.com/intro)頁面。
1. 在`Security`區段下，按一下`Authorizing`應用程式和網站旁的&#x200B;**[!UICONTROL edit]**。
1. 按一下[!DNL Commerce Intelligence]旁的&#x200B;**[!UICONTROL revoke access]**。

## 相關檔案

* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [正在連線 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析網站活動和客戶轉換率](../../analysis/web-act-cust-conversion.md)
* [使用 [!DNL Google Analytics] Cookie追蹤使用者贏取資料](../../analysis/google-track-user-acq.md)
