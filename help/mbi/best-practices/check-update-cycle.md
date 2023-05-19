---
title: 檢查更新週期狀態
description: 瞭解如何檢查更新週期狀態。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# 更新週期進度

當你登錄 [!DNL Adobe Commerce Intelligence] 儀表板，有多種方法可檢查上次更新週期的狀態。 都取決於 [用戶權限](../administrator/user-management/user-management.md) 你有。

## 為什麼應檢查更新週期狀態？

檢查狀態更新週期在您審核中的資料時非常有用 [!DNL Commerce Intelligence] 帳戶。 如果你看到 [不符合預期的結果](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)，例如，在 [!DNL Commerce Intelligence] 與您在電子商務平台或您的 [[!DNL Google] 電子商務收入](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 您可以檢查最後一個資料點，以查看更新完成後問題是否已解決。

## [!UICONTROL Read-Only] 和 [!UICONTROL Standard] 用戶

`Read-only` 用戶可以登錄到其儀表板，並通過懸停在頁面右上角的表徵圖上查看資料最近的更新時間。 這顯示上一個資料點的拉取時間。

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] 用戶

`Admin` 用戶可以登錄到儀表板並查看上面的最後一個資料點，以及其帳戶整合的簡短狀態表徵圖。

有關詳細資訊，管理員用戶可以按一下 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**。

![](../../mbi/assets/detail-manage-data-integrations.png)

此頁顯示當前更新狀態和上次完成更新的時間。

如果正在進行更新，則在更新完成後，您將看到一個連結來請求電子郵件通知。

如果更新未進行，則會看到一個連結以強制啟動更新。

>[!NOTE]
>
>如果您有停電時間(您不想 [!DNL Commerce Intelligence] 要更新資料)集，強制更新將啟動不遵守這些封鎖時間限制的更新週期。
