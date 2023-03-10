---
title: 控制面板範圍篩選
description: 了解如何大量編輯特定控制面板上的所有報表。
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 控制面板範圍篩選

透過控制面板範圍的篩選，您可以大量編輯特定控制面板上的所有報表。 您可以快速檢視不同時段或不同商店的相同分析。 您可以輕鬆比較每家商店前一年、每月或每週的效能。 此外，您可以更新整個控制面板以容納新啟動的促銷活動。

## 日期篩選

若要變更控制面板上報表的日期範圍或間隔，請按一下右上角的日曆圖示(![日曆](../../assets/calendar-button.png))。

您可以選擇使用 `Fixed Date Range` 或各種預先計算 `Moving Date Ranges`:

![移動日期範圍](../../assets/moving_date_ranges.png)

此 `Last Full...` 移動範圍選項代表最近完全完成的範圍，而 `This...` 是目前的進行中範圍。 例如，如果是June，則 `Last Full Month` is _5月1日 — 5月31日_，同時 `This Month` is _6月1日 — 立即_.

或建立自己的 `Custom Moving Range`\:

![自訂移動範圍](../../assets/custom-moving-range.png)

選擇也更改間隔。 選取預設按鈕(![時間間隔預設值](../../assets/time_interval_default.png))表示僅會變更日期範圍：

![時間間隔](../../assets/time_interval.png)

若要將所有報表還原為其初始日期範圍和間隔，請按一下 **[!UICONTROL Restore Defaults]** 或按一下 **[!UICONTROL Cancel]**.

當您為控制面板指定日期篩選時，該篩選器只會套用至該控制面板。 導覽至其他控制面板時，系統不會套用此功能。

>[!NOTE]
>
>目前， `Cohort Reports` 和 `SQL Reports` 在控制面板層級套用變更時，不會納入。

## 儲存篩選器

若要分析特定商店的執行情形，請按一下右上角的商店圖示(![儲存篩選](../../assets/store-filter.png))。 依預設， `Store Filter` 設為 `All Stores`，會顯示所有 [商店檢視](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) 可在您的商務網站中使用。

>[!NOTE]
>
>整個商店會啟用或停用商店篩選 [!DNL MBI] 帳戶。 如果控制面板包含不受篩選器影響的報表（例如未在任何Commerce資料上建置的報表），則套用儲存篩選器時這些報表不會更新。 您可以 [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 如果您認為報表應根據商店選擇而更新，或您認為您的帳戶商店篩選條件已錯誤停用。

當您從 `Store Filter`，當您在控制面板之間導覽時，篩選器會保留您的選取項目。 保留您的選取項目，可讓您在選取之前，隨處查看所選儲存的資料 `All Stores`.

## 共用控制面板的篩選器

對於共用控制面板，如果某位使用者設定日期篩選，則擁有控制面板存取權的其他使用者會看見套用的相同篩選。 不過，此情況下不會套用儲存篩選。 如果控制面板擁有者設定儲存篩選並共用控制面板，則設定的儲存篩選不會持續保存給其他使用者。 使用者必須 [編輯存取](../../data-user/dashboards/share-dashboard-with-users.md) 調整控制面板篩選器。
