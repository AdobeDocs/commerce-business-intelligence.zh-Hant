---
title: 建立量度的篩選器集
description: 了解如何建立儲存的篩選器集並將其套用至量度。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 建立篩選集

若您的 [!DNL MBI] 您可以建立儲存的篩選集，並將篩選集套用至量度，這需要以類似方式篩選（例如篩選掉測試順序）。 這樣可節省時間，因為您在建立或編輯量度時不需要新增個別篩選器。

請參閱 [訓練影片](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=en) 了解更多。

>[!NOTE]
>
>需要 [管理權限](../../administrator/user-management/user-management.md).

1. 按一下 **[!DNL Manage Data** > **Filter Sets]** 欄。

   ![](../../assets/create-filter-sets.png)

1. 按一下 **[!UICONTROL Add Filter Set]** 頁面頂端。

1. 選取包含您要篩選之量度的表格。

   例如，如果您要篩選 `Total number of orders` 量度，而且是以 `orders` 表格，選擇該表格。

1. 將 `Filter Set`.

1. 新增所有相關篩選器。

   例如，如果您只想在 `Total number of orders` 量度時，您會套用篩選器，排除所有沒有狀態=的訂單 `complete`.

1. 驗證篩選邏輯，並確認括弧和運算子已正確放置：例如， `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   錯誤的篩選器通常是 [!DNL MBI] 報告和預期結果。

1. 儲存 `Filter Set`.

儲存篩選器集後，您可將其套用至使用相同表格的任何量度。 例如，如果您建立 `Filter Set` 在 `orders` 表格，您可將其套用至 *任何量度* 建置在此表格上，例如 `Revenue`.

>[!NOTE]
>
>`Filter Sets` 也可套用至 [!DNL MBI]. 您可以要求將篩選器集套用至中建立的資料維度 [!DNL MBI] 透過連絡支援。

## 相關

* [分段和篩選的最佳實務](../../best-practices/segment-filter.md)
