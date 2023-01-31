---
title: 建立計算列
description: 了解如何整合來自不同來源的資料。
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 建立計算列

分析資料時，合併來自不同來源的資料會很有幫助。 想要依贏取來源、連結訂單表格和Google Analytics的資料來將收入分組？ 或者，如何依客戶性別將收入分組，或將客戶屬性加入交易資料以進行細分？

本指南會教您如何做到。 開始之前，建議您先查看 [計算列類型指南](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 此 _計算列類型指南_ 概述可在「Data Warehouse管理器」中建立的欄類型及其定義和範例。

1. 若要開始，請按一下 **[!DNL Manage Data > Data Warehouse]** 欄。

1. 按一下要在中建立列的表。 例如，如果我們想要建立 `Customer Gender` 欄，我們會選取 `sales_flat_order` 表格。

1. 將顯示表格配置。 按一下 **[!UICONTROL Create New Column]**.

1. 為欄命名，例如 `Customer Gender`.

1. 選取欄的定義。 這是 [計算欄類型指南](../data-warehouse-mgr/calc-column-types.md) 會派上用場的！

1. 對於某些類型的欄，正確建立欄需要更多資訊：
   * 針對 `One to Many` （已連結）和 `Many to One` （匯總）欄，您需要選取表格和欄。
   * 若 `Same Table calculation`，您需要從下拉式清單中選取所需的日期欄位。

如果您要建立 `One to Many` （連結）或 `Many to One` （聚合）列，需要選擇連接兩個表的路徑。 在此步驟中，您可以使用現有路徑或建立新路徑。

>[!NOTE]
>
>請記得將表格正確定義為多個或一個表格！

* 如有需要，您可以套用 [篩選器](../../data-user/reports/ess-manage-data-filters.md) 到新欄。
* 完成後，按一下 **[!UICONTROL Save]**.

就這樣！ 您的新欄將以 `Pending` 狀態。 下次更新完成後，您的欄便可在量度和報表中使用。

## 實用的參考圖 {#map}

如果您在建立計算欄時記住所有輸入內容有些困難，請在建立時試著讓此參考圖保持便利：

![](../../assets/Calculated_Columns_Example.png)

## 相關檔案

* [計算的列類型](../data-warehouse-mgr/calc-column-types.md)
* [高級計算列類型](../data-warehouse-mgr/adv-calc-columns.md)
* [建置 [!DNL Google ECommerce] 包含訂單和客戶資料的維度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
