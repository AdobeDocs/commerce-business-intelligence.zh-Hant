---
title: 儀表板範圍的篩選
description: 瞭解如何對特定儀表板上的所有報告進行批量編輯。
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 儀表板範圍的篩選

通過儀表板範圍的篩選，您可以對特定儀表板上的所有報告進行批量編輯。 您可以在不同時段或不同商店中快速查看相同的分析。 您可以輕鬆比較上一年、每月或每週的效能。 您可以更新整個儀表板以適應新啟動的市場活動。

## 日期篩選器

要更改儀表板上報告的日期範圍或間隔，請按一下右上角的日曆表徵圖(![日曆](../../assets/calendar-button.png))。

您可以選擇使用 `Fixed Date Range` 或各種預計算 `Moving Date Ranges`:

![移動日期範圍](../../assets/moving_date_ranges.png)

的 `Last Full...` 移動範圍選項表示最近完全完成的範圍，而 `This...` 是當前的正在進行的範圍。 例如，如果是June, `Last Full Month` 是 _5月1日 — 5月31日_, `This Month` 是 _6月1日 — 現在_。

或建立自己的 `Custom Moving Range`\:

![自定義移動範圍](../../assets/custom-moving-range.png)

選擇也更改間隔。 選擇預設按鈕(![時間間隔預設值](../../assets/time_interval_default.png))表示只更改日期範圍：

![時間間隔](../../assets/time_interval.png)

要將所有報告恢復到其初始日期範圍和時間間隔，請按一下 **[!UICONTROL Restore Defaults]** 按一下 **[!UICONTROL Cancel]**。

為儀表板指定日期篩選器時，該篩選器僅應用於該儀表板。 導航到其他儀表板時，不應用此選項。

>[!NOTE]
>
>目前， `Cohort Reports` 和 `SQL Reports` 在儀表板級別應用更改時不包括。

## 儲存篩選器

要分析特定儲存的執行方式，請按一下右上角的儲存表徵圖(![儲存篩選器](../../assets/store-filter.png))。 預設情況下， `Store Filter` 設定為 `All Stores`，顯示所有資料 [儲存視圖](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) 在您的Commerce網站中。

>[!NOTE]
>
>整個儲存篩選器已啟用或禁用 [!DNL Commerce Intelligence] 帳戶。 如果儀表板包含不受篩選器影響的報告（例如未在任何篩選器上構建的報告） [!DNL Adobe Commerce] 資料)時，這些報告在應用儲存篩選器時不會更新。 你可以 [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果您認為報告應根據儲存選擇進行更新，或者您認為帳戶儲存篩選器被錯誤禁用。

從中選擇商店時 `Store Filter`，在儀表板之間導航時，篩選器將保留您的選擇。 保留您的選擇後，您可以查看所選儲存的資料，直到您選擇 `All Stores`。

## 共用儀表板的篩選器

對於共用儀表板，如果一個用戶配置了日期篩選器，則具有儀表板訪問權限的其他用戶將看到應用了同一篩選器。 但是，此情況下儲存篩選器不適用。 如果儀表板所有者配置儲存篩選器並共用儀表板，則配置的儲存篩選器不會持續給其他用戶。 用戶必須 [編輯訪問](../../data-user/dashboards/share-dashboard-with-users.md) 到操控板以調整操控板濾鏡。
