---
title: 稽核Zendesk資料
description: 瞭解匯出Zendesk資料的步驟。
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 稽核Zendesk資料

在您的[[!DNL Zendesk] 資料](../integrations/exp-zendesk-data.md)中發現一些奇怪的內容？ 若要查明問題，您需要探索資料。 您可以將[!DNL Zendesk]資料匯出至可下載的檔案來完成此操作。

## 啟用資料匯出

目前並未針對所有[!DNL Zendesk]帳戶啟用資料匯出。 若要啟用此功能，請[提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)，並提及您的[!DNL Zendesk]子網域名稱。

>[!NOTE]
>
>目前只有`Enterprise`和`Plus`個計畫可以存取此功能。

啟用資料匯出後，只有特定電子郵件網域中的管理員才能從您的[!DNL Zendesk]帳戶匯出資料。 此電子郵件網域通常與您的[!DNL Zendesk]為相同的電子郵件網域。 系統會使用帳戶擁有者的電子郵件網域作為預設網域，但如有需要，您可以變更網域。

## 匯出至可下載的檔案

1. 按一下側邊欄中的管理員圖示（齒輪標誌），然後選擇&#x200B;**[!UICONTROL Manage** > **Reports]**。
1. 按一下「**[!UICONTROL Export]**」標籤。
1. 按一下「完整XML匯出」旁的&#x200B;**[!UICONTROL Request file]**，如下圖所示。

   此時，組建開始；完成時您會透過電子郵件收到通知。
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. 按一下電子郵件通知中的連結，下載包含報表的zip檔案。

   此下載連結的有效期至少為三天。

此程式會建立一個XML檔案，其中包含您目前[!DNL Zendesk]帳戶中儲存的所有資訊，包括票證資料（包含註解）、使用者資料及帳戶資料。 此時，您可以[提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant) （請務必附加此檔案！），以便進一步檢視您的資料。 如果檔案太大，請透過[!DNL Commerce Intelligence]或[!DNL Dropbox]與[!DNL Google Drive]團隊共用。

如需[!DNL Zendesk]檔案匯出的詳細資訊，請參閱官方的[[!DNL Zendesk] 匯出檔案](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file)。
