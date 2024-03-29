---
title: 建立量度的篩選器集
description: 瞭解如何建立已儲存的篩選器集，並將其套用至量度。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 建立篩選器集

如果您有多個量度 [!DNL Commerce Intelligence] （例如，篩選掉測試訂單）建立已儲存的「篩選設定」，並將它們套用至量度。 這樣可節省您的時間，因為在建立或編輯量度時，您不必新增個別篩選器。

請參閱 [訓練影片](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) 以取得詳細資訊。

>[!NOTE]
>
>需要 [管理員許可權](../../administrator/user-management/user-management.md).

1. 按一下 **[!DNL Manage Data** > **Filter Sets]** 在側邊欄中。

   ![](../../assets/create-filter-sets.png)

1. 按一下 **[!UICONTROL Add Filter Set]** ，位於頁面頂端。

1. 選取包含您要篩選之量度的表格。

   例如，如果您想要篩選 `Total number of orders` 量度且建立在 `orders` 表格中，選取該表格。

1. 為命名 `Filter Set`.

1. 新增所有相關篩選器。

   例如，如果您只想在您的訂單中包含狀態為「完成」的訂單， `Total number of orders` 量度，您可以套用篩選器，以排除所有沒有狀態的訂單= `complete`.

1. 驗證您的篩選邏輯，以及括弧和運運算元是否已正確放置：例如， `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   不正確的篩選器通常是造成兩者資料不一致的原因 [!DNL Commerce Intelligence] 報表與預期結果。

1. 儲存 `Filter Set`.

儲存篩選器集後，您可以將其套用至使用相同表格的任何量度。 例如，如果您建立 `Filter Set` 於 `orders` 表格，您可以將其套用至 *任何量度* 建置在此表格上，例如 `Revenue`.

>[!NOTE]
>
>`Filter Sets` 也可套用至中的計算欄 [!DNL Commerce Intelligence]. 您可以要求將篩選器集套用至中建立的資料維度 [!DNL Commerce Intelligence] 聯絡支援人員。

## 相關

* [細分和篩選的最佳作法](../../best-practices/segment-filter.md)
