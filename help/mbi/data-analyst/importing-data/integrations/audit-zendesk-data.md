---
title: 審核Zendesk資料
description: 了解匯出Zendesk資料的步驟。
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 審核Zendesk資料

在你的 [[!DNL Zendesk] 資料](../integrations/exp-zendesk-data.md)? 若要找出問題，您需要探索您的資料。 您可以匯出 [!DNL Zendesk] 資料至可下載的檔案。

## 啟用資料匯出

目前未針對所有項目啟用資料匯出 [!DNL Zendesk] 帳戶。 若要啟用此功能， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en)，提及 [!DNL Zendesk] 子網域名稱。

>[!NOTE]
>
>僅 `Enterprise` 和 `Plus` 計畫當前可以訪問此功能。

啟用資料匯出後，只有特定電子郵件網域的管理員才能從 [!DNL Zendesk] 帳戶。 此電子郵件網域通常與您的 [!DNL Zendesk]. 帳戶擁有者的電子郵件網域是預設網域，但您可以視需要變更網域。

## 匯出至可下載的檔案

1. 按一下側邊欄中的「管理員」圖示（齒輪標誌），然後選擇 **[!UICONTROL Manage** > **Reports]**.
1. 按一下 **[!UICONTROL Export]** 標籤。
1. 按一下 **[!UICONTROL Request file]** ，如下圖所示。

   此時，建築開始；完成時會透過電子郵件通知您。
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. 按一下電子郵件通知中的連結，以下載包含報表的zip檔案。

   此下載連結至少有三天有效。

此過程將構建一個XML檔案，其中包含當前儲存的所有資訊 [!DNL Zendesk] 帳戶，包括票證資料（含註解）、使用者資料和帳戶資料。 此時，您可以 [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) （請務必附加此檔案！） 以便您更仔細地查看資料。 如果檔案過大，請與共用 [!DNL MBI] 團隊經由 [!DNL Dropbox] 或 [!DNL Google Drive].

如需 [!DNL Zendesk] 檔案匯出，請參閱 [[!DNL Zendesk] 匯出檔案](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
