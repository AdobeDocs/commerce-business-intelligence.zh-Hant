---
title: 審核Zendesk資料
description: 瞭解導出Zendesk資料的步驟。
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# 審核Zendesk資料

在你身上發現 [[!DNL Zendesk] 資料](../integrations/exp-zendesk-data.md)? 要查明問題，您需要瀏覽資料。 通過導出 [!DNL Zendesk] 資料到可下載檔案。

## 啟用資料導出

當前未為所有對象啟用資料導出 [!DNL Zendesk] 帳戶。 要激活此功能， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)，提到 [!DNL Zendesk] 子域名。

>[!NOTE]
>
>僅 `Enterprise` 和 `Plus` 計畫當前可以訪問此功能。

啟用資料導出後，只有特定電子郵件域中的管理員才能從 [!DNL Zendesk] 帳戶。 此電子郵件域通常與您的 [!DNL Zendesk]。 帳戶所有者的電子郵件域用作預設域，但您可以根據需要更改域。

## 導出到可下載檔案

1. 按一下邊欄中的「管理」表徵圖（齒輪徽標），然後選擇 **[!UICONTROL Manage** > **Reports]**。
1. 按一下 **[!UICONTROL Export]** 頁籤。
1. 按一下 **[!UICONTROL Request file]** 在「完全XML導出」旁邊，如下圖所示。

   此時，建設開始；完成後，您將通過電子郵件收到通知。
   ![reports_export_new_png](../../../assets/reports_export_new.png)

1. 按一下電子郵件通知中的連結以下載包含報告的zip檔案。

   此下載連結至少有三天有效。

此進程生成包含當前儲存的所有資訊的XML檔案 [!DNL Zendesk] 帳戶，包括票證資料（帶注釋）、用戶資料和帳戶資料。 現在，你可以 [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （請務必附加此檔案！） 這樣你就可以更仔細地查看資料了。 如果檔案太大，請與 [!DNL Commerce Intelligence] 團隊 [!DNL Dropbox] 或 [!DNL Google Drive]。

有關 [!DNL Zendesk] 檔案導出，請參閱 [[!DNL Zendesk] 導出文檔](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file)。
