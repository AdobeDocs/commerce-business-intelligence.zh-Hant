---
title: 建立量度的篩選器集
description: 瞭解如何建立已儲存的篩選器集，並將其套用至量度。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 建立篩選器集

如果[!DNL Commerce Intelligence]中有多個量度需要以類似方式篩選（例如，篩選掉測試訂單），您可以建立已儲存的「篩選設定」並將它們套用至量度。 這樣可節省您的時間，因為在建立或編輯量度時，您不必新增個別篩選器。

如需詳細資訊，請參閱[訓練影片](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html)。

>[!NOTE]
>
>需要[管理員許可權](../../administrator/user-management/user-management.md)。

1. 按一下側邊欄中的&#x200B;**[!DNL Manage Data** > **Filter Sets]**。

   ![](../../assets/create-filter-sets.png)

1. 按一下頁面頂端的&#x200B;**[!UICONTROL Add Filter Set]**。

1. 選取包含您要篩選之量度的表格。

   例如，如果您要篩選`Total number of orders`量度且它是建置在`orders`資料表上，請選取該資料表。

1. 為`Filter Set`命名。

1. 新增所有相關篩選器。

   例如，如果您只想在`Total number of orders`量度中包含狀態為「完成」的訂單，則套用篩選條件，以排除所有沒有狀態= `complete`的訂單。

1. 驗證您的篩選邏輯，以及括弧與運運算元是否已正確放置：例如`\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`。

   不正確的篩選器通常是[!DNL Commerce Intelligence]個報表與預期結果之間資料不一致的原因。

1. 儲存`Filter Set`。

儲存篩選器集後，您可以將其套用至使用相同表格的任何量度。 例如，如果您在`orders`資料表上建立`Filter Set`，您可以將其套用至在此資料表上建置的&#x200B;*任何量度*，例如`Revenue`。

>[!NOTE]
>
>`Filter Sets`也可套用至[!DNL Commerce Intelligence]中的已計算資料行。 您可以透過連絡支援人員，要求將篩選器集套用至[!DNL Commerce Intelligence]中建立的資料維度。

## 相關

* [細分和篩選的最佳作法](../../best-practices/segment-filter.md)
