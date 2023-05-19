---
title: 管理資料維
description: 瞭解維是什麼，並可用於根據度量篩選或分段圖表。
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# 管理資料維

>[!NOTE]
>
>需要 [管理權限](../../administrator/user-management/user-management.md)。

維是表中與度量相同的欄位，可用於根據該度量篩選圖表或對圖表進行分段。 例如，收入度量可能包含城市、州、國家、訂單狀態、優惠券代碼和其他類型的維。

## 將維添加到多個度量

要一次將一個或多個維添加到多個度量：

1. 轉到 **[!UICONTROL Manage Data > Metrics]**。

1. 按一下 **[!UICONTROL Add Dimensions To Metric(s)]**。

1. 選擇包含維的表。

1. 在 `Choose Metric(s) to Add Dimensions` 列中，選擇要添加維的度量。 選擇後， `Choose Dimensions to Add` 列。 檢查要添加到選定度量的維。

   ![](../../assets/Add_Dimensions.png)

1. 如果要按報表上的任何資料維進行分段或分組，請確保指出 _可分組_。

1. 按一下 **[!UICONTROL Add]**。

## 從多個度量中刪除維

要從多個度量中刪除一個或多個維：

1. 轉到 **[!UICONTROL Data > Metrics]**。

1. 按一下 **[!UICONTROL Remove Dimensions From Metric(s)]**。

1. 選擇包含維的表。

1. 選擇要從左側刪除維的度量，以及要在右側刪除的維。

1. 按一下 **[!UICONTROL Remove]**。

1. 如果維正在報表上使用，則會顯示一個警告，其中顯示使用維的圖表清單。 按一下 **[!UICONTROL Delete]** 刪除選定維及其所有依存對象（包括報表）。

## 管理度量中的維

**要在度量中添加維：**

1. 轉到 **[!UICONTROL Data > Metrics]**。

1. 按一下 **[!UICONTROL Edit]** 在要新維的度量上。

1. 在 `Dimensions` ，使用 `Add a dimension` 下拉菜單以選擇要添加的維。

>[!NOTE]
>
>要篩選或分組依據的任何維都必須在中跟蹤 [!DNL Commerce Intelligence]。 如果找不到所需的維，可能需要通過 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 的子菜單。


**要從度量中刪除維：**

1. 轉到 **[!UICONTROL Manage Data > Metrics]**。

1. 按一下 **[!UICONTROL Edit]** 在要新維的度量上。

1. 在 `Dimensions` 部分，選中要刪除的維旁邊的刪除列中的複選框。

>[!NOTE]
>
>即使刪除維後，它仍作為列存在於Data Warehouse中。 您可以將其添加回任何度量，並使用這些維構建新度量。 刪除維與之對應的資料列 [!DNL Commerce Intelligence]，只需通過 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 的子菜單。

## 相關文檔

* [分段和過濾的最佳做法](../../best-practices/segment-filter.md)
