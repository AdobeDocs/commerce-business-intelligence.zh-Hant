---
title: 管理資料維度
description: 了解資料的產生方式、確切導致新列插入核心商務其中一列的原因，以及進行購買或建立帳戶等動作記錄至商務資料庫的方式。
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 管理資料維度

>[!NOTE]
>
>需要 [管理權限](../../administrator/user-management/user-management.md).

維度是表格中的欄位，可用來根據該量度篩選或分段圖表。 例如，收入量度可能包含城市、州、國家、訂單狀態、抵用券代碼和其他類型的維度。

## 新增維度至多個量度

若要一次新增一或多個維度至多個量度：

1. 在主導覽列上，前往 **[!UICONTROL Manage Data > Metrics]**.

1. 在頁面頂端，按一下 **[!UICONTROL Add Dimensions To Metric(s)]**.

1. 選擇包含維的表。

1. 在 `Choose Metric(s) to Add Dimensions` 欄，選取您要新增維度的量度。 選取後， `Choose Dimensions to Add` 欄會顯示在右側。 勾選您要新增至所選量度的維度。

   ![](../../assets/Add_Dimensions.png)

1. 如果您想要依報表上的任何資料維度來劃分或分組，請務必指出 _可分組_.

1. 按一下 **[!UICONTROL Add]**.

## 從多個量度刪除維度

若要從多個量度中刪除一或多個維度：

1. 在主導覽列上，前往 **[!UICONTROL Data > Metrics]**.

1. 在頁面頂端，按一下 **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. 選擇包含維的表。

1. 選取您要從左側移除的量度，以及要在右側移除的維度。

1. 按一下 **[!UICONTROL Remove]**.

1. 如果維度正在報表上使用，則會顯示警告和使用維度的圖表清單。 按一下 **[!UICONTROL Delete]** 刪除選定的維及其所有從屬項，包括報表。

## 管理量度中的維度

**若要在量度中新增維度：**

1. 在主導覽列上，前往 **[!UICONTROL Data > Metrics]**.

1. 按一下 **[!UICONTROL Edit]** 在您要新維度的量度上。

1. 在 `Dimensions` 區段，請使用 `Add a dimension` 下拉式清單，選取要新增的維度。

>[!NOTE]
>
>要篩選或分組依據的任何維都必須已在 [!DNL MBI]. 如果您找不到所需的維度，我們可能需要透過 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 頁面。


**若要從量度刪除維度：**

1. 在主導覽列上，前往 **[!UICONTROL Manage Data > Metrics]**.

1. 按一下 **[!UICONTROL Edit]** 在您要新維度的量度上。

1. 在 `Dimensions` 區段中，選取您要移除之維度旁之刪除欄中的核取方塊。

>[!NOTE]
>
>即使刪除維度後，它仍作為欄存在於我們的資料倉庫中的表格中。 您可以將其新增至任何量度，並使用這些維度建立新量度。 要刪除資料列，維與 [!DNL MBI]，只需透過 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 頁面。

## 相關檔案

* [分段和篩選的最佳實務](../../best-practices/segment-filter.md)
