---
title: 建立計算欄
description: 瞭解如何合併來自不同來源的資料。
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 建立計算欄

分析資料時，合併來自不同來源的資料會很有幫助。 想要依贏取來源將收入分組，連結來自`orders`資料表的資料和[!DNL Google Analytics]資料？ 您可能想要依客戶性別將收入分組，或將客戶屬性加入交易資料以進行分段。 本主題說明如何執行此作業。

開始使用前，Adobe建議您檢閱[計算資料行型別指南](../../data-analyst/data-warehouse-mgr/calc-column-types.md)，以取得您可以在Data Warehouse Manager中建立的資料行型別相關資訊，以及其定義和範例。

1. 若要開始，請按一下&#x200B;**[!DNL Manage Data > Data Warehouse]**。

1. 按一下您要在其中建立欄的表格。 例如，如果您想要為收入細分建立`Customer Gender`欄，則可選取`sales_flat_order`表格。

1. 隨即顯示表格配置。 按一下&#x200B;**[!UICONTROL Create New Column]**。

1. 為欄命名。 例如，`Customer Gender`。

1. 選取欄的定義。 這是[計算資料行型別指南](../data-warehouse-mgr/calc-column-types.md)方便的位置！

1. 對於某些型別的欄，需要更多資訊才能正確建立欄：

   * 對於`One to Many` （已聯結）和`Many to One` （彙總）欄，您必須選取資料表和欄。

   * 若為`Same Table calculation`，您必須從下拉式清單中選取所需的日期欄位。

如果您要建立`One to Many` （聯結）或`Many to One` （彙總）資料行，您必須選取一個路徑來連線兩個資料表。 在此步驟中，您可以使用現有路徑或建立路徑。

>[!NOTE]
>
>請記得將表格正確定義為多個或一個！

* 如有需要，您可以將[篩選器](../../data-user/reports/ess-manage-data-filters.md)套用至新資料行。

* 完成時，按一下&#x200B;**[!UICONTROL Save]**。

您的新欄會顯示在目前狀態為`Pending`的表格中。 下次更新完成後，您的欄將可用於量度和報表。

## 方便的參考地圖 {#map}

如果您在建立計算欄時無法記住所有輸入內容，請嘗試在建立時讓此參考地圖方便使用：

![](../../assets/Calculated_Columns_Example.png)

## 相關檔案

* [計算欄型別](../data-warehouse-mgr/calc-column-types.md)
* [進階計算欄型別](../data-warehouse-mgr/adv-calc-columns.md)
* [使用訂單和客戶資料建置 [!DNL Google ECommerce] 維度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
