---
title: 檢查更新週期狀態
description: 瞭解如何檢查更新週期狀態。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: d683f1362d87eee16c41ba9a8a83a9ff533b14aa
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 更新週期進度

當您登入[!DNL Adobe Commerce Intelligence]儀表板時，有數種方式可檢查您上次更新週期的狀態。 這完全取決於您擁有的[使用者許可權](../administrator/user-management/user-management.md)型別。

## 為何要檢查更新週期狀態？

當您稽核[!DNL Commerce Intelligence]帳戶中的資料時，檢查狀態更新週期會很有用。 如果您看到的[個結果不符合您的預期](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)，例如，[!DNL Commerce Intelligence]中的每日銷售與您在電子商務平台或[[!DNL Google] 電子商務收入](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=zh-Hant)中看到的不相符專案，您可以檢查最後一個資料點，以檢視問題在更新完成後是否得以解決。

## [!UICONTROL Read-Only]和[!UICONTROL Standard]位使用者

`Read-only`使用者可以登入其儀表板，並將滑鼠游標移至頁面右上角的圖示上，以檢視資料最近更新的時間。 這會顯示提取最後一個資料點的時間。

![介面中顯示的上次成功資料更新時間戳記](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin]位使用者

`Admin`使用者可以登入儀表板並檢視上方的最後一個資料點，以及其帳戶整合的簡短狀態圖示。

如需詳細資訊，管理員使用者可以按一下&#x200B;**[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**。

![管理資料整合頁面，顯示連線詳細資料和更新狀態](../../mbi/assets/detail-manage-data-integrations.png)

此頁面顯示目前的更新狀態以及上次完成更新的時間。

如果更新進行中，您會看到更新完成後要求電子郵件通知的連結。

如果更新不在進行中，您會看到強制開始更新的連結。

>[!NOTE]
>
>如果您設定了中斷時數（不希望[!DNL Commerce Intelligence]更新資料的時間），強制更新會啟動不遵守這些中斷時數限制的更新週期。


## 使用API檢查更新週期狀態

您可以使用&#x200B;**更新週期狀態API**&#x200B;來擷取最近完成的更新週期。

**要求**

```bash
curl -sS -H "X-RJM-API-Key: <EXPORT-API-KEY>" \
  https://api.rjmetrics.com/0.1/client/<CLIENT_ID>/fullupdatestatus
```

**回應（範例）**

```json
{
  "clientId": 194,
  "lastCompletedUpdateJob": {
    "id": 13554,
    "type": { "id": 2, "name": "Full Update" },
    "start": "2025-12-09 03:26:25",
    "end": "2025-12-09 03:29:03",
    "status": { "id": 4, "name": "Completed Successfully" }
  },
  "lastCompletedUpdateJobWithDataSync": null,
  "timezoneAbbreviation": "EST"
}
```

如需引數、驗證、錯誤和速率限制，請參閱開發人員檔案中的[更新週期狀態API](https://developer.adobe.com/commerce/services/reporting/update-cycle-status-api/)。
