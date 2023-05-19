---
title: 建立計算列
description: 瞭解如何整合來自不同來源的資料。
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 建立計算列

分析資料時，整合來自不同來源的資料會很有幫助。 希望按收購來源對收入進行分組，將資料與 `orders` 表格 [!DNL Google Analytics] 資料？ 您可能希望按客戶性別對收入進行分組，或將客戶屬性加入交易資料以進行細分。 本主題討論如何做到這一點。

開始之前，Adobe建議您查看 [計算列類型指南](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 有關可以在Data Warehouse管理器中建立的列類型及其定義和示例的資訊。

1. 要開始，請按一下 **[!DNL Manage Data > Data Warehouse]**。

1. 按一下要在其中建立列的表。 例如，如果要建立 `Customer Gender` 列以進行收入分段，您將選擇 `sales_flat_order` 的子菜單。

1. 將顯示表格方案。 按一下 **[!UICONTROL Create New Column]**。

1. 給列命名。 比如說， `Customer Gender`。

1. 選擇列的定義。 這裡 [計算列類型指南](../data-warehouse-mgr/calc-column-types.md) 派上用場了！

1. 對於某些類型的列，需要稍多一些資訊才能正確建立列：

   * 對於 `One to Many` （已加入） `Many to One` （聚合）列，需要選擇表和列。

   * 對於 `Same Table calculation`，您需要從下拉清單中選擇所需的日期欄位。

如果要建立 `One to Many` （已加入）或 `Many to One` (aggregate)列中，需要選擇連接兩個表的路徑。 在此步驟中，可以使用現有路徑或建立路徑。

>[!NOTE]
>
>切記將表正確定義為多個或一個！

* 如果需要，可以應用 [篩選](../../data-user/reports/ess-manage-data-filters.md) 的子菜單。

* 完成後，按一下 **[!UICONTROL Save]**。

新列將顯示在當前表中 `Pending` 狀態。 下次更新完成後，您的列將可用於度量和報告。

## 方便的參考地圖 {#map}

如果您在建立計算列時記不住所有輸入內容，請嘗試在構建時使此參考圖保持方便：

![](../../assets/Calculated_Columns_Example.png)

## 相關文檔

* [計算列類型](../data-warehouse-mgr/calc-column-types.md)
* [高級計算列類型](../data-warehouse-mgr/adv-calc-columns.md)
* [大樓 [!DNL Google ECommerce] 包含訂單和客戶資料的維](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
